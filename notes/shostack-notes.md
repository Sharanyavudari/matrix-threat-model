 Shostack Ch. 1: Dive In and Threat Model!

Threat modeling is organized around four questions:

1. What are we building?
2. What can go wrong?
3. What should we do about those things that can go wrong?
4. Did we do a decent job of analysis?

---

 1. What are we building?

Before looking for threats, the team needs a shared picture of the system. Diagrams are the usual way to communicate this, and the simplest useful one is a data flow diagram (DFD):

- Blocks represent processes (and other elements such as data stores and external entities).
- Arrows represent data flowing between them.
- Trust boundaries are drawn wherever the level of privilege or trust changes, for example between a user's browser and a server.

The DFD is the input to the next question: once we can see where data moves and where trust changes, we can start asking what can go wrong.

 2. What can go wrong?

Trust boundaries are the best place to start. For each one, ask how it could be crossed and how an attacker could reach something valuable.

Approach:
- Brainstorm on your own first, then use STRIDE to check the threats you found and to fill gaps.
- Apply STRIDE to the different processes and elements of the diagram, and think broadly about every way each category could affect the system.

How to identify threats:
- Work in an organized order, starting from external entities or from business logic, rather than randomly.
- Don't discard a threat just because you weren't looking for it. Record it.
- Prioritize the most feasible threats first.

 3. What should we do about those things that can go wrong?

There are four ways to address a threat:

| Strategy | Meaning |
|---|---|
| Mitigate | Make the threat harder to exploit. |
| Eliminate | Remove the feature or entity that creates the threat. |
| Transfer | Let another party or system carry the risk (for example, a third-party service or insurance). |
| Accept | If the cost of addressing the threat far outweighs its impact, doing nothing is a valid decision. |

Practical notes:
- Prefer input validation over sanitization. Sanitization functions are hard to get right and bring their own problems.
- At the start of a model it is reasonable to rely on the operating system's built-in protections rather than threat modeling the OS itself, and to revisit that assumption later.

 4. Did we do a decent job of analysis?

Check three things:

1. Check the model. Confirm the diagram matches the real system. If it doesn't:
   - Focus on data flow rather than control flow.
   - Add security context where it is needed.
   - Show data sinks.
   - Include the processes that move data.
2. Check the threats. There are two questions here:
   - Was each threat addressed correctly?
   - Did we find all the threats we should have?
3. Check the tests. Test each addressed threat, either manually or with automation, to confirm the mitigation works.

Shostack Ch. 2: Strategies for Threat Modeling

THREE APPROACHES TO THREAT MODELING

1. Focusing on assets
2. Focusing on attackers
3. Focusing on software

Getting started
A good starting point is a literature review: read existing threat models of systems similar to yours, understand how and why they were done, then brainstorm ideas for your own analysis.

Choosing an approach
To decide which approach suits the system, brainstorm the trade-offs using one of these techniques:

1. Scenario-based: walk through scenarios drawn from the use cases of the current development cycle, such as failover scenarios.
2. Pre-mortem: imagine the system has already failed, then express the concerns and doubts that explain why.
3. Movie plotting: build a storyline around a flawed protagonist (our system), a brilliant antagonist (the attackers) and imaginary gadgets, making sure all three are involved.

----------------------------------------

1. FOCUSING ON ASSETS

This approach is not very common. It is generally used by security experts with deep threat modeling knowledge and experience.

In this context, an asset can be:
a. something an attacker wants (tangibles such as keys and data)
b. something the security team wants to protect (intangibles such as reputation)
c. something required for either of the above

Process: list all assets, associate them with computer systems, draw them with their interconnections, work out how an attacker could threaten each asset, and list the resulting threats.

Drawback: agreeing on the list of assets takes a lot of effort, and a methodology for the actual threat modeling is still needed afterwards. By that point, no threats have been found yet.

2. FOCUSING ON ATTACKERS

Like the asset-centric approach, this is not optimal. It considers attacker types, their resources and capabilities, and human-centered attacks. What it does well is help us understand who might want to attack the system.

3. FOCUSING ON SOFTWARE

Software-centric models focus on the software being built or the system being deployed, which helps expose the accumulated complexity of the system.

This approach requires modeling the system with diagrams. The goal of every diagram is to communicate how the system works, so that everyone involved in the threat model shares the same understanding.

Types of diagrams

1. Data flow diagram (DFD)
2. Unified Modeling Language (UML): if the software process already uses UML, add trust boundaries for threat modeling.
3. Swim lane diagrams: represent the flow between participants.
4. State diagrams: represent the states a system can be in and the transitions between them.

DFD elements

Process: rectangle with rounded corners. Any running code.
Data flow: arrow (from source to sink). Communication between processes, or between processes and data stores.
Data store: two parallel lines. Things that store data.
External entity: rectangle. People, or code outside your control.

----------------------------------------

TRUST BOUNDARIES

There are two ways to add trust boundaries:
- add the known boundaries, then look for more, or
- enumerate the principals and derive boundaries from them.

Two main questions to ask:
1. Do all principals have the same privilege and access to the complete system?
2. Is everything in the system inside the same boundary?

Most threats cluster around trust boundaries, so ensuring they are correctly drawn is necessary.

WHAT TO INCLUDE IN A DIAGRAM

- Show the events that drive the system.
- Show the processes that are driven.
- Determine what responses each process will generate and send.
- Identify the data sources for each request and response.
- Identify the recipient of each response.
- Ignore the inner workings and focus on scope.
- Ask whether something will help you think about what goes wrong or find threats.

VALIDATING DIAGRAMS

Validating a diagram has two main goals: ensuring accuracy and aspiring to goodness. Include the elements that have a security impact, and for each one consider whether that impact arises in a common scenario or only in a special instance.

Shostack Ch. 3: STRIDE

OVERVIEW

Each STRIDE threat violates a different security property and affects different parts of the system.

Spoofing
Property violated: authentication
Meaning: pretending to be something or someone other than yourself
Typical targets: processes, external entities, people

Tampering
Property violated: integrity
Meaning: modifying something on disk, on a network, or in memory
Typical targets: data stores, data flows, processes

Repudiation
Property violated: non-repudiation
Meaning: claiming you did not do something, or were not responsible for it
Typical targets: processes

Information disclosure
Property violated: confidentiality
Meaning: giving information to someone who is not authorized to see it
Typical targets: processes, data stores, data flows

Denial of service
Property violated: availability
Meaning: absorbing the resources needed to provide a service
Typical targets: processes, data stores, data flows

Elevation of privilege
Property violated: authorization
Meaning: allowing someone to do something they are not authorized to do
Typical targets: processes

----------------------------------------

THREATS IN DETAIL

Spoofing threats
Spoofing has three subcategories:
1. Spoofing a process or file on the same machine
2. Spoofing a machine (can act as a mediator, or steal machine authentication)
3. Spoofing a person

Tampering threats
1. Tampering with files
2. Tampering with memory
3. Tampering with a network

Repudiation threats
Repudiation differs from the other threats because it often appears at the business layer.
1. Attacking the logs
2. Repudiating an action

Information disclosure threats
1. Information disclosure from a process
2. Information disclosure from a data store
3. Information disclosure from a data flow

Denial-of-service threats
By duration, there are two types:
1. Lasts only while the attacker is attacking
2. Persists, and can remain until the system reboots

By effort, there are two types:
1. Amplified attack: small effort, great impact
2. Unamplified attack: the opposite [check against the book]

Denial of service can target:
1. A process
2. A data store
3. A data flow

Elevation of privilege threats
1. Elevating privileges by corrupting a process
2. Elevating privileges through authorization failures

----------------------------------------

STRIDE VARIANTS

STRIDE-per-element
Not every threat applies to every element in a DFD.

Element            S   T   R   I   D   E
External entity    x       x
Process            x   x   x   x   x   x
Data flow              x       x   x
Data store             x   ?   x   x

Two weaknesses:
1. Similar issues keep coming up.
2. It does not cover all issues.

STRIDE-per-interaction
This variant looks at the origin, the destination and the interaction, and enumerates threats from those. It is the more practical and easier approach.
STRIDE-per-interaction (verified against the book)
#	Element	Interaction	S	T	R	I	D	E	
1	Process	Outbound data flow to a data store	✓			✓			
2	Process	Sends output to another process	✓		✓	✓	✓	✓	
3	Process	Sends output to an external interactor (code)	✓		✓	✓	✓		
4	Process	Sends output to an external interactor (human)			✓				
5	Process	Inbound data flow from a data store	✓	✓			✓	✓	
6	Process	Inbound data flow from a process	✓		✓		✓	✓	
7	Process	Inbound data flow from an external interactor	✓				✓	✓	
8	Data flow	Crosses a machine boundary		✓		✓	✓		
9	Data store	Process has outbound data flow to the data store		✓	✓	✓	✓		
10	Data store	Process has inbound data flow from the data store			✓	✓	✓		
11	External interactor	Passes input to a process	✓		✓	✓			
12	External interactor	Gets input from a process	✓						
Using this approach, we should be able to find threats through our mitigations, which helps us do well at finding threats.

DESIST
A variant of STRIDE. DESIST stands for Dispute, Elevation of privilege, Spoofing, Information disclosure, Service denial, and Tampering.

----------------------------------------

CHECKING THAT THE WORK IS DONE

To check that we found enough threats, compare the results against STRIDE-per-element. If there is not at least one threat for each applicable category, the process is not complete.
