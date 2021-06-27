
# AWS SERVERLESS OBSERVABILITY WORKSHOP 


### PREREQUISITES

The following prerequisites are required for this workshops:

- A computer with an internet connection running Microsoft Windows, Mac OS X, or Linux.
- An internet browser such as Chrome, Firefox, Safari, Opera, or Edge.
- Familiarity with common Linux commands and the concepts of CI/CD.



### CREATE AN AWS ACCOUNT

If you don’t already have an AWS account with Administrator access: <a href="https://aws.amazon.com/getting-started/">  create one now by clicking here </a>

<a href="https://console.aws.amazon.com/iam/home?#/users$new" > Go to the IAM Management console </a>

On the left hand navigation, select Users, then click on the Add User button.

Enter the user details:


<img width="892" alt="iam-1-create-user" src="https://user-images.githubusercontent.com/23625821/123538246-43c22400-d734-11eb-94b3-664485a5aeeb.png">

Attach the AdministratorAccess IAM Policy, and click Next: Tags


<img width="907" alt="iam-2-attach-policy" src="https://user-images.githubusercontent.com/23625821/123538257-53416d00-d734-11eb-85ed-2f9f8c2c0a22.png">


We will skip adding tags for the workshop. Click Next: Review

Click to create the new user:

<img width="905" alt="iam-3-create-user" src="https://user-images.githubusercontent.com/23625821/123538266-589eb780-d734-11eb-96ca-ada8adcf13c3.png">

Take note of the login URL and save it for future use:

<img width="905" alt="iam-4-save-url" src="https://user-images.githubusercontent.com/23625821/123538273-5f2d2f00-d734-11eb-9b38-15b10b1db805.png">


Click on this URL to go to the AWS Management Console login page, use the username and password for the workshop user you just created.



#### CREATE A WORKSPACE

Launch Cloud9 in your closest region:

Accept the default values for Stack name and Parameters and click Create stack.


![cfn-stack-1](https://user-images.githubusercontent.com/23625821/123538436-36596980-d735-11eb-8a36-49a2aef181ff.png)


![cfn-stack-2](https://user-images.githubusercontent.com/23625821/123538445-41ac9500-d735-11eb-98ec-2d660c766352.png)


Wait until your Stack creating status shows as CREATE_COMPLETE


![cfn-stack-3](https://user-images.githubusercontent.com/23625821/123538455-4e30ed80-d735-11eb-833b-fe49f4988263.png)

Go to your Cloud9 Environment.

Find the environment named serverless-observability-workshop, click Open IDE.

When the Cloud9 console is shown, customize the environment by closing the welcome tab and the AWS Toolkit tab, lower work area, and opening a new terminal tab in the main work area:


<img width="1432" alt="c9before" src="https://user-images.githubusercontent.com/23625821/123538480-63a61780-d735-11eb-8265-36bdd23f3dc7.png">

Your workspace should now look like this:


<img width="1432" alt="c9after" src="https://user-images.githubusercontent.com/23625821/123538490-73bdf700-d735-11eb-8d02-5a215198f4ba.png">


### UPDATE YOUR WORKSPACE

##### Install dependencies

- Run the following commands in the Cloud9 terminal to update nvm (Node Version Manager) and install jq (a command-line JSON processor) and Locust (a load testing tool)

```bash

nvm install stable
sudo yum -y install jq 
sudo pip3 install locust

```

