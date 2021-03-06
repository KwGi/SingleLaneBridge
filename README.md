# Single Lane Bridge
Demonstrates the use of multithreading and monitors to guide multiple cars of right and left side cross a single lane bridge.The skeleton code was taken from [Imperial College London](https://www.doc.ic.ac.uk/~jnm/book/book_applets/SingleLaneBridge.html).Every car is a thread. Red cars arrive on the left side of the bridge,the blue on the right. The frequency of arrival of cars, as well as the total number of cars cars arriving on each side are parameters of the simulation.The bridge is the shared memory area that we need to manage. The time which is required to pass a car, and how many cars on the same side they can pass each time are also parameters of the simulation.All cars enter the bridge hierarchically depending the time that they had came.

*Disclaimer: Times may differ but outcomes will be similar.  

## Methods
1. Unsafe Bridge(Bridge)
2. Safe Bridge
3. Fair Bridge
4. Adjusted Fair Bridge

## Usage & Examples
*After compiling in class files.   

```
java SingleLaneBridge [max Red cars] [maxBluecars] [Method] [arrival frequency milliseconds] [transit time in milliseconds] [#same cars in Bridge]
```

#### Unsafe Bridge
Write in cmd or powershell :  

```
java SingleLaneBridge 2 3 Bridge 30 100 1
```

##### Outcome:

```
Left Side                                                  Bridge                    Right Side
Red Car 0 Arrived at 2019-03-15T16:29:23.851Z
Red Car 0 Passing at 2019-03-15T16:29:23.913Z
                                                                                     Blue Car 0 Arrived at 2019-03-15T16:29:23.913Z
                                                                                     Blue Car 0 Passing at 2019-03-15T16:29:23.913Z
Crash
Red Car 1 Arrived at 2019-03-15T16:29:23.944Z
                                                                                     Blue Car 1 Arrived at 2019-03-15T16:29:23.944Z
Red Car 1 Passing at 2019-03-15T16:29:23.944Z
Crash
                                                                                     Blue Car 1 Passing at 2019-03-15T16:29:23.944Z
Crash
                                                                                     Blue Car 2 Arrived at 2019-03-15T16:29:23.976Z
                                                                                     Blue Car 2 Passing at 2019-03-15T16:29:23.976Z
Crash
Blue Car 0 Passed at 2019-03-15T16:29:24.023Z
                                                                                     Red Car 0 Passed at 2019-03-15T16:29:24.023Z
Blue Car 1 Passed at 2019-03-15T16:29:24.054Z
                                                                                     Red Car 1 Passed at 2019-03-15T16:29:24.054Z
Blue Car 2 Passed at 2019-03-15T16:29:24.086Z
```

##### Conclusion:
For the shake of the example when a crash happens the execution doesn't stop.As you can see the first crash is between red car 0 ,which crosses the bridge, and blue car 0 which enters the bridge.Furthermore we have 3 other crashes when 1)red car 1 tried to enter the bridge but red car 0 and blue car 0 were crossing it , 2) blue car 1 tried to enter the bridge but red car 0 ,1 and blue car 0 were crossing it and finally 3) blue car 2 tried to enter the bridge but red car 0 ,1 and blue car 0,1 were crossing it.The outcome is what that i was expected.


#### Safe Bridge
Write in cmd or powershell :  

```
java SingleLaneBridge 2 3 SafeBridge 30 100 1
```

##### Outcome:

```
Left Side                                                  Bridge                    Right Side
Red Car 0 Arrived at 2019-03-15T17:00:58.959Z
Red Car 0 Passing at 2019-03-15T17:00:59.021Z
                                                                                     Blue Car 0 Arrived at 2019-03-15T17:00:59.021Z
Red Car 1 Arrived at 2019-03-15T17:00:59.068Z
                                                                                     Blue Car 1 Arrived at 2019-03-15T17:00:59.068Z
                                                                                     Blue Car 2 Arrived at 2019-03-15T17:00:59.100Z
                                                                                     Red Car 0 Passed at 2019-03-15T17:00:59.131Z
Red Car 1 Passing at 2019-03-15T17:00:59.131Z
                                                                                     Red Car 1 Passed at 2019-03-15T17:00:59.240Z
                                                                                     Blue Car 0 Passing at 2019-03-15T17:00:59.240Z
Blue Car 0 Passed at 2019-03-15T17:00:59.350Z
                                                                                     Blue Car 1 Passing at 2019-03-15T17:00:59.350Z
Blue Car 1 Passed at 2019-03-15T17:00:59.459Z
                                                                                     Blue Car 2 Passing at 2019-03-15T17:00:59.459Z
Blue Car 2 Passed at 2019-03-15T17:00:59.569Z
```

##### Conclusion:
As you can see from times  we don't have crashes but we don't have justice too.For instance when red car 0 passed we have two blue cars waiting on right side and one red car waiting on left side,the next logical move is that it's blue cars's turn ,however red car 1 has taken first the lock on bridge and therefore it will cross the bridge .This example marks the unfairness.



#### Fair Bridge
Write in cmd or powershell :  

```
java SingleLaneBridge 2 3 FairBridge 30 100 1
```
##### Outcome:

```
Left Side                                                  Bridge                    Right Side
Red Car 0 Arrived at 2019-03-15T17:37:09.509Z
Red Car 0 Passing at 2019-03-15T17:37:09.587Z
                                                                                     Blue Car 0 Arrived at 2019-03-15T17:37:09.603Z
Red Car 1 Arrived at 2019-03-15T17:37:09.634Z
                                                                                     Blue Car 1 Arrived at 2019-03-15T17:37:09.634Z
                                                                                     Blue Car 2 Arrived at 2019-03-15T17:37:09.666Z
                                                                                     Red Car 0 Passed at 2019-03-15T17:37:09.713Z
                                                                                     Blue Car 0 Passing at 2019-03-15T17:37:09.713Z
Blue Car 0 Passed at 2019-03-15T17:37:09.822Z
Red Car 1 Passing at 2019-03-15T17:37:09.822Z
                                                                                     Red Car 1 Passed at 2019-03-15T17:37:09.931Z
                                                                                     Blue Car 1 Passing at 2019-03-15T17:37:09.931Z
Blue Car 1 Passed at 2019-03-15T17:37:10.041Z
                                                                                     Blue Car 2 Passing at 2019-03-15T17:37:10.041Z
Blue Car 2 Passed at 2019-03-15T17:37:10.150Z
```

##### Conclusion:
As you can see this time when red car 0 crosses the bridge the next car which crosses  is blue car 0 and after its exit ,the next car  crossing the bridge is red  and it is go on  like this till no car left. So there is fairness but when large amounts of same cars are arriving in one side the crowding is increasing in this side  and that's the reason why should make some adjustments to control the crowding . 


#### Adjusted Fair Bridge 
Write in cmd or powershell : 

```
java SingleLaneBridge 5 10 AdjustedFairBridge 30 100 1
```

##### Outcome:

```
Left Side                                                  Bridge                    Right Side
Red Car 0 Arrived at 2019-03-15T17:58:52.939Z
Red Car 0 Passing at 2019-03-15T17:58:53.002Z
                                                                                     Blue Car 0 Arrived at 2019-03-15T17:58:53.002Z
Red Car 1 Arrived at 2019-03-15T17:58:53.033Z
                                                                                     Blue Car 1 Arrived at 2019-03-15T17:58:53.033Z
Red Car 2 Arrived at 2019-03-15T17:58:53.065Z
                                                                                     Blue Car 2 Arrived at 2019-03-15T17:58:53.065Z
Red Car 3 Arrived at 2019-03-15T17:58:53.096Z
                                                                                     Blue Car 3 Arrived at 2019-03-15T17:58:53.096Z
                                                                                     Red Car 0 Passed at 2019-03-15T17:58:53.112Z
                                                                                     Blue Car 0 Passing at 2019-03-15T17:58:53.112Z
Red Car 4 Arrived at 2019-03-15T17:58:53.127Z
                                                                                     Blue Car 4 Arrived at 2019-03-15T17:58:53.127Z
                                                                                     Blue Car 5 Arrived at 2019-03-15T17:58:53.158Z
                                                                                     Blue Car 6 Arrived at 2019-03-15T17:58:53.190Z
                                                                                     Blue Car 7 Arrived at 2019-03-15T17:58:53.221Z
Blue Car 0 Passed at 2019-03-15T17:58:53.221Z
                                                                                     Blue Car 1 Passing at 2019-03-15T17:58:53.221Z
                                                                                     Blue Car 8 Arrived at 2019-03-15T17:58:53.252Z
                                                                                     Blue Car 9 Arrived at 2019-03-15T17:58:53.283Z
Blue Car 1 Passed at 2019-03-15T17:58:53.330Z
                                                                                     Blue Car 2 Passing at 2019-03-15T17:58:53.330Z
Blue Car 2 Passed at 2019-03-15T17:58:53.440Z
                                                                                     Blue Car 3 Passing at 2019-03-15T17:58:53.440Z
Blue Car 3 Passed at 2019-03-15T17:58:53.549Z
                                                                                     Blue Car 4 Passing at 2019-03-15T17:58:53.549Z
Blue Car 4 Passed at 2019-03-15T17:58:53.659Z
                                                                                     Blue Car 5 Passing at 2019-03-15T17:58:53.659Z
Blue Car 5 Passed at 2019-03-15T17:58:53.768Z
Red Car 1 Passing at 2019-03-15T17:58:53.768Z
                                                                                     Red Car 1 Passed at 2019-03-15T17:58:53.877Z
                                                                                     Blue Car 6 Passing at 2019-03-15T17:58:53.877Z
Blue Car 6 Passed at 2019-03-15T17:58:53.987Z
Red Car 2 Passing at 2019-03-15T17:58:53.987Z
                                                                                     Red Car 2 Passed at 2019-03-15T17:58:54.096Z
                                                                                     Blue Car 7 Passing at 2019-03-15T17:58:54.096Z
Blue Car 7 Passed at 2019-03-15T17:58:54.205Z
Red Car 3 Passing at 2019-03-15T17:58:54.205Z
                                                                                     Red Car 3 Passed at 2019-03-15T17:58:54.314Z
                                                                                     Blue Car 8 Passing at 2019-03-15T17:58:54.314Z
Blue Car 8 Passed at 2019-03-15T17:58:54.424Z
Red Car 4 Passing at 2019-03-15T17:58:54.424Z
                                                                                     Red Car 4 Passed at 2019-03-15T17:58:54.534Z
                                                                                     Blue Car 9 Passing at 2019-03-15T17:58:54.534Z
Blue Car 9 Passed at 2019-03-15T17:58:54.643Z
```

##### Conclusion:
As you can see from times we don't have any crashes , we have fairness but when cars are crowding on one side the fairness can be adjusted.For instance when blue car 0 passed the bridge we had 7 blue cars on right side and only 4 red cars on left side and it was red cars's turn but monitor adjusted to avoid overcrowding on right side , so it was blue cars's turn again .This continued until blue car 5 passed the bridge in that moment we had 4 blue cars and 4 red cars waiting so monitor became completely  fair and gave the turn to red cars from that moment till the end it is the same with fair bridge . 



### For more information regarding this project please check my comments inside the code .

