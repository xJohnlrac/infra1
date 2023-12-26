# Practice Exercise 1: Introduction to Processes and Process Attributes

## Tasks

1. Viewing Running Processes.
Open a terminal on your Linux system. Use the ```ps``` command to display a list of currently running processes.
Pay attention to the columns that show the process ID (PID), the name or command associated with each process, and the status.
Look for the process with the PID of 1 and take note of the process.(e.g. /sbin/launchd).

``` bash
[intern@intern-a1t-inf-lnx1 ~]$ ps aux
root                 1   0.1  0.1 408975104  15616   ??  Ss   20Jul23 267:59.47 /sbin/launchd
```
2. Identifying Parent and Child Processes
Identify a process from the list generated in Task 1 and note its PID.
Use the ```pgrep``` command to find child processes associated with the selected process.
Verify that the child processes have a different PID but the same parent PID as the selected process.
Can you share what command you ran?

``` bash
[intern@intern-a1t-inf-lnx1 ~]$ pgrep -P 1
309
311
313
314
315
.....
```
3. Viewing Detailed Process Information
Choose a process from the list generated in Task 2 and note its PID.
Use the ps command with the ```-p``` option followed by the PID (e.g., ```ps -p 12345```) to display detailed information about that specific process.
Observe the various attributes, including the process status, CPU and memory usage, and more. Take note that you will need to add another parameter and value to show the resource usage.

``` bash
[intern@intern-a1t-inf-lnx1 ~]$ ps -p 309 -o pid,stat,%cpu,%mem
  PID STAT  %CPU %MEM
  309 Ss     0.3  0.1
```

4. Monitoring Process Resource Usage
Use the ```top``` command to open the real-time system monitoring tool.
Observe the list of processes, their resource usage (CPU and memory), and the overall system statistics.
Pay attention to the dynamic updating of data and the interactive features of the top command.

  ``` bash
  [intern@intern-a1t-inf-lnx1 ~]$ top
Processes: 478 total, 7 running, 471 sleeping, 3524 threads            07:39:50
Load Avg: 2.20, 2.58, 2.45  CPU usage: 7.89% user, 5.50% sys, 86.59% idle
SharedLibs: 442M resident, 88M data, 27M linkedit.
MemRegions: 638649 total, 2976M resident, 92M private, 1371M shared.
PhysMem: 15G used (2288M wired, 7683M compressor), 40M unused.
VM: 227T vsize, 4184M framework vsize, 149166775(4) swapins, 153284764(0) swapou
Networks: packets: 105625798/89G in, 68209967/18G out.
Disks: 149860204/3802G read, 82907440/2972G written.

PID    COMMAND      %CPU TIME     #TH    #WQ  #PORT MEM    PURG   CMPRS  PGRP
381    WindowServer 43.5 78:26:44 24/1   6    8569  2064M  464K   1405M  381
0      kernel_task  15.8 91:10:31 575/10 0    0     2912K  0B     0B     0
54864  iTerm2       9.6  94:03.37 7      4    308   124M   0B     67M-   54864
399    coreaudiod   9.5  47:59:24 11     4    3641  116M   0B     94M-   399
9487   QEMULauncher 8.4  00:38.76 11     1    37    1727M  0B     1497M- 9487
```

Note that top is an interactive command\
Press q to exit

5. Sending Signals to Processes\
&bull; Identify a process from the list generated in Task 1 and note its PID.\
&bull; Use the ```kill``` command to send a termination signal (SIGTERM) to the selected process (e.g., ```kill -15 <PID>```).\
&bull; Confirm that the process has been terminated.\
&bull; Say run sleep 3600& and then kill it afterwards\

``` bash
[intern@intern-a1t-inf-lnx1 ~]$ sleep 3600 &
[1] 25783
[intern@intern-a1t-inf-lnx1 ~]$ kill -15 25783
[intern@intern-a1t-inf-lnx1 ~]$
[1]+  Terminated              sleep 3600
```
6. Background and Foreground Processes\
&bull; Launch a simple command in the foreground (e.g., ping www.google.com) that continuously runs in the terminal.\
&bull; Suspend the foreground process by pressing Ctrl + Z.\
&bull; Use the bg command to send the suspended process to the background.
&bull; Verify that the process is running in the background using the jobs command.

``` bash
[intern@intern-a1t-inf-lnx1 ~]$ ping www.google.com
PING www.google.com (142.251.220.164): 56 data bytes
64 bytes from 142.251.220.164: icmp_seq=0 ttl=119 time=25.553 ms
64 bytes from 142.251.220.164: icmp_seq=1 ttl=119 time=23.553 ms
^Z
[1]  + 10142 suspended  ping www.google.com
[intern@intern-a1t-inf-lnx1 ~]$ bg
[1]  + 10142 continued  ping www.google.com
64 bytes from 142.251.220.164: icmp_seq=2 ttl=119 time=22.471 ms
```
&bull; Note that after running bg your stdout will be bombarded by the pings output just continue running the next commands.

```bash
[intern@intern-a1t-inf-lnx1 ~]$ jobs
[1]  + running    ping www.google.com
[intern@intern-a1t-inf-lnx1 ~]$   kill %1
[1]  + 10142 terminated  ping www.google.com
```
7. Managing Process Priorities\
&bull; Use the ```nice``` command to launch a new process with a different priority level (e.g., ```nice -n 10 command```).\
&bull; Observe how the process priority affects its resource allocation.\
&bull; Experiment with different priority levels to see their impact.\

```bash
[intern@intern-a1t-inf-lnx1 ~]$ nice -n 10 echo Academy!
Academy!
```
## Conclusion
This practice exercise has provided you with practical experience in understanding and working with processes in a Linux environment. You've learned how to view running processes, identify parent and child processes, inspect process attributes, monitor resource usage, send signals to processes, manage background and foreground processes, and adjust process priorities. These skills are crucial for effective Linux system administration and troubleshooting.
