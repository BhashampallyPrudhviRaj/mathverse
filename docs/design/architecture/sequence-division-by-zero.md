sequenceDiagram
    autonumber

    actor Student
    participant FE as React Frontend
    participant GW as API Gateway
    participant CS as calc-service
    participant RC as Redis Cache
    
    Student->>FE: Enters A=10, B=0, clicks "/ Divide"

    FE->>FE: Validates inputs (non-empty, numeric)

    FE->>FE: Detects B=0 with operation=DIVIDE
    Note over FE: Frontend catches division by zero BEFORE API call

    FE-->>Student: Shows inline error immediately -
    Note over FE, Student: "Cannot divide by zero. Please enter a non-zero value for B."

    Note over FE, RC: Request STOPS here for frontend validation path.
    Note over FE, RC: Backend path shown below - for direct API calls (e.g. Postman, other clients)

    FE->>GW: POST /api/v1/calculate
    Note over FE, GW: Body: {a:10, b:0, operation: "DIVIDE"}

    GW->>GW: Rate limit check, auth check (Phase 2)

    GW->>CS: Forward request

    CS->>CS: Validate inputs (@Valid annotation)
    CS->>CS: Detects operation=DIVIDE and b=0 -> throws ArithmeticException

    Note over CS, RC: ERROR PATH - skip cache and DB entirely

    CS-->>GW: HTTP 400 Bad Request
    Note over CS, GW: {"error":"DIVISION_BY_ZERO", "message":"Cannot divide by zero."}

    GW-->>FE: HTTP 400 Bad Request (passed through unchanged)

    FE-->>Student: Displays error in result area