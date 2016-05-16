A basic Serverless project contains the following directory structure:
```
s-project.json
s-resources-cf.json
admin.env
_meta
    |__resources
         |__s-resources-cf-dev-useast1.json
    |__variables
         |__s-variables-common.json
         |__s-variables-dev.json
         |__s-variables-dev-useast1.json
functions
    |__function1
         |__event.json
         |__handler.js
         |__s-function.json
```
Here's the same directory structure with some explanation:
```
s-project.json                // project and author data
s-resources-cf.json       // CloudFormation template for all stages/regions
admin.env                     // AWS Profiles - gitignored)
_meta                          // meta data that holds stage/regions config and variables - gitignored
    |__resources             // final CF templates for each stage/region
         |__s-resources-cf-dev-useast1.json
    |__variables              // variables specific to stages and regions
         |__s-variables-common.json
         |__s-variables-dev.json
         |__s-variables-dev-useast1.json
functions                      // folder to group your project functions
    |__function1            // your first function
         |__event.json      // sample event for testing function locally
         |__handler.js      // your function handler file
         |__s-function.json   // data for your lambda function, endpoints and event sources
```
Now let's dive deeper into the most critical pieces of a Serverless project:

# Project
Each Serverless Project contains an `s-project.json` file that looks like this:
```
{
  "name": "projectName",
  "custom": {}, // For plugin authors to add any properties that they need
  "plugins": [] // List of plugins used by this project
}
```
# Meta Data
Each Serverless project contains a `_meta` folder in its root directory. This folder holds user specific project data, like stages, regions, CloudFormation template files and variables (more on variables later). Since this folder contains sensitive information, it's gitignored by default, allowing you to share your Serverless projects with others, where they can add their own meta data.

# Functions
Functions are the core of a Serverless project. These are the functions that get deployed to AWS Lambda. You can organize your project functions however you like. We recommend you group all of your project functions in a `functions` folder in the root of your project. You can make it even more organized with more nesting and subfolders inside that `functions` folder. For simple projects, you can put your functions directly in the root of your project. It's completely flexible.

Each function can have several endpoints, and each endpoint can have several methods (ie. GET, POST...etc). These are the endpoints that get deployed to AWS API Gateway and they all point to the Function that they're defined within. Functions can also have several event sources (i.e. DynamoDB, S3..etc). You can configure your Lambda Function, its Endpoints and Events in the `s-function.json` file:

```
{
  "name": "functionName",
  "customName": false,  // Custom name for your deployed Lambda function
  "customRole": false,  // Custom IAM Role for your deployed Lambda function
  "handler": "function1/handler.handler", // path of the handler relative to the function root
  "runtime": "nodejs",
  "description": "some description for your lambda",
  "timeout": 6,
  "memorySize": 1024,
  "custom": {
    "excludePatterns": [] // an array of whatever you don't want to deploy with the function
  },
  "environment": { // env vars needed by your function. Makes use of Serverless variables
    "SOME_ENV_VAR": "${envVarValue}"
  },
  "events": [ // event sources for this lambda
    {
      "name" : "myEventSource", // unique name for this event source
      "type": "schedule", // type of event source
      "config": {
         "schedule": "rate(5 minutes)",
          "enabled": true
     }
    }
],
  "endpoints": [ // an array of endpoints that will invoke this lambda function
    {
      "path": "function1",
      "method": "GET",
      "authorizationType": "none",
      "apiKeyRequired": false,
      "requestParameters": {},
      "requestTemplates": {
        "application/json": ""
      },
      "responses": {
        "400": {
          "selectionPattern": "^\\[BadRequest\\].*", // selectionPattern is mapped to the Lambda Error Regex
          "statusCode": "400" // HTTP Status that is returned as part of the regex matching
        },
        "403": {
          "selectionPattern": "^\\[Forbidden\\].*",
          "statusCode": "403"
        },
        "404": {
          "selectionPattern": "^\\[NotFound\\].*",
          "statusCode": "404"
        },
        "default": {
          "statusCode": "200",
          "responseParameters": {},
          "responseModels": {},
          "responseTemplates": {
            "application/json": ""
          }
        }
      }
    }
  ],
  "vpc": {
    "securityGroupIds": [],
    "subnetIds": []
  }
}
```

For more information about the `s-function.json` file, check out the [Function Configuration section](/docs/function-configuration).