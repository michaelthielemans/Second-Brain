### Blue - Green deployment
There are 2 identical environments 
One with the old code the other with the newer version of the code.

Blue = the old
Green = the new
Swap from Blue to green, once the migration is completed the original Blue environment can then be used for the next future release.

In a blue - green strategy the traffic is gradually changed from one to the other environmnet
In a red - black strategy the traffic is moved from one environment to the other all at once.

#### Canary testing
Transition to the new environment on a user-be-user basis