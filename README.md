# CPU
CPU Scheduling Algorithms  
By: Safwan Alselwi
Demo at: https://www.youtube.com/watch?v=jAyHkWFTrXM
Support me by subscribing to my youtube channel 

===================================================

First-Come-First-Served or FIFO Scheduling
The process that requests the CPU first is allocated the CPU first. The average waiting time for FCFS policy is often quite long.

Example:
Consider the following set of processes that arrive at time 0.
            Process			  CPU Burst Time (ms)
    	P1				24
	P2				3
	P3				3
Suppose that processes arrive in the order: P1, P2, P3, we get the result as :
Process:		P1 	                p2           p3
Time Line:	0		24	27	30


Waiting time for P1 = 0; P2 = 24; P3 = 27
Ave. waiting time: (0 + 24 + 27) /3 = 17 ms.


==============================================

Shortest-Job-First Scheduling
Associate with each process the length of its next CPU burst. Use these lengths to schedule the process with the shortest time. 
Two schemes:
* Non-preemptive - once CPU is given to the process, it cannot be preempted until it completes its CPU burst.
* Preemptive - if a new process arrives with CPU burst length less than remaining time of of current executing process, preempt.

Example of non-preemptive SJF:
	Process			   CPU burst time
 	P1		     		6
   	P2		     		8
   	P3		     		7
   	P4		     		3

Process :  	P4           P1	P3	P2
Time Line:	0	3	9	16	24
Average waiting time = (0 + 3 + 9 +  16)/4 = 7 ms

Example of Preemptive SJF
(Shortest-Remaining-Time-First)
	Process	Arrival Time 	Burst Time
	 P1			0	   8
	 P2			1	   4
	 P3			2	   9
	 P4			3	   5

Process:		P1    P2		P4	P1	P3
Time Line : 	0      1		5	10	17	26

When process P2	arrives, the remaining time for P1 (7 ms) is larger than the time required for P2 (4 ms), so process P1 is preempted and P2 is scheduled.
Average waiting time is :
((10-1) + (1-1) + (17-2) + (5-3)) / 4 = 6.5 ms.


=======================================

* Designed for time-sharing systems.
* Similar to FCFS, with preemption added.
* Each process gets a small unit of CPU time (a time slice), usually 10 - 100 milliseconds.
* After time slice has elapsed, the process is preempted and added to the end of the ready queue.

The ready queue can be implemented as a FIFO queue of processes. New processes are added to the tail of the queue. The scheduler picks the first process from the ready queue, sets a timer to interrupt after 1 time quantum and then dispatches the process. One of two things will happen:
1- The process may have a CPU burst of less than 1 time quantum, or
2- CPU burst  of the currently executing process is longer than one time quantum. In this case, the timer will go off, cause an interrupt, a context switch is then executed & the process put at the tail of the ready queue.

The average waiting time under the RR scheme is often quite long. Consider the following set of processes that arrive at time 0, the time quantum is set at 4 ms:
	Process		    CPU Burst Time
	  P1			24
	  P2			 3
  	  P3			 3

Process: 		P1	P2	P3	P1	P1	P1	P1	P1
Time Line:	0	4	7	10	14	18	22	26	30

The average waiting time is : 17/3 = 5.66 ms.


Performance of RR:
* If there are n processes in the ready queue at time quantum q, then each process gets 1/n of the CPU time in chunks of at most q time units at once. No process waits more than (n-1) x q time units until its next time quantum.
* The performance of RR depends on the size of q.
* At one extreme, if q is very large, RR policy is the same as FCFS policy.
* If q is very small, the RR approach is called   processor sharing. Overhead is too high.


=================================================


Priority Scheduling :
* The SJF is a special case of the general priority scheduling algorithm.
* A priority (an integer) is associated with each process.
* The CPU is allocated to the process with the highest priority (smallest integer = highest priority).
* Equal priority processes are scheduled in FCFS order.

Example: The following processes arrive at time 0 in the order - P1, P2, P3, P4, P5.
	Process	        Burst Time	Priority
	P1		10	   3
	P2		1	   1
	P3		2	   3
	P4		1	   4
	P5		5	   2

Process : 		P2	P5	P1		P3	P4
Time Line: 	0	1	6		16	18	19

The average waiting time is:
	(0 + 1 + 6 + 16 + 18)/5 = 8.2 ms

* Priority scheduling can be either preemptive or non-preemptive.
* A major problem with priority scheduling algorithms is indefinite blocking or starvation. Low priority processes could wait indefinitely for the CPU.
* A solution to the problem of starvation is aging. Aging is a technique of gradually increasing the priority of processes that wait in the system a long time.

thank you
