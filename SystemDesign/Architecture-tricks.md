- [Architecture Tricks](#architecture-tricks)
  - [Clock Sync across servers](#clock-sync-across-servers)
    - [Lamport clock](#lamport-clock)
    - [Hybrid Clock](#hybrid-clock)
  - [Data conflict](#data-conflict)
    - [CRDT](#crdt)
    - [Consistent Hashing](#consistent-hashing)
    - [Basic conversion](#basic-conversion)

# Architecture Tricks

## Clock Sync across servers
### Lamport clock
Use logical timestamps as a version for a value to allow ordering of values across servers

``` csharp
class LamportClock 
{
      int latestTime;
  
      public LamportClock(int timestamp) 
      {
          latestTime = timestamp;
      }
}
```

Usages:
- Databases like MongoDB and CockroachDB use variants of the Lamport Clock to implement [mvcc] storage
- Generation Clock is an example of a Lamport Clock


Links:
- [Lamport Clock](https://martinfowler.com/articles/patterns-of-distributed-systems/lamport-clock.html)
- [Generation Clock](https://martinfowler.com/articles/patterns-of-distributed-systems/generation.html)


### Hybrid Clock

Use a combination of system timestamp and logical timestamp to have versions as date-time, which can be ordered


Links:
- [Hybrid Clock](https://martinfowler.com/articles/patterns-of-distributed-systems/hybrid-clock.html)


## Data conflict

### CRDT
A Conflict-free Replicated Data Type (CRDT) is a data structure that simplifies distributed data storage systems and multi-user applications.

In many systems, copies of some data need to be stored on multiple computers (known as replicas). Examples of such systems include:

- Mobile apps that store data on the local device, and that need to sync that data to other devices belonging to the same user (such as calendars, notes, contacts, or reminders);
- Distributed databases, which maintain multiple replicas of the data (in the same datacenter or in different locations) so that the system continues working correctly if some of the replicas are offline;
- Collaboration software, such as Google Docs, Trello, Figma, or many others, in which several users can concurrently make changes to the same file or data;
- Large-scale data storage and processing systems, which replicate data in order to achieve global scalability.

Links:
- [crdt.tech](https://crdt.tech/)
- [Diving into Conflict-Free Replicated Data Types (CRDTs)](https://redis.com/blog/diving-into-crdts/)

### Consistent Hashing
Consistent hashing is a strategy for dividing up keys/data between multiple machines.

It works particularly well when the number of machines storing data may change. This makes it a useful trick for system design questions involving large, distributed databases, which have many machines and must account for machine failure.


Links:
- [Consistent Hashing](https://www.interviewcake.com/concept/java/consistent-hashing)


### Basic conversion
| type | size (in byte)|
|------|---------------|
| byte, sbyte | 1      |
| short, ushort | 2  |
|int, uint | 4 |
| float | 4 |
|long, ulong | 8 |
| double | 8 |
| object | 4 (referene)|
|char | 2 |
| string | 4 (reference)|
| decimal | 24 | 
| bool | 1 | 
|DateTime | 8 |


Links:
- (C# Primitive Datatypes)[https://condor.depaul.edu/sjost/nwdp/notes/cs1/CSDatatypes.htm]
- [Back of the Envelope Calculation](https://dev.to/vladisov/back-of-the-envelope-calculation-4eal)
