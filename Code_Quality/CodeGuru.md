
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















### Reference: 

<a href="https://codequality.workshop.aws/en/"> Source </a>

