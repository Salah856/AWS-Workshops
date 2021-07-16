
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


