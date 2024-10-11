# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers

1. In the search of a software bug, we found a article published by LeMagIT about the CrowdStrike incident.
This incident happened because of a bug in the EDR Falcon software from the cybersecurity company Crowdstrike.
They distributed a faulty configuration update for its Falcon sensor software running on Windows PCs and servers.
A modification to a configuration file which was responsible for screening named pipes, Channel File 291, caused an out-of-bounds memory read in the Windows sensor client that resulted in an invalid page fault. The update caused machines to either enter into a bootloop or boot into recovery mode.
Rebooting and blue screen loops froze 8.5 millions of devices in the world. This global bug paralyzed a large amount of companies in the entire world, from hospitals to airlines companies (thousand of planes cancelled) passing by banks and stocks markets. CrowdStrike fell more than 20% due to this bug.
Test have been made before they sent the update, but a particular way of the software wasn't really tested, only the "happy path" has been tested, and only valid datas were used, so yes testing the right scenario would have surely helped.

2. We chose the COLLECTION-796 bug, this bug is global because it affects everyone regardless of the material and the computer's configuration.
This bug happend because the method SetUniqueList.createSetBasedOnList doesn't add list elements to the return value any more. The documentation says it does, and it used to up to version 4.2, but a call to addAll was accidentally deleted.
Cbkurz managed to implement again the functionality then he did added tests, and also remove a typo in UnmodifiableListIterator.unmodifiableListIterator (previous 'UnmodifiableListIterator.umodifiableListIterator').

3.  Netflix performs several concrete experiments to test the resilience of their system:
    - Chaos Monkey: Randomly selects and terminates virtual machine instances to ensure that services can withstand individual instance failures.
    - Chaos Kong: Simulates the failure of an entire Amazon EC2 region to test the system's ability to handle large-scale outages.
    - Failure Injection Testing (FIT): Introduces failures in requests between Netflix services to verify that the system degrades gracefully.

    The requirements for these experiments include:
    - Robust and Redundant Infrastructure: The system must be designed to handle failures gracefully.
    - Advanced Monitoring Tools: Tools to monitor system performance and metrics in real-time.
    - Automated Recovery Mechanisms: Mechanisms to automatically recover from failures.
    - Regular Backups: Regular backups to ensure data integrity.
    - Engineering Teams: Teams ready to respond to any issues that arise during experiments.

    The variables observed during these experiments include:
    - Stream Starts Per Second (SPS): The primary metric used to measure the overall health of the system.
    - Request Latency: The time it takes for requests to be processed.
    - CPU Utilization: The usage of CPU resources by the system.
    - Error Logs: Logs of errors and exceptions that occur during the experiments.
    - User Complaints: Feedback from users about any disruptions in service.

    No, Netflix is not the only company performing these experiments. Other large tech organizations such as Amazon, Google, Microsoft, and Facebook also use similar techniques to test the resilience of their systems.

In other organizations, similar experiments could be performed to test the resilience of their systems. The types of experiments that could be performed include:
Network Failure Simulation, Database Failure Simulation, Load Testing (Simulating high traffic loads to test the system's ability to handle peak usage.), Configuration Change Simulation: Introducing changes to runtime configuration parameters to test the system's ability to handle unexpected changes.

The system variables to observe during these experiments could include:
Response Time: The time it takes for the system to respond to user requests.
Error Rates: The number of errors and exceptions that occur during the experiments.
System Throughput: The amount of data processed by the system per unit of time.
User Experience Metrics: Metrics that measure the impact on the user experience, such as page load times and user satisfaction scores.
Resource Utilization: The usage of system resources such as CPU, memory, and disk space.


4. Main advantages of a Formal Specification for WebAssembly :

 - Clarity and Precision: A formal specification provides a clear, accurate description of how WebAssembly should behave, reducing errors and misunderstandings.
   
 - Interoperability: It ensures consistent implementation across different browsers and environments, promoting code portability.

 - Security: The specification enables rigorous verification, reducing the risk of security vulnerabilities.

 - Optimization: It helps compilers and engines optimize code while ensuring consistent behavior.

 - Maintenance and Evolution: It supports consistent updates and extensions to the language without introducing errors.


Perhaps, yes we think that testing remains crucial. A formal specification doesn’t eliminate the need for:

 - Conformance Validation: To ensure implementations match the specification.
 - Bug Detection: To find issues not covered by the spec.
 - Performance Testing : To evaluate efficiency and optimize implementations.
 - Compatibility Testing: To ensure code works across different platforms.

In short, while a formal specification is valuable, testing is essential for quality and performance.


5. Main Advantages of the Mechanized Specification
    According to the author of the paper "Mechanising and Verifying the WebAssembly Specification," the main advantages of the mechanized specification are:
    - Precision and Clarity: The mechanized specification provides a precise and unambiguous description of WebAssembly's behavior, which is crucial for understanding and implementing the language correctly.
    - Formal Verification: The mechanized specification allows for formal verification of the WebAssembly type system, ensuring that it is sound. This means that well-typed programs will not encounter certain types of errors during execution.
    - Identification of Issues: The process of mechanizing the specification revealed several issues and inconsistencies in the original WebAssembly specification. These issues were corrected, leading to a more robust and reliable specification.
    - Executable Artifacts: The mechanized specification includes a verified executable interpreter and type checker. These artifacts can be used to validate the specification and ensure that implementations conform to it.
    - Interaction with Host Environment: The mechanized specification models the interaction between WebAssembly and its host environment, which is a crucial aspect of the language's behavior.

Improvement of the Original Formal Specification
Yes, the mechanized specification helped improve the original formal specification of WebAssembly. The author mentions that the process of mechanizing the specification uncovered several deficiencies and unsoundness issues in the original specification. These issues were communicated to the WebAssembly working group and subsequently corrected, leading to a more accurate and reliable specification.

Other Artifacts Derived from the Mechanized Specification
Several artifacts were derived from the mechanized specification:
Verified Executable Interpreter: An interpreter that executes WebAssembly programs while adhering to the formal specification. This interpreter is proven to be correct with respect to the mechanized specification.
Verified Type Checker: A type checker that ensures WebAssembly programs conform to the type system defined in the mechanized specification. This type checker is also proven to be sound and complete.
Proof of Soundness: A fully mechanized proof of the soundness properties of the WebAssembly type system. This proof ensures that well-typed programs enjoy progress and preservation properties during execution.

Verification of the Specification
The author verified the specification through several means:
 - Formal Proofs: The author provided formal proofs of the soundness properties of the WebAssembly type system. These proofs were mechanized using Isabelle, ensuring their correctness.
 - Conformance Tests: The executable interpreter derived from the mechanized specification was validated using the official WebAssembly conformance test suite. This ensures that the interpreter behaves correctly according to the specification.
 - Fuzzing Experiments: The author conducted fuzzing experiments to further validate the mechanized specification and the executable interpreter. These experiments involved generating random WebAssembly programs and comparing the behavior of the verified interpreter with industry implementations.

Need for Testing ?
 No, the mechanized specification does not remove the need for testing. While the mechanized specification provides a formal basis for the language and allows for formal verification, testing remains essential for several reasons:
 - Validation of Conformity: Tests help validate that implementations conform to the formal specification. They can reveal discrepancies between the theory and the practice.
 - Detection of Bugs: Tests can identify bugs and unexpected behaviors that may not be covered by the formal specification or the mechanized proofs.
 - Performance and Optimization: Tests are necessary to evaluate the performance and optimizations of WebAssembly implementations, which are not covered by the formal specification.
 - Compatibility: Tests ensure that WebAssembly code runs correctly across different platforms and browsers, even if these platforms have slight differences in their implementations.
In summary, while the mechanized specification provides a strong foundation for the formal analysis and verification of WebAssembly, testing remains a crucial component for ensuring the quality, security, and performance of WebAssembly implementations.






