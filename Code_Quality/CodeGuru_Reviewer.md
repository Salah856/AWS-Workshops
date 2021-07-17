
In previous parts, we have done setup for the environment and made integrations between CodeBuild and CodeGuru. 

Now ready for production code. The develop branch’s code has passed all unit tests and deploy, so we will deploy it to the production environment. developers usually don’t have permission to push directly to the master branch. So, through pull-request, we will go through a code review with a senior developer or a other developer and merge it in the master. 

Go to the CodeCommit console to create a pull-request. 

Go to CodeCommit: https://console.aws.amazon.com/codesuite/codecommit/repositories

Select Repositories in Source and click on concurrencysample.

![pc-codecommit-select](https://user-images.githubusercontent.com/23625821/126028806-1f5af3b0-7d91-409a-809e-96ae632bc720.png)

Select Pull requests from Repositories and click Create pull request in the upper right.

![pc-codecommit-prselect](https://user-images.githubusercontent.com/23625821/126028829-ae7b5dbf-1327-4b33-aef6-4f87ee490d43.png)

Create pull request, Destination set master and Source set develop and click the Compare button.

![pc-codecommit-createpr](https://user-images.githubusercontent.com/23625821/126028860-d70729fc-8d66-4e10-a509-f57952fef6d7.png)


You have created a pull-request. Now let`s see what happens.




