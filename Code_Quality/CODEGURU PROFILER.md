
In this final part, we will create CodeGuru Profiler groups. This is where you can see the data of Profiling.

Go to the CodeGuru console: https://console.aws.amazon.com/codeguru

Select Profiling groups from the Profiler on the left menu. Then select concurrencysample-profiler.

<img width="1361" alt="1" src="https://user-images.githubusercontent.com/23625821/126029675-b9c7ac2a-ceb9-4acc-ac85-d0368ab55e9f.png">

You can see the analysis by CodeGuru Profiler. You can estimate the amount of time, percent, and cost per function. In addition, the results of profiling can be analyzed to provide reports that require improvement.

<img width="1354" alt="2" src="https://user-images.githubusercontent.com/23625821/126029707-c9971344-620e-44c2-8613-f8f77db89022.png">


## Overview Visualization

An overview visualization can help you find specific call stacks that lead to inefficient code. You can find code that is running on the CPU by looking for flat tops in the visualization. It is an area where the CPU is doing work directly in that function and not a callee.


<img width="1352" alt="3" src="https://user-images.githubusercontent.com/23625821/126029822-12e9eac2-a3f1-48b9-97dd-e5265da72cec.png">


## Hotspot Visualization

A hotspots visualization can be used to investigate functions that are by themselves computationally expensive. It shows a top-down view of your profile. The functions consuming the most application time are at the top of the visualization. At the bottom of the visualization are the entry point functions.

<img width="1083" alt="4" src="https://user-images.githubusercontent.com/23625821/126029826-85cb39f2-c1f4-4948-8590-56269daaf812.png">


## Recommendations Report

Amazon CodeGuru Profiler makes recommendations you can use to optimize your applications. Each recommendation includes information about why the recommendation was made, a description, suggested resolution steps, and the stack locations that were the source of the recommendation.

<img width="1240" alt="5" src="https://user-images.githubusercontent.com/23625821/126029966-6bf75a65-e4e8-4d38-b887-d8303f5fffda.png">


Reusing the AWS Client seems to be able to more optimize the program. You can optimize the software using this variety of information.

Now that the training is finish! Congrats and thank you for bearing with me. <3 :D 


### Reference 

<a href="https://codequality.workshop.aws"> For more details </a> 



