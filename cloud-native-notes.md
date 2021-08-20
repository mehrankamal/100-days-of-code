## Book: Cloud Native Go: Building Reliable Services in Unreliable Environments

## Chapter 1: What Is a “Cloud Native” Application?

### What is cloud native?

Three components:
- Scalability: Scalable in the face of changing load
- Resiliency: Resilient in face of environment uncertainty
- Managalility: Managable in face of changing requirements

A cloud native service must be designed to achieve all these goals, according to [CNCF]().

A kludgy application is still cludgy even if you containerize it and deploy on K8s because the applicaion is not primarily designed to be cloud native.


## Era of computing:

- Started with bulky happy monoliths on a mainframe machine that is accessed using some dumb terminal with no computing power in 1950s.
- Then comes, in 1980, inexpensive network-connected PC era with some computing power on the hand of user. This led to decoupling systems into three main layers/tiers.
  
  1. Presentation, here comes the client systems and users
  2. Business, here comes the web and applicaion servers
  3. Data, here comes the databases and stores

- In 1990, with popularization of World Wide Web, introduced the SaaS model for enterprices and drove the development of complex and resource-hungry applicaions. And multitiered architecture further broke down to sub-components which were indepdent and scalable.

- In 2006, as Amazon launched AWS and EC2 compute services revolutionizing the IaaS. Gave the user the ability to scale quickly. But introduces the problem of migrations and services became to break and also scaling manually using VMs is not easy.

## So, what it means to be cloud native?

Being a truly cloud native service means to incorporate all the things learned in those 50-60 years and provide 1) scalability, 2) maintainability, and 3) reliability. Or we can say that cloud native application is an application built for living in a crudl, uncertain world.

```
Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds….

These techniques enable loosely coupled systems that are resilient, manageable, and observable. Combined with robust automation, they allow engineers to make high-impact changes frequently and predictably with minimal toil.

—Cloud Native Computing Foundation, CNCF Cloud Native Definition v1.0
```

So, a cloud native application is considered an application which has the following attributes:

1. scalable
2. loosely coupled
3. resilient
4. managable
5. observable

### Scalability:

System is scalable if the increase or decrease in demand does not need to make refactoring changes to perform the intended functionality.

There are two types of scaling:

1. **Vertical Scaling or Scaling up:** Which means to allocate more hardware resources to same instance running the service such as increasing the storage/memory of a database instance. But this is limited by the limit a single computer having at max level of computation which is limited.

2. **Horizontal Scaling or Scaling out:** Which means to increase the instances running an specific service and make the loadbalancer emit traffic to that instance to fulfill request(s). Benefit of this pattern is that there is no limit to the number of instances we can add to the system but problem is the orchestration of the system and making the applicaion stateless for this purpose.

#### When a system is horizontally scalable and when vertically?

It comes down to the state of the system or service. A stateless service is more easily horizontally scaled whereas a stateful applicaions is easily vertically scalable if that can take benefit of added resources. 

### Loose Coupling:

System is loosely coupled if changes in one component does not require changes in other component(s). That said, the components need minimal knowledge of other components to operate.

### Resilience:

Roughly synonymous to fault tolerance is measure of how well a system withstands and recovers from errors and faults. A system is considered resilient if it can operate correctly-maybe at a reduced level- rather than failing completely when some part of system fails.

Loosely coupled systems also protect us from cascading failures in the sub-systems to finally causing the whole system to fail.

Redundant components, Circuit Breaker Patterns and other retry logics are used to comply with system resiliency and to not cause the whold system to collapse.


Note: Resilience and reliability are not same.

### Managability:

System's Managability is the ease of modifying it's behavior to keep it secure, running smoothly, and compliant to changing requirements. A system is managable if it is sufficiently easy to alter it's behavior without needing to change its code. Think of it like a configurable applicaion but not only. It also covers other dimensions of the system.

Note: Managability is not maintainability

### Observability

A system is considered observable if the internal states can be inferred from knowledge of its external outputs withoud having to reinstrument or build new code. This is achieved through rich data from the system metrics, logging and tracing.

## Why is Cloud Native a thing?

Cloud native exists because of the current scale of the systems are extra-ordinarily large in both size and the amount of data they process. Consider 100s of 1000s of servers being deployed, maintained and monitored to cope up with the user's ever changing requirements.


## Chapter No 2: Why Go Rules the Cloud Native World?

### The Motivation Behind Go

- In September 2007, when the era of multicore systems and distributed environments began, Google decided felt the need of a new language for developing such systems.

- Deveopled by 3 geniuses, master in their craft of designing other languages: Robert Griesemer, Rob Pike, and Ken Thompson.

### Features of the Cloud Native World:

The complexity of writing such systems using other traditional languages caused the code to be unreadable and unavoidable repetitions.

- Low program comprehensionability: Code demanded cleverness over clarity. And as the codebase grew, the mess grew.

- Slow builds: Language compilation and years old unnecessary language grammars caused the builds to run minutes and even hours on big clusters.

- Inefficiency: Due to above slow builds, programmers responded with more fluid, dynamic languages and trading the system efficiency.

- High cost of updates: The incompatibility in even minor versions of language or dependencies caused the updating a pain in the neck.

Over years, people proposed solutions to address these issues but these solutions introduced more complexity instead of decreasing them.
