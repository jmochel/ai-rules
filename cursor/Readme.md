# Cursor Rules Format

## TBD

* Basic Approach
* Model
* Design
* Architecture
* Coding (Defaults to Java)
    * logging
        * levels
    * error handling
        * Operator result pattern
        * Exception handling
    * testing
        * bdd
        * 
* Dropwizard




## MDC (Markdown with Code) Format

An `.mdc` file is a Markdown file with YAML frontmatter, designed to encapsulate both metadata and rule content. This structure allows Cursor to process and apply rules effectively within your project.​

More human-readable and maintainable for complex rules
Better for rules that need extensive context or documentation
Combines natural language documentation with code examples

Each rule is defined in a Markdown Container (.mdc) file with the following structural components:



```markdown
---
description: Enforce consistent logging practices
globs: "**/*.js"
---

- Use structured logging with Winston.
- Avoid using `console.log`; prefer `logger.info` or `logger.error`.
- Ensure all error logs include stack traces.

```

In this example:​

The description provides a brief overview of the rule's purpose.
The globs field specifies the file patterns the rule applies to.

The body contains the actionable guidelines or instructions.​


Rules can be implemented at multiple levels of specificity:

File-Type Specific Rules: Apply to particular extensions or file patterns

Globs: **/*.tsx

Directory-Scoped Rules: Target specific architectural components

Globs: src/components/**/*

Pattern-Based Rules: Apply to files matching naming conventions

Globs: **/*{.test,.spec}.{ts,tsx}

Universal Rules: Apply globally when no specific rule takes precedence

Globs: **/*.*



Better for:

* Complex rules that need detailed explanations
* Rules that require multiple examples
* Documentation-heavy rules
* Rules that benefit from rich text formatting
* Can include:
    * Detailed descriptions
    * Multiple code examples
    Step-by-step instructions
(   * Visual formatting (headings, lists, etc.)


## YAML Format

Structured, hierarchical format that's well-suited for static analysis rules
Uses a clear, declarative syntax with key-value pairs
Supports pattern-based matching with specific fields like:

id: Unique identifier for the rule
pattern: The code pattern to match
message: The warning/error message
severity: Level of importance (WARNING, ERROR, etc.)
tags: Categorization labels

Better for technical rules that require precise pattern matching
Easier to parse and process programmatically
Supports metadata like descriptions, justifications, and recommendations
Can include scoped matching and process guidelines


The choice between YAML and MDC depends on the nature of the rule:
Use YAML for simple, pattern-based rules that need precise matching
Use MDC for complex rules that require detailed documentation, multiple examples, or extensive context
Both formats can be used to enforce cursor rules, but they serve different purposes and have different strengths. YAML is more structured and machine-friendly, while MDC is more flexible and human-friendly.


# Specific Rule Files

## persona-and-approach.mdc

Derived from [getting-better-results-from-cursor-ai](https://medium.com/@aashari/getting-better-results-from-cursor-ai-with-simple-rules-cbc87346ad88#id_token=eyJhbGciOiJSUzI1NiIsImtpZCI6ImM3ZTA0NDY1NjQ5ZmZhNjA2NTU3NjUwYzdlNjVmMGE4N2FlMDBmZTgiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJodHRwczovL2FjY291bnRzLmdvb2dsZS5jb20iLCJhenAiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJhdWQiOiIyMTYyOTYwMzU4MzQtazFrNnFlMDYwczJ0cDJhMmphbTRsamRjbXMwMHN0dGcuYXBwcy5nb29nbGV1c2VyY29udGVudC5jb20iLCJzdWIiOiIxMDIxNTM3NzExMzQ1Mjg5MzMxODkiLCJoZCI6InNhbHRhdGlvbnMub3JnIiwiZW1haWwiOiJqbW9jaGVsQHNhbHRhdGlvbnMub3JnIiwiZW1haWxfdmVyaWZpZWQiOnRydWUsIm5iZiI6MTc0NDQ2OTQ2OSwibmFtZSI6IkppbSBNb2NoZWwiLCJwaWN0dXJlIjoiaHR0cHM6Ly9saDMuZ29vZ2xldXNlcmNvbnRlbnQuY29tL2EvQUNnOG9jS1RpZG9ScDc3azVOWENMalFlRmt6RnBXREV3S2Q4VFQyRXNVZWpiNlRmQk01U3h3PXM5Ni1jIiwiZ2l2ZW5fbmFtZSI6IkppbSIsImZhbWlseV9uYW1lIjoiTW9jaGVsIiwiaWF0IjoxNzQ0NDY5NzY5LCJleHAiOjE3NDQ0NzMzNjksImp0aSI6ImE1Mzg0YTg5MmFhNTRlMGY0YTczNmRjMzA3NzBmMDNkN2NhN2QyODkifQ.G7qI7iZd3bvindYE4xC1wRMJuiHR7En4M1-32ND4DaAp7_PY_BDee3kFlwxsSPzX2eKBhfPLZUbx8vXcB1ymkhntjHcunFoliqvwDuqCBPq7Nv45-kmDPIAuauS_gZLL7HxaA360gy6gSBGs_NntNJQle4_67TGLd0s37H9ainppmRSmySafvR_Y3My_7ytS-lMZp6GuAkm2NwPCIvyu27ccNhIPs7nqBMbuBwpibOSl-Th4u_vDlH3Dz9jfttvydCYmY4BYGjdBNC4dxuHnaoQA8YsRFDohIzGNNGSPhT4x2dFziWt8OeEJe1d93h8lUKwnlz_CqKP3MNOzZYtOfQ)

### User Rules Setting (Global Rules)

* Open the Command Palette in Cursor AI: Cmd + Shift + P (macOS) or Ctrl + Shift + P (Windows/Linux).
* Type Cursor Settings: Configure User Rules and select it.
* This will open your global rules configuration interface.
* Copy the entire content of the core.md file.
* Paste the copied content into the User Rules configuration area.
* Save the settings.

Note: These rules will now apply globally to all your projects opened in Cursor, unless overridden by a project-specific .cursorrules file.



## Using refresh.mdc (When Something is Still Broken)

Use this template when you need the AI to re-diagnose and fix an issue that wasn't resolved previously.

* Copy: Select and copy the entire content of the refresh.md file.
* Modify: Locate the first line: User Query: {my query}.
* Replace Placeholder: Replace the placeholder {my query} with a specific and concise description of the problem you are still facing.
* Example: User Query: the login API call still returns a 403 error after applying the header changes
* Paste: Paste the entire modified content (with your specific query) directly into the Cursor AI chat input field and send it.


## Using request.mdc (For New Features or Changes)

Use this template when you want the AI to implement a new feature, refactor existing code, or perform a specific modification task.

* Copy: Select and copy the entire content of the request.md file.
* Modify: Locate the first line: User Request: {my request}.
* Replace Placeholder: Replace the placeholder {my request} with a clear and specific description of the task you want the AI to perform.
* Example: User Request: Add a confirmation modal before deleting an item from the list
* Example: User Request: Refactor the data fetching logic in UserProfile.jsto use the newuseQuery hook
* Paste: Paste the entire modified content (with your specific request) directly into the Cursor AI chat input field and send it.
