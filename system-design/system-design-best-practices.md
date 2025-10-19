# System Design Best Practices

1. Define the "Why" Problem & Scope

Before any diagramming or modeling:

- Identify the core problem you're solving
- Define who the users are and what they need
- Write a short problem statement and success criteria

*Note:* Project brief or requirements document

2. Map the System Conceptually (High-Level Design)

Now create visual models that help you and others understand the structure and behavior:

Common tools:

- **Use Case Diagram:** Defines interactions between users and the system
- **Context Diagram:** Shows your system as a black box with external entities
- **Data Flow Diagram (DFD):** Shows how data moves through the system
- **Entity-Relationship Diagram (ERD):** Models the database structure
- **System Architecture Diagram:** Shows backend, frontend, APIs, databases

*Note:* Visual understanding of how everything fits together

3. Model the Data (Database & Entities)

This is where your method already shines — creating ERDs or Data Models.

Best practice:

- Start with **conceptual models** (entities and relationships)
- Then **logical models** (table structure, keys, constraints)
- Then **physical models** (data types, indexes, normalization)

*Note:* Database schema or migration files (ex: SQL)

4. Define System Behavior (Flow, Logic & APIs)

After knowing what data exists, define how it moves and transforms

Tools:

- Sequence diagrams (how processes interact step-by-step)
- API design (OpenAPI/Swagger for endpoints)
- State diagrams (for UI or process logic)

*Note:* API contract or backend design spec.

5. Prototype

Create a minimal version to test the flow:

- Mock the UI with Figma or Framer
- Set up a backend skeletons (Nextjs)
- Test critical paths early

*Note:* Working prototype or proof-of-concept

6. Iterate — Feedback and Refinement

After the prototype:

- Get user feedback
- Update models and flows
- Improve performance, scalability, and usability

7. Typical Order (Best Practice Flow)

1. Problem definition & scope
2. Use cases / context diagram
3. DFD + ERD (your step!)
4. System architecture diagram
5. API design & sequence diagrams
6. Prototype (UI + backend)
7. Iterate and test
