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
