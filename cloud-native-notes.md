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


### Summary:

This chapter linked the Golang with the cloud native applications and showed how the Golang's ecosystem provides better tooling for the Cloud Native applications rather than the other languages such as C++, Java, or Python.

Main topics of discussion was following:

- Composititon and Structural Typing: Golang used this type of relations rather being a fully Object Oriented Language which makes it more easier to define object relations and provide interfaces for their implementation
- Comprehensibility: Go is a minimalist language with 25 keywords and 1 loop type (for only) which encourages clarity over cleverness.
- CSP-Style Concurrency: Go implements CSP style concurrency which favors to share memory with communicating rather than communicating by sharing memory.
- Fast Builds: Go builds are faster than many of the mainstream languages. For instance: The whole K8 v1.20.2 takes 45 seconds to build on a 8-core i9 MacBook Pro rather than other languages which may take minutes to hours to compile a system with same complexity on Google's large compilation clusters.
- Linguistic Stability: As of March, 2012, with Go 1 spec, it is a promise from the Go community that all applications on this spec will run without breaking changes during it's lifetime.
- Memory Safety: Go provides pointers for memory passing rather than bulky copying of objects but Go does not allow any pointer arithematic which is a cause of major security issues related to buffer overflow attacks etc.
- Performance: Performance wise Go performs 10-100s time faster than all the interpretted languages and on par with the low level languages such as Rust, C/C++.
- Static Linking: This type of linking makes the Go programs executable self dependently. Also, does not require any language runtime or other configuration. In fact Go binary can be used to directly create container images without any other dependency.
- Static Typing: Static Typing is more readable and more easier to work with as the types clarify the semantics of the code rather than the need of adding Docstrings/comments to clarify decisions. This is another step towards the Clarity vs. Cleverness argument and causes many bugs to be fixed and catched early in the development cycle.

## Chapter 3: Cloud Native Go Constructs

### Summary:

- Data types:
  1. Booleans (bool) => true or false
  2. Numeric - signed (int8,int16,int32,int64), unsigned (uint8,uint16,uint32,uint64), floating (float32,float64), complex(complex64,complex128. e.g. 3.1415i)
  3. String - (literal -> "hello\nworld!\n" and raw strings -> `Hello<newline here>world!`)
- Variables:
  - General Syntax: ```var foo type = expression```
  - with init: ```var foo int = 42```
  - multi declarations: ```var foo, bar int = 42, 1302```
  - with type inference: ```var foo = 42```
  - mixed multi declarations: ```var foo, bar = 88, "strings"```
  - without initialization (default zero val init): ```var s string```
  - Short Variable Declarations: ```var_name := expression```, type is inferred.

- Zero Values: every type has a zero val i.e the 0 byte representation of the value, e.g. integers -> 0, steings -> "" etc.

- The Blank Identifier: Represented by _ (underscore) is used to ignore a value returned from a function of expression. Is used in variable declarations and package imports because of some depedency. Also, if you do not use a variable after declaring it then the program will not compile, go's was of reducing dead and cluttered code, so we can use _ identifier there.

- Constants: As in all other languages, constants are unmodifiable values and are checked on compilation. Must be initialized with declaration to some value, does not intitalize by default to zero values of data types.

- Container Types: Arrays, Slices, and Maps. Has 3 first-class containers.

  - Arrays: Fixed sized containers for one type only. Declaration: ```var a[size]type```
  - Slices: Dynamic arrays for one type as arrays are. Declaration: ```a := make([]type, size)```. Initialized and declared using the builtin ```make()``` function.
  - Maps: Key value containers, typically implemented using hash map type of data structure. Declaration: ```a := make(map[key_type]value_type)```. Used builtin ```make()``` for declaration.


- Pointers: Pointers are variables to store other variable's memory addresses.
  - Declaration: ```var p *type = &foo```, here pointer ```p``` points to the address of ```foo```
  - Dereferencing: ```*p``` provides value in that address.
  - Initialization: Inititalized to ```nil``` if not provided with an address at the declaration.
  - Usage: used to avoid unnecessary overhead due to copying objects around.

- Control Structures: One of the basic and core building block of programming.
  - for loop: The one and only looping construct in golang. Can be used as while loop and traditional for loop.
    - range keyword for iterating over slices and arrays.
  - if statement: In contrast to other C-style languages, there is no  parentheses. Allows initialization.
  - switch statement: no parentheses and no fallthrough by default as C does.

- Error Handling: Treated in Go just as another value with built-in error type. There is no try catch here making it less error prone if you miss something.

- Functions: Variadics and Closures: Can return or accept multiple values, or being used as first-class types or anonymoud functions.
  - C-style declaration
  - Multiple return values
  - Allows recurrence
  - defer keyword: it can be used to schedule function calls before the end of function calling it. Ensures resource release and memory safety. Like atexit builtin for C/C++ languages.
  - Allows pass by reference using pointers.
  - Variadic Functions: Functions that allow zero or more trailing arguments as inputs. like the builtin ```fmt.Printf(format string, a ...interface{}) (n int, err error)``` funtion.
    - variadic operator (...) can be used to define such functions. Behind the scenes slice is used to make it behave as such.
  - Anonymous Functions and Closures: Functions maybe created within other functions which are then called anonymous functions. Anonymous functions have access to parent scope and have access even after the parent exits, such functions are called closures.
  - Can be used as return types and argument types.

- Structs, Methods, and Interfaces:
  - Struct: An struct is an aggregation of zero or more fields as a single entity.
    - A struct can never be ```nil``` instead its zero value is the zero value of all its field.
    - Fields can be accessed through dot notation as with classes in other languages.
    - As in many cases pointers to structs are used for passing structs back and on. So, the dereference is done automatically by the Go in case of accessing field values.

  - Methods: Methods are function attached to types (not specifically structs). Declared same as functions are but uses *reciever arguments* before the function name.
  - Interface: A set of method signatures. Can be used as a contract that a type may satisfy. No explicit satisfaction of interface required. If a type possesses all the methods defined in interface then it implicitly satisfies that interface.
    - Type assertion: Assert that some interface is a certain concrete type.
    - empty interface: An interface that has nothing, with no method and data.
  - Composition with Type Embedding: Go doesn't allow subclassing but allows functionality to be extended using embedding. It allows typed to be embedded within one another, extending the functionalities of the embedded types into the embedding type.
    - Interface embedding: An interface may require 2 or more interfaces to be implemented. So, we can use other interfaces as field to implement some interface that requires both of their functionality.
    - Struct embedding: Struct embedding are like same interface embeddings. But in this case struct requires other structs as part.
    - Promotion: Question arises that why not use addint a struct field instead of composition. The answer to that is the embedded type methods are promoted to embedding type. Thus, making them directly accessable from the embedding type.

- Concurrency: Concurrency is defined as being able to execute multiple parts of program at the same time.
  - Goroutines
    > Provides application level threads for asynchronous processing or concurrency using `go` keyword.
    > Syntax: `go func()`
  - Channels: 
    > Think of them as pipes for communications between the goroutines. At one end a routine sends data and is recieved by another goroutine at the other end 
    > Created using the `make` function.
    > Example Declaration: `ch := make (chan int)` makes a channel for sending and recieving `int` data. 
    > Sending: `ch <- val`
    > Recieving: `val = <- ch`
    - Blocking: By default every channel if *unbuffered* meaning the channel will block any incoming data until the channel is empty i.e. the recieving routine has recieved the data and inversly the recievers block until the sender sends the data.
    - Buffering: Channels can also be *buffered* meaning we can have a fixed *capacity* queue while initializing. Sends block only when queue is full and recieves block when queue is empty.
      > Creating a buffered channel:
      > ```go
      > myChan := make(chan int, buffsize)
      > ```

    - Closing channels: Another operation on channels in `close(chanName)` which sets a flag to not expect any more incoming value from the channel.
      > Caution: Sending on a closed channel will cause `panic` and must be avoided.

    - Looping over channels: Values from a channel can be extractes using `range` keyword until the channel is closed and has buffered values.

  - Select
    > `select` keyword is synonymous to `switch` but for multiplexing between channels.

## Chapter 4: Cloud Native Patterns

### Summary:

- Fallacies of Distributed Computing:
  1. Network is reliable
  2. Latency is zero
  3. Bandwidth is infinite
  4. Network is secure.
  5. Topology is constant
  6. There is one admin.
  7. Transport cost is zero.
  8. The network is homogeneous
  9. Services are reliable.
- Context Package: Provides idioms for carrying deadlines, cancellation signals and request-scoped values between processes. Has `context.Context` interface.
- What context can do?
  > It allows cancellation of sub-requests easier to coordinate their cancellation and reduce the amount of wasted time.
  > When a `Context` is cancelled, all `Context` derived from it are also cancelled but not the parent `Context`s

- Stability Patterns: These patterns are supposed to imporve the services' own stability and stability of the larger system they're part of.

  - Circuit Breaker:
    > Automatically degrades service functions in responce to likely fault, preventing cascading failures.
    - Applicability:
      > This pattern allows a service to detect a failure and to "open the circuit" by temporarily ceasing to execute requests.
      > For example if a database crashes, the server should be able to detect crash and temporarily open the circuit to avoid flooding logs and errors.
    - Participants
      - Circuit: The function that interacts with the service
      - Breaker: A closure with same function signature as `Circuit`

    - Implementation: The client interacts with the `Breaker` which has two states *open*, and *closed*. In case of open, the breaker forwards requests to `Circuit` unchanges and responses back to the client while in close state, the `Breaker` responds immediately with a meaningful error message.
    - Sample code: See [here](https://github.com/cloud-native-go/examples/tree/main/ch04)

  - Debounce: Limits the frequency of a function invocation so that only first or last in a cluster of calls is actually performed
    - Applicability:
      > This pattern is used to avoid many same type of calls to be performed in a given frame of time. It restricts other calls while only executing the first or last call to a function.
      > Can provide solution to problems such as The Thundering Herd by rate limiting and clever caching.
    - Participants:
      > Circuit: The function to regulate
      > Debounce: The closure for debounce logic with same function signature as `Circuit`

    - Implementation: The `Debounce` wraps the `Circuit` with the ratelimiting logic. 

    - Sample code: See [here](https://github.com/cloud-native-go/examples/tree/main/ch04)

  - Retry: Used to transparently