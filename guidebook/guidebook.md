# Context
1. What is this software project/product/system all about?
1. What is it that is being built?
1. How does it fit into the existing environment? (e.g. systems, business processes, etc)
1. Who is using it? (users, roles, actors, personas, etc)
1. Context Diagram should be included
1. Technical and non-technical audience

# Functional Overview
1. Highlight and summarize major functions of the software
1. Is it clear what the system actually does?
1. Is it clear which features, functions, use cases, user stories, etc are significant to the architecture and why?
1. Is it clear who the important users are (roles, actors, personas, etc) and how the system caters for their needs?
1. Is it clear that the above has been used to shape and define the architecture?
1. Is it clear what the system does from a process perspective?
1. What are the major processes and flows of information through the system?
1. Feel free to reference existing documentation
1. The goal is to provide and *overview*
1. Sequence diagram when discussing automated business processes is useful
1. Technical and non-technical people, both inside and outside the immediate development team

# Quality Attributes
1. Summarize key quality attributes
1. Performance (eg latency and throughput)
1. Scalability (eg data and traffic volumes)
1. Availability (eg uptime, downtime, scheduled maintenance, 24x7, 99.9%, etc)
1. Security (eg authentication, authorization, data confidentiality, etc)
1. Extensibility
1. Auditing
1. Monitoring and management
1. Reliability
1. Failover/disaster recovery targets (eg manual vs automatic, how long will it take?)
1. Business continuity
1. Interoperability
1. Legal, compliance and regulatory requirements (eg data protection act)
1. I18n and L10n
1. Accessibility
1. Usability
1. Use SMART (specific, measurable, achievable, relevant and timely) attributes
1. Technical people only

# Constraints
1. Summarize the constraints your're working in and some of the decisions that have been made for you
1. Time, budget and resources
1. Approved technology lists and technology constraints
1. Target deployment platform
1. Existing systems and integration standards
1. Local standards (eg development, coding, etc)
1. Public standards (eg. HTTP, SOAP, XML, XML Schema, WSDL, etc)
1. Standard protocols
1. Standard message formats
1. Size of software development team
1. Skill profile of the development team
1. Nature of the software being build (et, tactical or strategic)
1. Political constraints
1. Use of internal intellectual property
1. Technical and non-technical people

# Principles
1. Make it explicit what principles are being followed
1. Supply existing references, if they exist
1. Architectural layering strategy
1. No business logic in views
1. No database access in views
1. Use of interfaces
1. Always use an ORM
1. Dependency injection
1. The Hollywood principle
1. High cohesion, low coupling
1. Follow SOLID
1. DRY
1. Ensure all components are stateless (eg to ease scaling)
1. Prefer a rich domain model
1. Prefer an anaemic domain model
1. Prefer stored procedures
1. Avoid stored procedures
1. Don't reinvent the wheel
1. Approaches to error handling, logging, etc
1. Buy rather than build
1. Technical people only

# Software Architecture
1. Summarize the software architecture
1. What does the "big picture" look like?
1. Is there a clear structure?
1. Is it clear how the system works from the "30,000 foot view"?
1. Does it show major containers and technology choices?
1. Does it show major components and their interactions?
1. What are the key internal interfaces? (eg web service between web and business tiers)
1. Technical people only

# External Interfaces
1. What are the key external interfaces?
  * system-to-system
  * publicly exposed APIs
  * exported files
1. Has each interface been thought about from a technical perspective?
  * what is the technical definition of an interface?
  * if messaging is being used, which queues and topics are components using to communicate?
  * what format are the messages (eg. plain text, Avro, JSON)?
  * are they synchronous or asynchronous?
  * are asynchronous messaging links guaranteed?
  * are subscribers durable where necessary?
  * can messages be received out of order and is this a problem?
  * are interfaces idempotent?
  * is the interface always available or do you need the cache data locally?
  * how is performance/security/etc catered for?
1. Has each interface been thought about from a non-technical perspective?
  * who has ownership of the interface?
  * how often does the interface change and how is versioning handled?
  * are there service-level agreements in place?
1. A paragraph on each interface covering this topics is sufficient
1. Technical people only

# Code
1. Describe implementation details for important/complex parts of the system
1. homegrown frameworks
1. WebMVC frameworks
1. approach to security
1. domain model
1. component frameworks
1. configuration mechanisms
1. architectural layering
1. exceptions and logging
1. how patterns and principals are implemented
1. short description of each element using diagrams as necessary
1. Technical people only

# Data
1. Record anything that is important from the data perspective
1. What does the data model look like?
1. Where is data stored?
1. Who owns the data?
1. How much storage space is needed for the data?
1. Are there any requirements for long term archival?
1. Are there any requirements for log files and audit trails?
1. Are flat files being used for storage?
1. short description of each element using diagrams as necessary
1. Technical people only, including Operations

# Infrastructure Architecture
1. Describe the physical/virtual hardware and networks the software will be deployed to.
1. Is there a clear physical architecture?
1. What hardware does this include across all tiers?
1. Does it cater for redundancy, failover and disaster recovery if applicable?
1. Is it clear how the chosen hardware components have been sized and selected?
1. If multiple servers and sites are used, what are the network links between them?
1. Who is responsible for support and maintenance of the infrastructure?
1. Are there central teams to look after common infrastructure?
1. Who owns the resources?
1. Are there sufficient environments for development, testing, acceptance, pre-production, production?
1. Provide an infrastructure/network diagram with a short narrative
1. Technical people only, including Operations

# Deployment
1. Describe the mapping between software (containers) and the infrastructure.
1. How and where is the software installed and configured?
1. Is it clear how the software will be deployed across the infrastructure elements described in the Infrastructure Architecture section?
1. What are the options and have they been documented?
1. Is it understood how memory and CPU will be partitioned between the processes running on a single piece of infrastructure?
1. Are any containers/components running in an active-active, active-passive, hot-standby, cold-standby formation?
1. Has the deployment and rollback strategy been defined?
1. What happens in the event of a software or infrastructure failure?
1. Is it clear how data is replicated across sites?
1. Can use tables to show mapping between containers and infrastructure
1. Can use UML deployment diagrams
1. Can use color coding to designate runtime status (primary vs secondary, etc_
1. Technical people only, including Operations

# Operation and Support
1. Be explicit about to run, monitor and manage the software
1. Is it clear how the software provides the ability for Operations to monitor and manage the system?
1. Has is this achieved across all tiers of the architecture?
1. How can Operations diagnose problems?
1. Where are errors and information logged?
1. Do configuration changes require a restart?
1. Are there any manual housekeeping tasks that need to be performed on a regular basis?
1. Does old data need to be periodically archived?
1. A simple narrative should suffice here
1. Technical people only, including Operations

# Development Environment
1. Summarize how new team members set up a development environment
1. Pre-requisite versions of software needed
1. Links to software downloads
1. Links to virtual machines
1. Environment variables
1. Host name entries
1. IDE configuration
1. Build and test instructions
1. Database population scripts
1. Username, passwords and certificates for connecting to services
1. Links to build servers
1. Technical people only, developers specifically

# Decision Log
1. Capture major decisions that have been made
1. Why did you choose technology/framework X over Y and Z?
1. How did you make the selection? PoC? Product evaluation?
1. Did corporate policy or architecture standards force you to select X?
1. Why did you choose the selected architecture?  What other options did you consider?
1. How do you know that the solution satisfies the major non-functional requirements?
1. Short paragraph describing each decision. Include a date of the decision?
1. Technical people only
