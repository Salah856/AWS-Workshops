
In <a href="https://dev.to/awsmenacommunity/aws-ci-cd-pipeline-with-codeguru-unittest-part-i-i4o"> previous part </a> , we knew how to setup our environment for CI/CD using AWS series, and CodeGuru. 

Now, Let's check the code. 

- This is the structure of the source code.

```
-src
    -main/java/com/example/concurrencysample
        -BasicCHeckMap.java
        -BasicSynchronization.java
        -Concurrency.java
        -ConcurrencyCheckout.java
        -SingletonRepo.java
        -Util.java
    -test/java/com/example/concurrencysample
        -SingletonRepoTests.java


```

