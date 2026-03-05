# ADR-001: Use Microservices Architecture over Monolith

## Status
Accepted

## Date
04-Mar-2026

## Context
MathVerse Phase 1 is a basic calculator - a feature set that
could trivially fit in a single monolithic application.
However, the stated goal is to master all SDLC phases using
production-grade patterns. Future phases will add an AI service
(Python/FastAPI), a formula engine, and a user management system.

## Decision
We will use a microservices architecture from Day 1, starting with:
- calc-service (Java Spring Boot) - arithmetic logic
- API Gateway (Spring Cloud Gateway) - single entry point

Additional services (ai-service, user-service) will be added
in future phases as separate deployable units.

## Rationale
1. LEARNING GOAL: Microservices expose real distributed systems
challenges (network failures, service discovery, distributed
tracing) that a monolith hides. Experiencing these firsthand
is the primary goal.

2. FUTURE-PROOFING: The AI service MUST be Python (Hugging Face
ecosystem). A monolith in Java cannot cleanly incorporate
Python services. Microservices allow ployglot architecture.

3. INDEPENDENT SCALING: In Phase 4, the calc-service may need
to scale differently than the AI service. Microservices
make this trivial; a monolith makes it impossible.

## Consequences
### Positive
- Each service can be developed, deployed, and scaled independently
- Technology-appropriate choices per service (Java for business
  logic, Python for ML)
- Failure in one service doesn't cascade to all services

### Negative / Risks
- Higher initial complexity vs. a monolith
- Requires API Gateway, service discovery setup
- Network latency between services (mitigated by Redis caching)
- More infrastructure to manage (mitigated by Docker/K8s later)

## Alternatives Considered
- **Monolith + Python subprocess:** Rejected - fragile, not
  production-appropriate, poor separation of concerns
- **Full monolith in Java:** Rejected - cannot cleanly host
  Hugging Face Python models; limits learning objectives