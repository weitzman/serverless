AWS gives you a ton of free resources whenever you create a new AWS account. This is called the free tier. It includes a massive allowance of free Lambda Requests, DynamoDB tables, S3 storage, and more. Before building Serverless apps, we strongly recommend starting with a fresh AWS account for maximum cost savings.

# Creating an Administrative IAM User
The Serverless Framework is one of the first application frameworks to manage both your code and infrastructure.  To manage your infrastructure on AWS, we're going to create an Admin user which can access and configure the services in your AWS account.  To get you up and running quickly, we're going to create a AWS IAM User with Administrative Access to your AWS account.

# Admin Access to Your AWS Account
In a production environment we recommend reducing the permissions to the IAM User which the Framework uses.  Unfortunately, the Framework's functionality is growing so fast, we can't yet offer you a finite set of permissions it needs.  In the interim, ensure that your AWS API Keys are kept in a safe, private location.

Now let's create an Admin IAM user:

* Create or login to your Amazon Web Services Account and go the the Identity & Access Management (IAM) Page.
* Click on **Users** and then Create New Users. Enter *serverless-admin* in the first field and click **Create**.
* View and copy the security credentials/API Keys in a safe place.
* In the User record in the AWS IAM Dashboard, look for **Managed Policies** on the **Permissions** tab and click **Attach Policy**. In the next screen, search for and select **AdministratorAccess** then click **Attach**.

When you go to create or install a Serverless Project, you will be prompted to enter your AWS Access Keys.  Once you enter them, they will be persisted to your Project's folder in the `admin.env` file.

#AWS Profiles
The Serverless Framework can also work with AWS Profiles already set on your computer.  In the Project Create or Project Install screens, it will detect your AWS Profiles and display them.  Select the one you want, and the AWS Access Keys for that profile will be persisted to your project.