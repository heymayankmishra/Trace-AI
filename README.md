# TRACEAI --- A Trust Layer for AI-Generated Code

> **AI said it. TraceAI asks: Where is the evidence?**

TraceAI is an explainable AI reliability tool designed to verify whether
claims made about AI-generated code are supported by observable evidence
in the code.

## Problem Statement

AI coding assistants can generate code and confidently explain what that
code is supposed to do. However, those explanations can be incorrect,
overconfident, or inconsistent with the actual code.

TraceAI addresses this gap by connecting:

**AI Claim → Code Evidence → Verification Status**

## Proposed Solution

TraceAI analyzes submitted code and an AI-generated explanation or
claim. It identifies the programming language, checks observable code
properties, extracts relevant claims, and compares those claims against
available evidence.

TraceAI does not claim to prove that code is universally correct or
secure. It reports what the available evidence supports and highlights
uncertainty.

## Core Workflow

``` text
AI-Generated Code + AI Claim
            ↓
     Language Detection
            ↓
       Code Analysis
            ↓
       Claim Extraction
            ↓
    Evidence Verification
            ↓
 ┌──────────┼───────────┐
 ↓          ↓           ↓
SUPPORTED  NOT        REQUIRES
           SUPPORTED   REVIEW
```

## Verification States

  -----------------------------------------------------------------------
  Status                              Meaning
  ----------------------------------- -----------------------------------
  ✅ SUPPORTED                        Available evidence supports the
                                      specific claim.

  ❌ NOT SUPPORTED                    Evidence contradicts the claim or a
                                      clear mismatch was detected.

  ⚠️ REQUIRES REVIEW                  Available evidence is insufficient
                                      to confidently verify the claim.
  -----------------------------------------------------------------------

**Important:** "No issue detected" does not mean "perfectly correct."

## Key Features

-   Claim-to-evidence verification
-   Multi-language code analysis
-   Language mismatch detection
-   Output and behavior claim checking
-   Syntax and pattern analysis
-   Explainable evidence-based results
-   Explicit uncertainty and human review

The prototype is designed for languages including C, C++, C#, Java,
Python, JavaScript, TypeScript, Go, Rust, PHP, Ruby, Kotlin, Swift,
Dart, SQL, HTML, CSS, R, Scala, Lua, Bash, Perl, Haskell, and MATLAB.

## Example

### Correct claim

``` python
print("Hello World")
```

Claim:

``` text
This Python code is correct and will print "Hello World".
```

Result:

``` text
✓ AI CLAIM SUPPORTED
```

### Language mismatch

``` python
print("Hello World")
```

Claim:

``` text
This C# code is correct and will print "Hello World".
```

Result:

``` text
❌ AI CLAIM NOT SUPPORTED
```

Evidence: the submitted code is Python while the claim identifies it as
C#.

## What Makes TraceAI Different?

  Tool                  Primary Purpose
  --------------------- --------------------------------
  AI Coding Assistant   Generate and explain code
  Compiler              Check whether code can compile
  Static Analyzer       Detect specific code issues
  TraceAI               Connect AI claims to evidence

### USP

> **Claim-to-evidence verification for AI-generated code.**

TraceAI is not intended to be another LLM wrapper that simply asks an AI
whether its own answer is correct. In a production system, AI can assist
with claim extraction and interpretation, while independent evidence can
come from parsers, compilers, tests, runtime behavior, static analysis,
and security tools.

## Technical Approach

### Current Prototype

-   HTML
-   CSS
-   JavaScript
-   Language detection
-   Language-specific heuristics
-   Rule-based claim verification
-   Observable output comparison

### Future Production Direction

-   AST and language-aware parsing
-   Compiler/interpreter diagnostics
-   Sandboxed execution
-   Static analysis and security scanners
-   LLM-assisted claim extraction
-   Code-region evidence mapping
-   Test execution
-   IDE and GitHub integration

## Responsible Design

TraceAI does **not** claim to:

-   Guarantee complete code correctness
-   Guarantee software security
-   Replace developers
-   Replace compilers or security tools
-   Detect every possible bug
-   Prove the absence of vulnerabilities

For ambiguous or insufficiently supported claims, TraceAI should return:

``` text
⚠️ REQUIRES REVIEW
```

rather than creating false confidence.

## Reliability Evaluation

A production version can be evaluated with a labeled test set covering:

-   Correct code + correct claim
-   Correct code + incorrect claim
-   Incorrect code + correct-looking claim
-   Language mismatches
-   Incorrect output claims
-   Syntax errors
-   Behavioral claims
-   Security claims
-   Ambiguous claims
-   Edge cases

Useful metrics include verification accuracy, false positives, false
negatives, language coverage, evidence quality, claim extraction
accuracy, and review rate.

## Expected Impact

TraceAI encourages a safer AI-assisted development workflow:

``` text
Generate → Inspect → Verify → Understand → Use
```

instead of:

``` text
Generate → Trust
```

Potential users include students, developers, educators, software teams,
and developer-tool platforms.

## Future Scope

-   AST-level semantic analysis
-   Cross-file dependency analysis
-   Sandboxed runtime verification
-   Automated test generation
-   Security scanner integration
-   Dependency analysis
-   VS Code extension
-   GitHub pull-request verification
-   CI/CD integration
-   Evidence provenance
-   Multi-model comparison
-   Human review workflows

## Project Structure

``` text
TraceAI/
├── frontend/
├── backend/
├── analyzer/
├── examples/
├── assets/
│   └── traceai-logo.png
└── README.md
```

## Getting Started

Clone the repository:

``` bash
git clone <repository-url>
cd TraceAI
```

For the current frontend prototype, open:

``` text
frontend/index.html
```

in a browser, enter code and an AI claim, then select **Analyze**.

## Suggested Demo Tests

### Test 1 --- Supported

``` text
Code: print("Hello World")
Claim: This Python code is correct and will print "Hello World".
Expected: SUPPORTED
```

### Test 2 --- Language mismatch

``` text
Code: print("Hello World")
Claim: This C# code is correct and will print "Hello World".
Expected: NOT SUPPORTED
```

### Test 3 --- Wrong output

``` text
Code: print("Hello")
Claim: This Python code will print "Hello World".
Expected: NOT SUPPORTED
```

### Test 4 --- Uncertain security claim

``` text
Claim: This code is completely secure.
Expected: REQUIRES REVIEW
```

## Project Context

**Project:** TraceAI --- A Trust Layer for AI-Generated Code\
**Event:** Logic League --- Ideathon\
**Organizer:** HackForge\
**Powered by:** HackerRank\
**Institution:** Galgotias University\
**Primary Category:** Explainable AI\
**Secondary Category:** AI Reliability

## Team TraceAI

-   Mayank Mishra
-   Sanuj Pal

## Core Message

> **AI can generate the code.**\
> **AI can explain the code.**\
> **But explanations should be checked against evidence.**\
> **TraceAI connects the claim to the evidence.**

## License

This project is currently a prototype created for educational and
ideathon purposes. A formal open-source license can be added when the
project is prepared for public distribution.
