
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



### Reference: 

<a href="https://codequality.workshop.aws/en/"> Source </a>

