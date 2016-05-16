Now that you've configured AWS, you're ready to start using the Serverless framework. To install, simply run the following command:

```
npm install serverless -g
```

After it installs, you can create a new project:

```
serverless project create
```
The Serverless CLI will ask for a few pieces of information about your project (name, domain, email...etc). Serverless uses this information to build up your stack with [CloudFormation](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/Welcome.html). This process takes around 3 mins.
