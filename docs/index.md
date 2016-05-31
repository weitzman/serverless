In 2014, Amazon Web Services released a groundbreaking service called [AWS Lambda](https://aws.amazon.com/lambda/) that offers a new way to deploy your *web*, *mobile* or *IoT* application's code to the cloud.  Instead of deploying the entire codebase of your app all at once, with Lambda you deploy each of your application's functions individually, to their own containers.  Overall, Lambda is groundbreaking for three reasons:

* ##### **Pay-Per-Use Pricing**
AWS Lambda charges you only when your functions are run.  No more monthly-based billing for servers, no more wasted dollars spent on under-utilized servers.  There is no such thing as under-utilization with AWS Lambda. 

* ##### **Unprecedented Agility**
Lambda offers ready to go containers and orchestration out-of-the-box, leaving you free to decide how you would like to containerize your logic.  You can choose a monolithic, microservices, or nanoservices approach with Lambda.  Read more about that in our [Overview](http://docs.serverless.com/docs/introducing-serverless).

* ##### **No Servers**
Every Lambda function container auto-scales automatically when called concurrently.  Since your functions can scale massively out-of-the-box, you no longer have to think about scaling/managing servers, Amazon deals with that.  You focus only on building your product, wit.

However... while AWS Lambda offers a powerful new way of developing/running applications, when we began building our first project based entirely on AWS Lambda, we realized structure was badly needed.  Managing all of the containers that Lambda introduces is a difficult task.  Add to that multi-developer teams, multi-stage and multi-region support and you will quickly get into a messy situation.

Thus, the [Serverless Framework](https://github.com/serverless/serverless) was born.  The first and most powerful framework for building applications exclusively on AWS Lambda.