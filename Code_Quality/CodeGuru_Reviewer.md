
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


## CODEGURU AWSSDK

let’s check what kind of code review has doing in pull-request.(almost wait 5min.)

Go to CodeCommit’s console: https://console.aws.amazon.com/codesuite/codecommit/repositories

If CodeCommit and Repository are connected, the following screen will appear. Select Activity at the top.

![pr-solve-comment](https://user-images.githubusercontent.com/23625821/126028954-b9c01252-bb4b-4a71-8ae6-21ba0fac61ef.png)

The code review comment was attached to the code that I thought had no problems.

![codeguru-ac](https://user-images.githubusercontent.com/23625821/126028984-b1ef5ab3-645d-4c09-9fbc-8559d1e5d7ff.png)

Temporary Security Credentials rather than long-term Security Credentials such as AccessKey and SceretKey. CodeGuru tells you how and how to use the AWS SDK secure. These are things that cannot be found in simple unit tests or experience!

Let’s change SingletonRepo.java code. Delete the AWS SDK credential code. And you just need to give EC2 the IAM Role to access the necessary resources. let’s delete the AWS SDK credentials related code of SingleRepo.java.

![1](https://user-images.githubusercontent.com/23625821/126029060-baebfca0-5f10-4f0e-8ccd-e5871ba37545.png)

And… We have other problem. CodeGuru recommend that you use the Regions enum. not using string. Regions is an enumeration of all publicly available regions. To create a client with a region from the enum, use the following code.

![codeguru-region](https://user-images.githubusercontent.com/23625821/126029080-9cf5bf0c-bd85-477d-8337-f9e78344702c.png)

![2](https://user-images.githubusercontent.com/23625821/126029096-53777cde-6e61-410e-80ab-bc3b07e1481a.png)

You can evaluate whether CodeGuru’s suggestions are really useful through feedback. These can contribute to better CodeGuru comments.


## CODEGURU CONCURRENCY

![pr-solve-comment-show](https://user-images.githubusercontent.com/23625821/126029438-b8f2862a-1f23-4283-aa8d-6508abb234f7.png)


I thought concurrentHashMap was a thread-safe data structure, but there was one problem. ConcurrentHashMap does not lock the entire map when performing put command for performance. Of course, you can declare a function to be synchronized , but in this case, it is the same as a single-thread, which can cause performance problems.


Edit the code and push.

```
~ git add .
~ git commit -m "fix put(), containsKey()-> putifAbsent()"
~ git push
```

The problem has been fixed, we will end the Pull-Request. Click the Merg button in the top right corner of the AWS console.

![merge](https://user-images.githubusercontent.com/23625821/126029446-e25831ef-90d5-4742-b45c-57d5da11f246.png)

Since master has not changed, we choose Fast forward merge. Source is develop branch, uncheck the box of Delete source branch develop after merging?.

![merge2](https://user-images.githubusercontent.com/23625821/126029455-b4422d7e-d199-470e-b521-573ce05808f2.png)


Using the CD/CI pipeline, modifications of the code can be safely reflected as the master. Also, developers can easily see the test results and process of the code by simply using Commit and push.

UnitTest and CodeReview are one of the best ways to improve code quality. For each process, you can use the CodeBuild Report and CodeGuru Reviwer to make code review and UnitTest safer and more effective.

In the next final part, we will check the profiling results that are actually deployed and running. 











