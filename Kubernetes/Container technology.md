# Cgroups - Control groups
- current version is cgroupsv2

purpose:
- A pool of memory and cpu resources is linked to a cgroup.
- Processes are linked to a cgroup
- this makes it possible to limit the amount of cpu and memory to specific processes

It is like applications are given a bubble of resources 
## Is a kernel feature
It manages and controls RESOURCES
-> resources: processes and tasks
-> subsystems: cpu time, memory,...


# cgroup hierarchy

cgroup has a single hierarchy like the process hierarchy there is one single root
>all cgroups live in the directory:
>/sys/fs/cgroup 

- memory ->
- disk i/o -> data storage groups
- cpu -> data process groups

Example of a cgroup:    /sys/fs/cgroup/kubepods/cg1
you just put the process ID (PID) inside the file

> The init process is the first process that is the root process that will trigger all the other processes. this is a daemon process, which means that is running always in the background

> The init process in most cases is systemd !!


# RUNC

runc is a tool that makes it possible to run containers. 
- It makes use of the cgroups and namespaces to isolate the container process


# ContainerD

> A tool that has been developed by docker inc.

- It can ship containers, pull, push, export, .......
- It is a container handler
- It is via runc that containerD can run containers.

containerD is a layer on top of RUNC


## ctr tool
with the ctr cli tool you can directly steer the containerd tools

$ ctr image export