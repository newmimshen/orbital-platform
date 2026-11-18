# ORBITAL — Project Requirements & Prerequisites

> **Document status:** Living document  
> **Last reviewed:** 2026-11-18  
> **Purpose:** Preserve agreed project requirements, learning prerequisites, technical decisions, and their rationale. Update this document whenever an important project decision is made or changed.

## 1. Document maintenance rules

1. Do not leave important project decisions only in chat conversations. Record approved decisions here or in a dedicated Architecture Decision Record (ADR).
2. Clearly distinguish **approved decisions** from **proposals**, **assumptions**, and **open questions**.
3. Do not silently turn a proposal into a requirement. The founder must review and approve consequential product and architecture decisions.
4. When a decision changes, update this document and, when useful, add an ADR explaining the context, alternatives, trade-offs, and consequences.
5. Keep this document current as the project evolves. Update the review date whenever substantive changes are made.
6. Never commit credentials, API keys, access tokens, passwords, private keys, or other secrets.

## 2. Product direction

ORBITAL is a long-term product and simulation project exploring the management of a privately operated interplanetary industrial network.

The intended company may:
- Operate a primary space station and facilities on celestial bodies.
- Explore, extract, process, store, and transport resources.
- Manage facilities, equipment, fleets, personnel, missions, inventory, and logistics.
- Retain resources for internal operations or sell them to customers and markets.
- Grow progressively through investment, revenue, and commercial or government contracts while remaining privately owned.
- Evaluate expansion opportunities using operational, scientific, logistical, and financial information.

The initial scope is not yet fixed. Candidate domains in the repository README are areas for product discovery, not a commitment to build all of them in the first release.

## 3. Product and domain requirements

### 3.1 Separate celestial bodies from facilities
A celestial body (for example, the Moon) is not the same entity as a facility located on it. One body may host multiple facilities, potentially owned or operated by different organizations.

The domain model should therefore distinguish:
- CelestialBody: a planet, moon, asteroid, dwarf planet, or another supported body type.
- Facility: a station, base, mine, factory, warehouse, or other installation with its own ownership, location, capacity, status, workforce, inventory, and capabilities as applicable.

### 3.2 Scientific provenance and uncertainty
The system must distinguish:
- Established or observed scientific data.
- Estimates derived from measurements, models, or published assessments.
- Uncertain hypotheses.
- Explicit simulation assumptions.

Where practical, preserve source provenance, confidence, units, and source date/version. Fictional or gameplay assumptions must not be represented as established scientific facts.

### 3.3 Explainable operational and financial decisions
Business recommendations should expose relevant assumptions and costs. Examples include comparing the economics of extracting a resource from different bodies, processing it at different facilities, transporting it, and selling it to different markets.

A basic financial principle is:

    Profit = Revenue - Total Cost

The full cost model may later include extraction, processing, storage, transport, labor, energy, maintenance, depreciation, risk, and other relevant costs. These details require further product and simulation design.

### 3.4 Human approval for consequential actions
AI-assisted capabilities may analyze information and recommend actions. Consequential company actions—such as establishing a facility or committing resources—must require explicit human authorization.

### 3.5 Time-dependent space logistics
Distances and transfer opportunities vary over time. A straight-line distance alone is not sufficient to model a mission's feasibility or economics. Future logistics modeling may need orbital positions, transfer windows, travel time, energy/propellant, payload capacity, and mission costs. The required fidelity is an open design question.

## 4. Approved decisions

The following decisions are approved as of the date above:

| Area | Decision | Rationale / boundary |
|---|---|---|
| Learning and implementation path | Begin with Python and FastAPI, learning the foundations systematically while building toward ORBITAL. | The founder selected the Python + FastAPI learning path rather than jumping straight into implementation or first building a framework comparison. |
| Project documentation | Keep important requirements and decisions in version-controlled repository documentation; update the relevant documents when decisions change. | Prevents important project context from being lost in chat and provides a durable project record. |
| Domain modeling | Model celestial bodies separately from facilities located on them. | Supports multiple facilities, ownership, operators, and competitors on the same body. |
| Initial architecture direction | Start with a modular monolith in one repository. | Keep module boundaries clear without introducing distributed-system complexity prematurely. |
| Project decision authority | The human founder owns and approves product and consequential architecture decisions. | AI assistance provides analysis and implementation support, not unilateral project authority. |

## 5. Technical stack: current direction and proposals

Only the Python + FastAPI learning/implementation direction is approved so far. The other items below are candidates and must not be treated as final until reviewed and approved.

| Area | Candidate | Status |
|---|---|---|
| Backend language | Python | Approved direction |
| Backend framework | FastAPI | Approved direction |
| Database | PostgreSQL | Proposed; pending decision |
| ORM | SQLAlchemy 2.x | Proposed; pending decision |
| Data validation / schemas | Pydantic | Proposed; pending decision |
| Database migrations | Alembic | Proposed; pending decision |
| Backend testing | Pytest | Proposed; pending decision |
| Frontend | React + TypeScript | Proposed; pending decision |
| Frontend framework | Next.js (with React) | Proposed; pending decision; compare with React + Vite if the product is primarily an authenticated dashboard |
| Styling | Tailwind CSS | Proposed; pending decision |
| API style | REST / JSON | Proposed; pending decision |
| Local development / deployment packaging | Docker | Proposed; introduce when useful |
| Background jobs / message broker | Not selected | Defer until a concrete use case exists; do not add Redis or a task queue prematurely |

### Architecture constraints
- Begin as a modular monolith in the existing orbital-platform repository.
- Define module responsibilities and boundaries before considering service extraction.
- Do not split repositories or introduce microservices without a demonstrated technical, organizational, or deployment need.
- Prefer explicit, testable domain rules and clear interfaces.
- Add infrastructure only when a current requirement justifies it.

## 6. Learning and implementation prerequisites

The founder has prior experience with backend development, PHP frameworks, Python frameworks, and frontend technologies. The learning path should therefore rebuild or verify foundations without unnecessarily repeating material already understood.

### Python and backend foundations to verify
- Python syntax, data types, collections, control flow, functions, modules, and packages.
- Classes, objects, composition, and type hints.
- Exceptions, context managers, and practical error handling.
- Virtual environments, dependency management, and project structure.
- HTTP fundamentals, request/response lifecycle, status codes, headers, and JSON.
- REST API design, validation, authentication, authorization, and security fundamentals.
- Async programming: what async / await mean, when they help, and their limitations.
- Automated testing, test isolation, and debugging.

### FastAPI foundations
- Routing and dependency injection.
- Pydantic request and response schemas.
- Application configuration and environment variables.
- Error handling and API documentation.
- Authentication and authorization design.
- Database integration and transaction boundaries.
- Testing endpoints and dependencies.

### Database foundations
- Relational modeling, keys, constraints, indexes, and normalization.
- SQL queries, joins, aggregation, and transactions.
- PostgreSQL-specific capabilities when a concrete requirement needs them.
- ORM trade-offs: understand the SQL and data model rather than relying blindly on ORM abstractions.
- Schema migrations and safe evolution of existing data.

### Engineering workflow
- Git and GitHub: branches, commits, reviews, and change history.
- Automated tests and code quality checks.
- Environment-based configuration and secret handling.
- Reproducible local development.
- Documentation of important decisions and trade-offs.

These are a learning checklist, not a requirement to finish every topic before writing useful project code. Learn each concept when it becomes relevant to a small, testable project increment.

## 7. Working method

For each significant feature or technical choice:

1. State the problem and the intended outcome.
2. Identify constraints and relevant domain rules.
3. Explore reasonable alternatives.
4. Explain trade-offs, risks, and maintenance implications.
5. Get the founder's decision or approval.
6. Record the approved decision in this document or a dedicated ADR.
7. Implement a small, reviewable increment.
8. Test it, review the result, and update the documentation.

The founder should understand the important decisions and be able to explain why they were made. AI assistance should guide, review, and accelerate the work without obscuring the reasoning.

## 8. Open questions

Keep unresolved matters here until they are decided. Add or remove items as discovery progresses.

- What is the smallest coherent and demonstrable first release (MVP)?
- Which celestial bodies, facilities, resources, and business processes belong in the first simulation scenario?
- How scientifically detailed should orbital mechanics and transfer planning be in the first version?
- Is the frontend primarily an authenticated management dashboard, or will it also include substantial public-facing pages? This affects the choice between Next.js and a simpler React + Vite setup.
- Confirm PostgreSQL, SQLAlchemy, Pydantic, Alembic, Pytest, and the API approach.
- Define the first users, permissions, and organization/competitor model.
- Define how real-world data sources will be selected, cited, versioned, and updated.

## 9. Change log

| Date | Change |
|---|---|
| 2026-11-18 | Created the initial living requirements and prerequisites document. Recorded the approved Python + FastAPI learning direction, documentation maintenance rule, domain separation principle, modular-monolith direction, and founder decision authority. Marked the remaining technology stack as proposed rather than final. |
