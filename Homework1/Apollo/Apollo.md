# First sight of Apollo:

#### A Scalable and Coordinated Scheduler for Cloud-Scale computing

## Background

It use high-level SQL-like languange.The job query plan is represented as a DAG, tasks are the basic unit of computation, which are grouped in stages. The excution is driven by a schedular.

For example, a query job like 

**Select** AVG(DatetTime.Parse(latency)) **As** E2ELatency, market **From** QueryLatencies **Group by** market    

will be represented like

![1](D:\ren\Homework1\Apollo\1.png)

## Challenges

  To scheduling at Cloud Scale, the scheduler should minimize job latency while maximizing cluster utilization.  To achieve it, there are three main chalenges:

####   Challenging Scale

   Since jobs process gigabytes to petabytes of data and issue peaks of 100000 scheduling requests/seconds, and clusters run up to 170000 tasts in parallel and each contains over 20000 servers, so the challenge is how to make optimal scheduling decisions at full production scale.

####   Heterogeneous workload

   Another challenge is the complexity of tasks. As a task, it can run from seconds to hours, it can be IO bound or CPU bound, it can require from 100 MB to more than 10GB of memory. Short tasks are sensitive to scheduling latency, Long IO bound tasks are sensitive to locality. So the second challenge is how to make optimal scheduling decisions for a complex workload.

####   Maximize utilization

   We need to effectively use resources and maintain performance guarantees but the workload constantlyy fluctuates. The challenge is how to maxinmize utilization while maintain performance guarantees with a dynamic workload.

## Overview of Apollo

#### Distributed and Coordinated

To scale, Apollo adopts a distributed and coordinated architecture There is one scheduler per job each making high quality decisions independently, informed by global information.The distributed architectures scales by allowing schedulers to make independent decisions with global coordination .



#### Representing![2](D:\ren\Homework1\Apollo\2.png) Load

The server load representation must
― Be hardware independent
― Be lightweight
― Supports heterogeneous workload
Apollo represents the load
― Using a wait-time matrix
― It represents the expected wait time to obtain resource of a certain size

As a conclusion, the wait time matrix allows to reason about future resource availability.

#### Estimation-Based Scheduling

Apollo minimizes the estimated task completion time with this formula:

\<center\> **E = I + W + R**\</center\>

in which **E** means  **Estiamted task completion time**, **I** means **Initialization time**, **W** means **Wait time** , **R** means **Runtime**

#### Conflict resolution

The cluster is dynamic. Schedulers can have conflicts, and Apollo defers the correction of conflict.

Triggers a duplicate if the decision isn't optimal with up to date information.

#### Opportunistic Scheduling

For Apollo, maximizing utilization

- Use the remaining capacity

- Dispatch more than the resource allocation

- Tasks only consume otherwise idle resources

- Tasks can be preempted or terminated

- Tasks can be upgraded 

  ## Pros

     Apollo's Shared state is read-only, the scheduled transaction is committed directly to the machine in the cluster, and the machine itself checks for conflicts to accept or reject the change, which allows Apollo to execute even if the Shared state is temporarily unavailable

  ## Cons

  ​    It must work in a situation where there is stable information (unlike a central scheduler), which can cause performance degradation of the scheduler in a highly competitive cluster of resources (although this can happen in other frameworks as well).



##  My comments

​    Apollo is a kind of Shared state scheduling architecture. Comparing to centralized scheduling architecture, it use Resource Monitor to maintain a globally Shared cluster state, that is, continuously collecting the load information of all Process nodes of the cluster and providing each Job Manager with a global view of the cluster state.