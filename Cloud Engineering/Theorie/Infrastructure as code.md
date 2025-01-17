### Blue - Green deployment
There are 2 identical environments 
One with the old code the other with the newer version of the code.

- Blue = the old stable service
- Green = the new version of the service

Swap from Blue to green, once the migration is completed the original Blue environment can deleted or it  can become the green infra for the next future release.

- In a blue - green strategy the traffic is gradually changed from one to the other environment. If things go wrong not all users are affected immediately.
- In a red - black strategy the traffic is moved from one environment to the other one,  all at once. -> a BIG BANG

#### Canary testing
Transition to the new environment on a user-be-user basis.