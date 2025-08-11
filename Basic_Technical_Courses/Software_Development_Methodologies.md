# Software Development Methodologies

## **1. High-Level Overview**

* Software Development Models are frameworks that guide how software is planned, built, tested, and delivered.
* There are two main types:

  * Traditional (e.g., Waterfall) – sequential and structured.
  * Iterative/Agile – flexible and adaptive to change.
* Choice depends on project size, requirements stability, and team/customer collaboration needs.

---

## **2. Waterfall Model**

* Follows sequential phases: Requirements → Design → Implementation → Testing → Deployment → Maintenance.
* Pros:

  * Easy to understand and manage.
  * Clear deliverables at each stage.
* Cons:

  * Inflexible to changes once a phase is completed.
  * Late discovery of issues.
* Best for projects with fixed, well-understood requirements.

---

## **3. Agile Model**

* Is an iterative and incremental approach emphasizing flexibility, collaboration, and customer feedback.
* Values:

  * Individuals & interactions over processes & tools.
  * Working software over documentation.
  * Customer collaboration over contract negotiation.
  * Responding to change over following a plan.
* Pros:

  * Adapts to changing requirements.
  * Frequent delivery of usable software.
* Cons:

  * Requires strong team discipline.
  * Can lead to scope creep.
* Best for projects with evolving requirements.

---

## **4. Scrum**

* Is an Agile framework with time-boxed iterations called Sprints (1–4 weeks).
* Roles:

  * Product Owner defines priorities & backlog.
  * Scrum Master facilitates process and removes blockers.
  * Development Team delivers increments.
* Events include Sprint Planning, Daily Scrum, Sprint Review, Sprint Retrospective.
* Pros:

  * Clear structure and defined roles.
  * Fast feedback loop.
* Cons:

  * Can become rigid if misunderstood.
* Best for small-to-medium teams needing rapid delivery.

---

## **5. Kanban**

* Uses visual workflow management with columns like "To Do", "In Progress", and "Done".
* Focuses on continuous delivery and limits Work In Progress (WIP).
* Pros:

  * Simple and flexible.
  * Easy to visualize bottlenecks.
* Cons:

  * No fixed timeframes can make tracking progress harder.
* Best for teams with ongoing, continuous tasks.

---

## **6. Extreme Programming (XP)**

* Is an Agile methodology focused on high-quality code and customer satisfaction.
* Key practices include pair programming, test-first development, continuous integration, and refactoring.
* Pros:

  * High software quality.
  * Rapid response to changes.
* Cons:

  * Requires highly skilled, collaborative teams.
* Best for complex projects with high technical risk.

---

## **7. Test-Driven Development (TDD)**

* Involves writing tests first, then writing minimum code to pass the test, then refactoring.
* Follows the cycle: Red → Green → Refactor.
* Pros:

  * Ensures code correctness.
  * Improves design and maintainability.
* Cons:

  * Can slow initial development.
* Best for codebases where reliability is critical.

---

## **8. Behavior-Driven Development (BDD)**

* Is an extension of TDD focusing on user behavior and collaboration.
* Uses natural language specifications, typically in “Given-When-Then” format.
* Pros:

  * Improves communication between technical and non-technical stakeholders.
  * Aligns code with business needs.
* Cons:

  * Needs discipline to maintain tests and specifications.
* Best for projects with close stakeholder involvement.