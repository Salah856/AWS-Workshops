
# AWS CI/CD pipeline with CodeGuru & UnitTest to improve code quality 

This post explains how to build a CI/CD pipeline using AWS services. It also explains how to organize various ways to improve code quality (CodeReview & UnitTest) in the AWS pipeline.

It covers simple branch build and deployment, UnitTest report, and CodeGuru which automatically performs code review when create pull-requests.

![1](https://user-images.githubusercontent.com/23625821/125891953-96b13bd1-19ab-4b20-8093-e0bf42196dc1.png)

## AWS Code Series (AWS CI/CD services)

You can use the AWS Code Series. Code series is a fully managed service, so there is no need for a infrastructure.

- CodeCommit: AWS CodeCommit is a fully-managed source control service that hosts secure Git-based repositories.
- CodeBuild: AWS CodeBuild is a fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy.

- CodeDeploy: AWS CodeDeploy is a fully managed deployment service that automates software deployments to a variety of compute services such as Amazon EC2, AWS Fargate, AWS Lambda, and your on-premises servers.
- CodePipeline: AWS CodePipeline is a fully managed continuous delivery service that helps you automate your release pipelines for fast and reliable application and infrastructure updates.


## AWS CodeGuru 

Amazon CodeGuru is a machine learning service for automated code reviews and application performance recommendations.

It helps you find the most expensive lines of code that hurt application performance and keep you up all night troubleshooting, then gives you specific recommendations to fix or improve your code. It supports JAVA, repository can use GitHub or CodeCommit. It is also easy to integrate. 


<img width="757" alt="codequeility" src="https://user-images.githubusercontent.com/23625821/125892654-b146bb4f-ea60-4c5a-96f6-ce6c36eb4b5e.png">

### CodeGuru Reviewer that provides Automated CodeReview

Amazon CodeGuru Reviewer finds issues in your code and recommends how to remediate them.

<img width="546" alt="git-pr-codereviewer" src="https://user-images.githubusercontent.com/23625821/125892722-da641d48-e54a-4f4e-8303-8b09d99167bf.png">

The contents that CodeGuru Reviewer detects can be this categories.

- AWS Best Practices : AWS APIs contain a rich set of features to ensure performance and stability of software.
- Concurrency : CodeGuru Reviewer identifies problems with implementations of concurrency in multithreaded code

- Resource Leaks : CodeGuru Reviewer looks for lines of code where resource leaks might be occurring.
- Sensitive Information Leak : Sensitive information in code should not be shared with unauthorized parties.

### CodeGuru Profiler 

Amazon CodeGuru Profiler is always searching for application performance optimizations, identifying your most expensive lines of code and recommending ways to fix them to reduce CPU utilization, cut compute costs, and improve application performance.


For setup steps, you can find it  <a href="https://codequality.workshop.aws/en/setup.html"> here </a> and  <a href="https://codequality.workshop.aws/en/setup/lab-setup.html"> here </a> 


###  CodeCommit Setup and source code download

1. let’s set up the code in Cloud9. Enter the following command in the terminal of Cloud9. 

```sh
~ git clone https://github.com/aws-samples/amazon-cicd-concurrency-sample-application.git
```

2. If the command is executed successfully, created a folder name amazon-cicd-concurrency-sample-application in the file cloud9 file tree. 

<img width="1402" alt="codecommit-master2" src="https://user-images.githubusercontent.com/23625821/125893870-3a1851ec-ce50-40d3-9424-e318f2d0d292.png">

3. clone gets the master branch. If you look at the contents of the folder, there are no other files except the README.md file. the real source code in develop, pull the develop branch.

```
~ cd amazon-cicd-concurrency-sample-application
~ git checkout origin/develop -b develop
```

<img width="1397" alt="codecommit-develop2" src="https://user-images.githubusercontent.com/23625821/125894076-005ceaa3-7d63-413a-866d-7e914d610e38.png">


4. To check the output of CloudFormation, go to the CloudFormation console.

go to the CloudFormation console : https://console.aws.amazon.com/cloudformation

5. Select Stacks from the left menu and select CodeQuality-Workshop you created. You can check the detailed information of the stack created here.

![codecommit-cloudformation-select-stack](https://user-images.githubusercontent.com/23625821/125894252-d1be4ba8-ab38-4b2f-a17d-62bdf0add95f.png)


6. Select Outputs at the top of the stack details. There you copy the URL of CodeCommit that lab `a repository. 

![codecommit-cloudformation-stacks-output](https://user-images.githubusercontent.com/23625821/125894261-aca5c364-6dad-4a30-acf2-c70d3d8f5ba7.png)

7. Change the url of origin to the address of the newly created codecommit at https://github.com/aws-samples/amazon-cicd-concurrency-sample-application.git.

Entering the following in the terminal of Cloud9. <YOUR_REPOSITORY-URL> is the changeCodeCommit copied from the Stack of CloudFormation.

```
~ git remote set-url origin <YOUR-REPOSITORY-URL>
```

After finished the command, check again with git remote show origin, and you can see that the URL of origin has been changed to your CodeCommit address. 

After that, you can checkout to master branch first then push commits. Then, develop branch and push commits. 

```
~ git checkout master 
~ git push 

~ git checkout develop
~ git push 
```


### CodeGuru Reviewer setup

- Go to the CodeGuru console : https://console.aws.amazon.com/codeguru. 
- Select Associated repositories from Reviewer on the left menu. 

![codeguru-reviewer-select](https://user-images.githubusercontent.com/23625821/125894830-c5ce561b-a694-4dcd-af38-09ce70c3fbfb.png)

- Select Associate repository at the top right.

![codeguru-associate-repository](https://user-images.githubusercontent.com/23625821/125894873-6cfa7a23-5fd4-4170-aba4-b1efda61cfc3.png)

- Select AWS CodeCommit as the Source provider for Repository details, then select concurrencysample at Repository location. and click Associate.

![codeguru-associate2](https://user-images.githubusercontent.com/23625821/125894982-07d4b1fa-8080-43e8-9177-2e6605bf679e.png)

- Check the connected concurrencysample in Codeguru’s Dashboard. 

![codeguru-fin](https://user-images.githubusercontent.com/23625821/125894987-c610df69-0610-40d9-b0db-9b77e4351928.png)

- Now CodeGuru and Codecommit are linked. 


### CodeGuru profiler setup 

- Go to the CodeGuru console: https://console.aws.amazon.com/codeguru
- Select Profiling groups from Profiler on the left menu.

<img width="939" alt="codeguru-profiler-select" src="https://user-images.githubusercontent.com/23625821/125895194-baefb27b-c896-4e90-8230-45cb01652f99.png">

- Select Create profiling groups at the top right. 

<img width="1389" alt="codeguru-profiler-group" src="https://user-images.githubusercontent.com/23625821/125895240-87393775-54d8-4bed-8131-9441c308dac1.png">
- Enter concurrencysample-profiler in Name of Profiling group details in Create profiling group. click Create at the bottom right. 

<img width="1091" alt="codeguru-profiler-create" src="https://user-images.githubusercontent.com/23625821/125895291-d9d6ec27-212f-43e1-ba66-832cec0db831.png">

- Enter WebAppRole in choose users and roles in the Manage permissions for concurrencysample-profiler box. Select the checkbox on the left and click Save to save. 

<img width="636" alt="1" src="https://user-images.githubusercontent.com/23625821/125895451-fd1360dc-ddbf-40a7-a08a-fa0ddcd0f4de.png">

- Profiler can be found in the main of the source code, ConcurrencyCheckout.java.

```java
public static void main(final String[] args) {
    // Start the profiler
    Profiler.builder().profilingGroupName("concurrencysample-profiler").withHeapSummary(true).build().start();
    
} 

```

- Now CodeGuru profiler and instance is complete. 
 

### CodeBuild report 

- Go to the Codebuild console : https://console.aws.amazon.com/codebuild
- Select Report groups in the right Build tab. Select Create report group at the top right.

![codebuild-report-4](https://user-images.githubusercontent.com/23625821/125895994-5f8311df-632d-4f14-91b8-5a7822ada0cc.png)
- Enter Concurrency-Unittest-Report in Report group name of Rport group configuration. Select Test for the report type. Uncheck the box for Export to Amazon S3.

![codebuild-report-5](https://user-images.githubusercontent.com/23625821/125896035-783d3042-945b-45cd-be19-7550a6f65e18.png)

- To copy the ARN of the report groups, Concurrency-Unittest-Report from Report groups. The results of the Unittest here will now be shown. Copy the contents of Report group ARN of Configuration.

![codebuild-report-copy-arn](https://user-images.githubusercontent.com/23625821/125896099-f54e393e-c11e-4257-844c-4bd59983cb9e.png)


- Now let’s go back to Cloud9 and edit buildspec.yml. buildspec.yml is located in ConcurrencySample’s root directory. 

- Double-click the file to add content. Paste the Report group ARN to <YOUR-REPORT-GROUP-ARN>.

```yaml
reports:
  <YOUR-REPORT-GROUP-ARN>:
    files:
      - '**/*'
    base-directory: 'build/test-results/test'    
    
```





### Reference: 

<a href="https://codequality.workshop.aws/en/"> Source </a>

