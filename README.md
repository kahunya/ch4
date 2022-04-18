# Deadlocks

## Resource Usage

1. request
2. use
3. release

## Definition

A deadlock occurs when for a set of processes, each process in the set is waiting for an event that can only be caused by another process.

## Conditions

1. Mutual exclusion must be implemented
2. Processes must be holding their resources and proceed to wait for the event
3. There must be no pre-emption
4. There must be a circular wait condition

## Strategies

1. Ignore the problem (Ostrich algorithm)
2. Detection and Recovery: let deadlocks occur, detect them, and correct them
3. Dynamic avoidance by careful resource allocation
4. Prevention, by structurally negating one of the four required conditions


## Detection
1. For each node N in the graph, perform following five steps with N as starting node
2. Initialize L to empty list, and designate all arcs as unamrked
3. Add current node to end of L, check to see if node now appears in L two times. If so, graph contains a cycle and algorithm terminates
4. From given node, see if there are any unmarked outgoing arcs. If so, go to step 5; if not, go to step 6.
5. Pick unmarked outgoing arc at random, mark it. Then follow to new current node and go to step 3.
6. If this is initial node, graph does not contain cycles, algorithm terminates. Otherwise, dead end. Remove it and go back to the previous node.

## Detection with Multiple Resources
1. Look for unmarked process Pi for which the ith row of R is less than or equal to A
2. If such a process is found, add the ith row of C to A, mark the process, go back to step 1
3. If no such process exists, algorithm terminates

## Recovery
1. Preemption: take resource away from current owner
	- problem: other process cannot do its work
2. Rollback: process checkpoints to go back to
	- problem: rolling back just to deadlock again, configuration of checkpoints, uses extra space
3. Killing Processes: self-explanatory
	- problem: self-explanatory
	

## Deadlock Avoidance
Is there an algorithm that can always avoid deadlock by making the right choice all the time? Only if certain information is available in advance
### Safe and Unsafe States
- safe states: a state where some scheduling order in which every process can run to completion even if all of them suddenly request their maximum number of resources immediately
### Banker's Algorithm
- checks to see if granting a request leads to a safe state


## Deadlock Prevention
1. Attacking Mutual Exclusion: Spooling
	- can lead to deadlock if two processes filled up one half of available spooling space with output (if daemon relies on full output)
2. Attacking Hold and Wait: Request all Resources before Execution
	- processes often dont know how many resources they need until runtime  
	- resources also wont be used optimally 
3. Attacking No Pre-emption: Virtualization
	- not all resources can be virtualized
4. Attacking Circular Wait: Single Entitlement or Numbering
	- some processes NEED more than one resource at a time
	- a satisfactory ordering may be impossible to find
	

## Communication Deadlock
- cooperative synchronization as opposed to competitive synchronization
- solved with timeouts rather than the other methods

## Livelock
- a process tries to give up the locks it already acquired, waits, tries again
	+ but two processes do this