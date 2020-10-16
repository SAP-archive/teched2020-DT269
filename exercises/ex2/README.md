# Exercise 2 - Implement extensional functions in Kyma runtime

In this exercise, we will create several serverless functions for extensional service purposes.

- **itcm-func-exec**</br>
Consumer for ITCM domain event.

- **itcm-func-fetch**</br>
Expose fetch API for mobile App to list domain event notifications.

- **itcm-func-upload**</br>
Expose upload API for mobile App to upload invoice pic.
call a 3rd party OCR service, analyse and extract remark. 
Update claim with the remark and attachment in ITCM.    

## Step 2.1 - Create an exec function for consuming ITCM domain events

function **itcm-func-exec**</br>
Subscribe to the ITCM domain event, persist the event to a Redis cluster when the event is triggered.

Create itcm-func-exec.
![](/exercises/ex2/images/e2-func-exec.png)

Write code in function source.
![](/exercises/ex2/images/e2-func-exec-detail.png)

Sample source code.
```javascript
const asyncRedis = require("async-redis");
const {v4: uuidv4} = require('uuid');
const prefix = "claimId-";

module.exports = {
    main: async function (event, context) {
        try {
            const client = asyncRedis.createClient({
                host: process.env.REDIS_HOST,
                port: process.env.REDIS_PORT
            });

            let data = JSON.parse(event.data);
            let key = prefix + uuidv4() + "-" + data.claimId;
            let wrapData = {createTime: Date.now(), data: data, status: "new", updateTime: "", eventKey: key};

            await client.set(key, JSON.stringify(wrapData));
            console.log("key %s value %s saved", key, wrapData);
            return wrapData;
        } catch (err) {
            console.log(err);
            return "event save failure, please see function logs for more details";
        }
    }
};
```

Add dependencies for the function.
![](/exercises/ex2/images/e2-func-exec-dependencies.png)

Add dependencies.
```json
{
    "name": "itcm-func-exec",
    "version": "1.0.0",
    "dependencies": {
        "async-redis": "^1.1.7",
        "node-rest-client": "^3.1.0",
        "redis": "^3.0.2",
        "sync-request": "^6.1.0",
        "uuid": "^8.3.0"
    }
}
```

Add Redis Cluster Environment Variables.
![](/exercises/ex2/images/e2-func-exec-env.png)

Subscribe to the event by adding an event trigger.
![](/exercises/ex2/images/e2-func-exec-event-trigger.png)

Save operation will trigger serverless function deployment automatically each time.
Wait until the function status change to running, then the function is ready to serve.

## Step 2.2 - Create a fetch function, expose API for the external solution

function **itcm-func-fetch**</br>
Fetch event data from Redis Cluster and expose data by a REST API.

Write code in function source.
![](/exercises/ex2/images/e2-func-fetch-source.png)

Sample source code.
```javascript
const asyncRedis = require('async-redis');
const prefix = "claimId-";

module.exports = {
  main: async function (event, context) {
    console.log("start to fetch claim events");
    try {
      const client = asyncRedis.createClient({
        host: process.env.REDIS_HOST,
        port: process.env.REDIS_PORT
      });

      let keys = await client.keys(prefix + "*");
      if (keys.length < 1) {
        return [];
      }
      return await client.mget(keys);
    } catch (err) {
      console.log(err);
      return "event fetch failure, please see function logs for more details";
    }
  }
};
```

Add dependencies.
![](/exercises/ex2/images/e2-func-exec-dependencies.png)

```json
{
    "name": "itcm-func-fetch",
    "version": "1.0.0",
    "dependencies": {
        "async-redis": "^1.1.7",
        "node-rest-client": "^3.1.0",
        "redis": "^3.0.2",
        "sync-request": "^6.1.0",
        "uuid": "^8.3.0"
    }
}
``` 

Add Redis Cluster Environment Variables.
![](/exercises/ex2/images/e2-func-fetch-env.png)

Expose function by API Rule.
![](/exercises/ex2/images/e2-func-fetch-apirule.png)

## Step 2.3 - Create an upload function, process ITCM domain event

function **itcm-func-upload**</br>
The upload function provide REST API for mobile App to upload invoice pic, calling a third party OCR service, extract remark base 
on the pic, update claim with the remark, and the pic as an attachment.

Write code in function source.
![](/exercises/ex2/images/e2-func-upload-source.png)

```javascript
const asyncRedis = require("async-redis");
const request = require('sync-request');
const prefix = "claimId-";

module.exports = {
  main: async function (event, context) {
    console.log("start to upload claim invoice file");
    console.log("event data: %s", JSON.stringify(event.data));

    try {
      let data = event.data;
      let cEvent = JSON.parse(data.event);
      let img64 = data.base64;

      let remark = extractRemark(img64);
      updateClaim(cEvent.data.claimId, remark, img64);

      const client = asyncRedis.createClient({
        host: process.env.REDIS_HOST,
        port: process.env.REDIS_PORT
      });

      let valueStr = await client.get(cEvent.eventKey);
      let v = JSON.parse(valueStr);
      v.status = "processed";
      v.updateTime = Date.now();
      await client.set(cEvent.eventKey, JSON.stringify(v));

      console.log("upload cEvent %s done", valueStr);
    } catch (err) {
      console.log(err);
      return "upload failure, please see function logs for more details";
    }
  }
}

function extractRemark(base64) {
  console.log("start to extract remark by calling OCR Server");
  let result = "";
  let data = {
    "base64": base64,
    "trim": "\n"
  };

  try {
    let res = request("POST", process.env.OCR_URL, { json: data });
    result = JSON.parse(res.getBody('utf8'));
    console.log("ocr input: %s, ocr result: %s", base64, result);
  } catch (e) {
    console.log("ocr error: %s", e);
  }
  return result;
}

function updateClaim(claimId, remark, base64Str) {
  let payload = { claimsId: claimId, remark: remark, attachment: base64Str };
  console.log("request itcm payload: %s", payload);
  try {
    let res = request("POST", "https://extensions-gateway.dev2.eurekacloud.io/claim-submission/addAttachment", { json: payload });
    console.log("response itcm update %s", res.getBody());
  } catch (e) {
    console.error("update claim failure with exception %s", e);
    throw e;
  }
}
```

Add dependencies.
![](/exercises/ex2/images/e2-func-upload-depedencies.png)

```json
{
    "name": "itcm-func-upload",
    "version": "1.0.0",
    "dependencies": {
        "async-redis": "^1.1.7",
        "node-rest-client": "^3.1.0",
        "redis": "^3.0.2",
        "sync-request": "^6.1.0",
        "uuid": "^8.3.0"
    }
}
```

Add Redis Cluster & OCR Server Environment Variables.
![](/exercises/ex2/images/e2-func-upload-env.png)

Expose function by API Rule.
![](/exercises/ex2/images/e2-func-upload-apirule.png) 

## Summary
Now the extension services in Kyma runtime are ready,</br>
Go to the final exercise - [Interaction between ICTM and Kyma runtime](../ex3/README.md)
