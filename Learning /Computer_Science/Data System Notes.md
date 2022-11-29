```toc style: bullet | number | inline (default: bullet) min_depth: number (default: 2) max_depth: number (default: 6) title: string (default: undefined) allow_inconsistent_headings: boolean (default: false) delimiter: string (default: |) varied_style: boolean (default: false) 
```
### 1. Reliable, Scalable, and Maintainable Applications
A data intensive application is typically built from below:
- store data (databases)
- Remember the result of an expensive operation, to speed up reads ([[caches]])
- Allow users to search data by keyword or filter it in various ways (search indexes)
- Send a message to another process, to be handled asynchronously (stream processing)
- Periodically crunch a large amount of accumulated data (batch processing)
> why should we lump them all together under an umbrella term like data systems?
1. Many new tools for data storage and processing have emerged in recent years. like Redis or Apache Kafka.
2. increasingly many applications now have such demanding or wide-ranging requirements that a single tool can no longer meet all of its data processing and storage needs.
#### Thinking About Data System
A lot of tricky question will arise when design a data system:
- How do you ensure that the data remains correct and complete, even when things go wrong internally?
- How do you provide consistently good performance to clients, even when parts of your system are degraded?
- How do you scale to handle an increase in load?
- What does a good API for the service look like?

We focus on three concerns that important in most software systems:
**Reliability**
	System should continue to work correctly even in the hardware or software faults, and even human error
**Scalability**
	As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth. 
**Maintainability**
	Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively. 

#### Reliability