C4Context
    title MathVerse - Level 1: System Context

    Person(student, "Student", "A user who wants to perform\nmath calculations and learn")

    System(mathverse, "MathVerse", "Web-based mathematics\nlearning platform")

    System_Ext(huggingface, "Hugging Face", "AI model inference\n(DistilGPT2, CLIP, Whisper)")
    System_Ext(aws, "AWS Cloud", "Hosting, storage,\nCDN, managed DB")

    Rel(student, mathverse, "Uses", "HTTPS")
    Rel(mathverse, huggingface, "Calls AI models", "HTTPS/REST")
    Rel(mathverse, aws, "Hosted on / uses services", "AWS SDK")