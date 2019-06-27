# Software Technical Debt and Risk Assessment

## Introduction
Here is described a general framework for objectively assessing the technical debt, and risks associated with technical debt for a given codebase. A codebase generally describes a discrete system or application tier that is written in a single programming language. For complex and multi-tier systems it may be useful to assess each sub-system or tier separately or independently.

## Goals of the assessment:
Determine a measure of overall quality of software project with respect to:
- A) Maintainability – cost of extending or adding features, or fixing problems
- B) Scalability – cost of system ownership as a function of growth and adoption
- C) Stability – likelihood of problems related to software errors or limited error handling
- D) Conformance – use of and support for established and proven software engineering and operational practices

## What this assessment is not intended to measure:
- Security – penetration testing of deployed environments
- Bugs – presence of software bugs or incorrect features
- Performance and capacity – load testing of deployed environments

## A) Maintainability
The relative ease of a software product for developers to work on is a key yard-stick for the quality of code and technical merit of a product generally.  Projects which are easier to maintain lower the cost, and increase the speed, of development by removing unnecessary hurdles for unfamiliar developers to overcome before they begin to add business value to the product. Low maintenance code bases are easier for engineers of all levels to extend and resolve issues, because they can spend less time trying to understand the code relevant to the business process at hand.

Projects which have been engineered using principles that allow easy maintenance also generally have the benefit of increase stability, performance and adherence to standards. With clean and concise code, it is less likely that bugs will be become hidden in the codebase. Code that is easy to reason about is easier to optimise. With easily understood software, the presence of common patterns can be more efficiently recognised, and generally accepted solutions can be applied (not re-inventing wheels).

### Local development set-up
- Is there an up-to-date and document describing how to run the system locally included in the project?
- Is is possible to build and run the system locally without having to connect to external databases or web services?
- How much time does it take for a developer to obtain and install the necessary system tool chain required to run the system locally?
- How long does it take to build the system and run locally to the point of being able to manually test or inspect code changes?

### Project Structure
- Is there documentation which explains how the project is structured with relational to functional and architectural design?
- Is the project divided into logical and easily identified areas cleanly separating architectural concerns?
- Is the project or project divisions cleanly (sub) divided into logical and easily identified areas cleanly separating functional concerns?
- Is there a uniform and sensible approach to splitting code into files of manageable size?
- Are external libraries explicitly defined and with compatible versions stated?
- Are there mechanisms for cleanly separating and managing settings and dependencies required for various environments e..g development, test, and production?

### Code Structure
- Is there a document providing an overview of code structure from a class or module level e.g. a class diagram?
- Is the code organised into logical units via classes or modules which semantically represent underlying features?
- Is the structure interface-designed so that implementation details are separated from higher functions?
- Is there a sufficient level of abstraction at the class or module level which encourages re-use and avoids duplication, but does not overly impede identifying and understanding business logic?
- Are functions and methods keep reasonable short and with a single-purpose?
- Is code structured to facilitate effective unit-testing by externalising dependencies e.g. using the inversion of control pattern?
- Is code structured to facilitate effective unit-testing by clearly defining inputs and expected outputs?

### Code Style
- Is there document or a reference to some standards describing code style conventions?
- Are there automated tools to check adherence to code styles? Are these run as a requirement for a successful build?
- Are comments applied consistently to explain non-intuitive or subtle operations?
- Have relevant code auto-documentation tools been used appropriately to annotate modules, classes and functions/methods?
- Are functions and methods and classes consistently annotated with good English descriptions?
- Are identifiers such as classes, methods and variables named appropriately with a low semantic gap between name and function?
- Are comments never used to deactivate code (‘commented-out’), except where surrounding comments explicitly explain the relevance of the commented-out code and usefulness to future readers?
- Is there never pointless or excessively verbose code such as checking a typed boolean value is equal to true with an if statement guard?
- Is there an execution path to all code – i.e. all code is reachable?
- Are there tools configured to verify all code is reachable?

### Development Data
- Is there an automated method of obtaining realistic production-like data for development work?
- Is there an automated method of obtaining actual production data which has been masked to remove sensitive or identifying information?

## B) Scalability
Well designed software systems are built for success. Although one must be wary of over-engineering and ‘gold-plating’ (the best solution is usually the simplest) – it’s important that the software is built to grow and not place artificial limits on business success.

Good software uses the built-in features of programming languages and storage platforms to efficiently process and store data as these often come at no extra cost, but do require awareness and knowledge on the part of the developer. Consistent use of efficient data structures and appropriate algorithms shows that the developers are aware that performance is important, but hard to sometimes hard to diagnose and fix, and therefore use good practices in all cases to favour performance, without introducing complexity.

Generally simplicity is favoured over performance when writing new code as the vast majority of code executes extremely quickly. It can be difficult even for experienced developers to anticipate the parts of code which are sensitive to scaling (‘bottlenecks’). Great software projects utilises performance testing approaches to identify these bottlenecks. It’s only in these areas where simple code should be re-factored to highly-optimised code, which sometimes become more difficult to understand.

Software should be designed to scale well vertically (e.g. support more users) and horizontally (allow for new features to be written). Scaling out features is assisted by well designed codebases from a maintenance perspective, also thought should be given as to how the system can integrate with other services, external or internally. Using an interface-based design can greatly assist in extendibility over a software products lifetime.

Data stores should be appropriately structured to support future growth and extension. When using a client-server data store, efficient retrieval and transmission is a consideration to improve performance and network utilisations. The decision to use structured, semi-structured or unstructured data stores should be made carefully support anticipate vertical or horizontal growth.

### Programming Language features
- Is a recent, stable version of the language used?
- In typed languages, have variables of the appropriate type and size been used?
- Have built-in features to efficiently represent data structures such as lists, dictionaries and hash tables been appropriately used?

### Structured Data Stores
- For online transaction processing type relation data stores, has the schema been designed using a well normalised form?
- If there are large tables or complex queries evident, is there appropriately defined structures for optimisation e..g indexing or caching?
- For online analytical processing (reporting) type data stores, is the data transformed and populated in a reasonable time-frame? e.g. less than one hour for daily operations or less than one minute for hourly operations?

### Non-structured and Semi-structured Data Stores
- If non-structured (such as NoSQL) backend are employed, are they a good fit for the data use case?

### Performance testing
- Is there a standard method or procedure for load testing?
- Is there a document which explains what frameworks and tools have been configured to performance test the application?
- Is there and environment which mimics the production environment that can be used to simulate the required loads?
- Is there a historical record of benchmarks attained?

## C) Stability
In deployed systems, faults generally exist, and are discovered over time - or in response to new data inputs or problems of scale. This is to say that they do not spontaneously erupt. Here we consider stability as a result of development work i.e. the resilience of a codebase to deleterious software changes and upgrades.  In unstable systems, new problems can occur during development cycles which increase the cost of development, or post-live deployment which can cause significant development and business costs, even reputation al damage. Technically sound projects employ a wide range of techniques to lower the risks of breaking changes.

### Unit Testing
- Is there a unit test suite with good code coverage that can detect a wide range of low-level errors? Do all unit tests run and pass?

### Automated Code Checking
- Are static analysis tools employed to check for likely code errors?

### Continuous Integration
- Are unit tests, static analysis, style checks able automatically run prior as part of the code build process?
- Are branches of code automatically built and tested on check-in?
- Is successful build and test required prior to integration new code into the main source code repository?

### Continuous Deployment
- Is the latest integrated version of code under development automatically deployed to a test environment after successful build and test?

### Automated Integrating Testing
- Is there are mechanisms or frameworks in place to reliably perform automated integration test on a standard test environment?

### Defensive Coding and Code Style
- Are user inputs validated according to expected data and sensible ranges?
- Are parameters to public interface methods always according to expected ranges?
- Are global variables variables avoid and never exposed across interfaces?
- Are variables declared for use in minimum possible scope?
- Are variables never re-used to store different conceptual entities?
- Is error handling employed in a consistent style?
- Do error handling mechanisms preserve error information?
- When errors are handled, is the system state appropriately restored?
- Are errors logged in a consistent manner? Are error logs easily accessible on deployed systems?

### Structured Data Stores
- For relational databases, have foreign key constraints been used to enforce referential integrity?
- For relational databases, have NOT NULL constraints always been defined where null data would be meaningless to the application?

### Deployment
- For application updates, is there a completely automated (single-step) process for updating deployments from the latest master version in source control?
- Is the production deployment process completely testable in a like-for-like
- non-production environment?
- Is there an automated way to determine the success of deployments?

## D) Conformance
This section covers a range of established practices in software engineering which generally have effect of improving the codebase from a maintenance, scalability and/or stability perspective. These practices are the result of decades of prior work to achieved these outcomes. Adhering to these practices is the hallmarks of quality software projects.

### Source control
- Is any centralised or distributed source control system always used by developers?
- Is there a documented source control process flow?

### Frameworks and library code
- Does the project employ software frameworks to solve common technical problems which are general to application development distinct from the business domain?
- Have mature software frameworks, been appropriately selected for the project?
- Are frameworks likely to be supported well in the future?

### Standards
- Have appropriate standards be used e.g. ISO formats for dates, country codes, currency codes?  

### Secrets
- Are secrets e.g. passwords and API keys always stored encrypted?
