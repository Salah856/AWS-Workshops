
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


- let’s take a check the SingletonRepo file. SingletonRepo can only have one instance in the program. And sigletonsrepo have one HashMap. let’s check the putKey() function, which is the core of this workshop. 

```java
public Concurrency putKey(int product_code ) {           
    Date date = Util.getRandomDate();
    if (map.containsKey(product_code)) {
        return map.get(product_code);
    }else{
        return map.put(product_code, new Concurrency(product_code,"test" , date));
    }   
}


```

- putKey works is simple. Check that HashMap has a number with containsKey() and if not, save the number with put(). 
- If the HashMap already has the same value, don’t put it.

- BasicSynchronization calls pukey() of SingletonRepo and inserts a randomly generated number between 0 ~ 2000.
- ConcurrencyCheckout is Main class. This class creates 5 BasicSynchronizations and starts 5 threads.

![Screenshot from 2021-07-16 08-40-35](https://user-images.githubusercontent.com/23625821/125903682-aacacecb-f5ab-45d3-9ba6-e25d760508e7.png)


### SO WHAT IS THE PROBLEM WITH THIS PROGRAM? 

- This code has a concurrency issue. if it call two PutKey() from two threads at the same time. What will happen?


- The number is entered only once, but the call count is increased twice.

- HashMap is not thread-safe. The code above is dangerous because get and put don’t guarantee atomicity.

- If the number of threads is increased and the number of put calls executed simultaneously increases, the result cannot be guaranteed.

- An error occurs because the same problem appears in the UnitTest being executed. SingletonRepotests, a unit test that is performed, creates 8 threads and raises the count one by one when an input occurs in the HashMap. And after all the work is done, the number of values entered in the HashMap is compared with the number of occurrences. If the values are the same, the number of inputs and the number of HashMaps are the same, so the function worked correctly.

- However, UnitTest will continue to fail because the current code was programmed without considering concurrency. Of course, if you are very lucky, the test may succeed. However, to prevent this, SingletonRepotests performs the same test 100 times.

So how do you solve this problem?

- You can change HashMap to ConcurrentHashMap. ConcurrentHashMap is designed to be thread-safe, so it operates stably in a multi-threaded environment and has slightly better performance than Hashtable and synchronized map. ConcurrentHashMap locks the map when you put it, so you can prevent the same key put at the same time.

- Open the SingletonRepo.java file in Cloud9, then change the HashMap below to ConcurrentHashMap.

```java
+   import java.util.concurrent.*;
    ...
-   private HashMap<Integer, Concurrency> map = new HashMap<>();
+   private ConcurrentHashMap<Integer, Concurrency> map = new ConcurrentHashMap<>();
```

- push the changes again.

```
git add .
git commit -m "fix singletonrepo.java"
git push
```
- And if you check the concurrencysample of Build, you can see that the build was successful. 

![codequality-solve](https://user-images.githubusercontent.com/23625821/125905251-b554def6-9a53-4f87-8206-4ae54d663fed.png)

- let’s also check the Report. If you select Concurrency-Unittest-Report in Report group of Build, you can see the result passed by 100%.

![codequality-100](https://user-images.githubusercontent.com/23625821/125905288-54a27b2c-6ff4-4b41-8657-1e7f381767ab.png)

- Let`s go to CodePipeline : https://console.aws.amazon.com/codepipeline

Select Pipeline in left menu and click concurrencysample-develop. this pipeline triggerd committing develop branch in concurrencysamle repository. you can find recently successed execution result.

![codepipeline-dev-success](https://user-images.githubusercontent.com/23625821/125905320-9312953c-93cd-4012-a750-89ca67b1ded7.png)




