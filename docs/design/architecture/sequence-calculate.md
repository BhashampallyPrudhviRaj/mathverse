sequenceDiagram
    autonumber

    actor Student
    participant FE as React Frontend
    participant GW as API Gateway
    participant CS as calc-service
    participant RC as Redis Cache
    participant DB as PostgreSQL

    Student->>FE: Enters A=10, B=5, clicks "/ Divide"

    FE->>FE: Validates inputs (non-empty, numeric)

    FE->>GW: POST /api/v1/calculate
    Note over FE, GW: Body: {a: 10, b:5, operation: "DIVIDE"}

    GW->>GW: Rate limit check, auth check (Phase 2)

    GW->>CS: Forward request

    CS->>CS: Validate inputs (@Valid annotation)

    CS->>RC: Check cache: key="DIVIDE:10:5"
    RC-->>CS: Cache MISS (first time)

    CS->>CS: Execute 10 / 5 = 2.0

    CS->>RC: Store result in cache (TTL: 10 min)
    CS->>DB: Persist calculation record (Phase 2+)

    CS-->>GW: HTTP 200 { result: 2.0 }
    GW-->>FE: HTTP 200 { result: 2.0 }

    FE->>FE: Display "A / B = 2.0"
    FE-->>Student: Shows result instantly

    Note over Student, DB: Second request for same A=10,B=5,DIVIDE:
    CS->>RC: Cache HIT -> returns 2.0 immediately (no recalculation)