# MathVerse Phase 1 - User Stories

## Epic: MATH-001 | Phase 1: Basic Calculator

---

### US-001: Enter Numeric Inputs
**As a** student using MathVerse,
**I want** to enter two numeric values (A and B) into input fields,
**So that** I can perform arithmetic operations on those values.

**Acceptance Criteria:**
- AC-001-01: Input fields accept integers and decimal numbers
             (e.g., 3, 3.14, -7, 0.001)
- AC-001-02: Input fields reject non-numeric characters
             (letters, symbols like @, #) and display the error:
             "Please enter a valid number"
- AC-001-03: Submitting with one or both fields empty displays:
             "Both fields are required"
- AC-001-04: Values outside the range [-1×10¹⁵, 1×10¹⁵] display:
             "Value exceeds allowed range"

**Priority:** P0 (Blocker - no other story works without this)
**Story Points:** 3

---

### US-002: Addition (A + B)
**As a** student,
**I want** to click an Add button and see the sum of A and B,
**So that** I can instantly verify addition results.

**Acceptance Criteria:**
- AC-002-01: Clicking "+ Add" computes and displays A + B
- AC-002-02: Result is accurate to 10 decimal places
- AC-002-03: Result displays in format: "A + B = [result]"
- AC-002-04: Result updates immediately (no page reload)

**Priority:** P0
**Story Points:** 2

---

### US-003: Subtraction (A - B)
**As a** student,
**I want** to click a Subtract button and see the difference of A and B,
**So that** I can instantly verify subtraction results.

**Acceptance Criteria:**
- AC-003-01: Clicking "- Subtract" computes and displays A - B
- AC-003-2: Negative results display correctly (e.g., -5.5)
- AC-003-03: Result displays in format: "A - B = [result]"
- AC-003-04: Result updates immediately (no page reload)

**Priority:** P0
**Story Points:** 2

---

### US-004: Multiplication (A * B)
**As a** student,
**I want** to click a Multiply button and see the product of A and B,
**So that** I can instantly verify multiplication results.

**Acceptance Criteria:**
- AC-004-01: Clicking "* Multiply" computes and displays A * B
- AC-004-02: Very large products display in scientific notation
             if result exceeds 10 digits (e.g., 1.23456789e+15)
- AC-004-03: Result displays in format: "A * B = [result]"
- AC-004-04: Result updates immediately (no page reload)

**Priority:** P0
**Story Points:** 2

---

### US-005: Division (A / B)
**As a** student,
**I want** to click on a Divide button and see the quotient of A divided by B,
**So that** I can instantly verify the division results.

**Acceptance Criteria:**
- AC-005-01: Clicking "/ Divide" computes and displays A / B
- AC-005-02: Result is accurate to 10 decimal places
- AC-005-03: Result displays in format: "A / B = [result]"
- AC-005-04: Result updates immediately (no page reload)

**Priority:** P0
**Story Points:** 2

---

### US-006: Division by Zero Error Handling
**As a** student,
**I want** to see a clear, friendly error when I divide by zero,
**So that** I understand why the operation failed and what to do next.

**Acceptance Criteria:**
- AC-006-01: When B = 0 and the user clicks Divide, the result area displays: 
             "Cannot divide by zero. Please enter a non-zero value for B."
- AC-006-02: The error message appears in the result area (not a popup)
- AC-006-03: Input fields retain their values after the error
             (user does not lose their inputs)
- AC-006-04: The backend returns HTTP 400 Bad Request (not 500)
             with JSON body: { "error": "Division by zero is undefined" }

**Priority:** P0
**Story Points:** 2

---

## Story Point Summary
|   Story   | Points | Priority |
|---------- |--------|----------|
|   US-001  |    3   |    P0    |
|   US-002  |    2   |    P0    |
|   US-003  |    2   |    P0    |
|   US-004  |    2   |    P0    |
|   US-005  |    2   |    P0    |
|   US-006  |    2   |    P0    |
| **Total** | **13** |    -     |