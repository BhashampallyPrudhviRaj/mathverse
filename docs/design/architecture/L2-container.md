C4Container
    title MathVerse - Level 2: Container Diagram (All Phases)

    Person(student, "Student", "Browser or Mobile")

    System_Boundary(mathverse, "MathVerse Platform") {

        Container(frontend, "React Frontend", "React 18, Remix,\nTypeScript, Tailwind",
                 "Renders the calculator UI,\nhandles user interactions")

        Container(gateway, "API Gateway", "Spring Cloud Gateway",
                  "Single entry point - routes requests,\nhandles auth, rate limiting")

        Container(calc_svc, "calc-service", "Java 21, Spring Boot 3",
                  "Core arithmetic logic\n(+, -, *, /). Phase 1 focus.")

        Container(ai_svc, "ai-service", "Python, FastAPI",
                  "Handles natural language queries\nvia Hugging Face models. Phase 2.")

        ContainerDb(postgres, "PostgreSQL", "AWS RDS",
                    "Stores calculation history,\nuser data (Phase 2+)")

        ContainerDb(redis, "Redis Cache", "AWS ElastiCache",
                    "Caches frequent calculations,\nsession data")

        ContainerDb(mongodb, "MongoDB", "Atlas / AWS",
                    "Stores AI chat history,\nunstructured logs (Phase 2+)")
    }

    System_Ext(huggingface, "Hugging Face Hub", "Remote AI model inference")

    Rel(student, frontend, "Interacts via", "HTTPS")
    Rel(frontend, gateway, "API calls", "HTTPS/REST + JSON")
    Rel(gateway, calc_svc, "Routes /api/v1/calculate", "HTTP/REST")
    Rel(gateway, ai_svc, "Routes /api/v1/ai/chat", "HTTP/REST")
    Rel(calc_svc, postgres, "Reads/writes", "JDBC/JPA")
    Rel(calc_svc, redis, "Caches results", "Redis Protocol")
    Rel(ai_svc, mongodb, "Stores chat history", "MongoDB Driver")
    Rel(ai_svc, huggingface, "Model inference", "HTTPS")