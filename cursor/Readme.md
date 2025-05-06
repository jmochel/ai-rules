# Usage of Cursor

**⌘+k** - Localized generate code

**⌘+l** - Chat

* Add context with `@` or `/` . 
* Use **⌘+⏎** To add the entire code base as context
* **+** button to add files
* Code generated here will not be applied. If you like it, you can apply it with **⌘+i**
* **⌘+/** Switch models
* **@Web** To get up-to-date information from the web
* **@git** Stuff to reference your changes. For example `@` A commit and ask for AI to review. (Branch ?)
* **`@<link>`** So the AI visits the link before answering  


Tip: If you are starting on a new task remember to clear the chat history ny hitting / and then reset.

Tip: In chat, if you hit cmd+enter you use the entire codebase.

## `@Web`

With @Web, Cursor constructs a search query based on the query and the context you’ve provided, and searches the web to find relevant information as additional context. This is particularly useful for finding the most up-to-date information.

The @Web symbol is like having a research assistant built into Cursor. Here's how it works:

1. You give it a query and some context.
1. Cursor turns that into a web search.
1. It searches the internet for relevant info.
1. The search results get added to your query's context.

# Cursor Rules

Rules help with.

* Maintaining code consistency.
* Enhancing code quality.
* Vending unintended changes.
* Shepharding security concerns
* And making sure the code aligns with project requirements

# Keep in mind

* Style, Scope, Standard

## Pitfalls

* Overly general instructions
* Lack of Specificity
* Excessive complexity
* Conflicting rules


## Best practices

Do the following 

* Specified technology stack
* Coding standards and style
* Naming conventions
* Syntax and formatting
* Key conventions

# Cursor Rules Format

## Markdown-based Domain Configuration (MDC) Format Rules:

Introduced in cursor 0.45 , These target specific file patterns. Typically these rules are added to the prompt only an agent mode, chat and normal compose by default use only the global ones.

An `.mdc` file is a Markdown file with YAML frontmatter, designed to encapsulate both metadata and rule content. This structure allows Cursor to process and apply rules effectively within your project.

More human-readable and maintainable for complex rules
Better for rules that need extensive context or documentation
Combines natural language documentation with code examples

Each rule is defined in a Markdown Container (.mdc) file with the following structural components:


* These are written in markdown files (.md)
* They are more descriptive and narrative in nature
* They provide detailed explanations, examples, and context
* They are typically used for:
    * Architectural decisions
    * Design patterns
    * Coding standards
    * Best practices
    * Process guidelines


Examples .mdc Files:

Example 1

```Markdown
---
description: Enforce consistent logging practices
globs: "**/*.js"
---

- Use structured logging with Winston.
- Avoid using `console.log`; prefer `logger.info` or `logger.error`.
- Ensure all error logs include stack traces.
```

Example 2

```Markdown
# Exception Handling

## Overview
Exceptions are a critical part of any application's error handling strategy. They should be used judiciously and consistently throughout the codebase.

## Rules
- Only throw when necessary like within the repository layers, rest layers, or other external adapters
- Use checked exceptions for recoverable conditions
- Use unchecked exceptions for programming errors
```

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

`Globs: **/*.tsx`

Directory-Scoped Rules: Target specific architectural components

`Globs: src/components/**/*`

Pattern-Based Rules: Apply to files matching naming conventions

`Globs: **/*{.test,.spec}.{ts,tsx}`

Universal Rules: Apply globally when no specific rule takes precedence

`Globs: **/*.*`

### Tips

1. Reference architecture using `@ syntax`
```markdown
# Bad
- Controllers should use service objects for complex business logic...

# Good
- Follow service object patterns defined in @docs/architecture/services.md
- See implementation examples in @docs/examples/service_objects
```
2. Strategic Glob Patterns

Create focused, hierarchical patterns:

```markdown
# Too broad
Globs: **/*.rb

# Better
Globs:
  app/services/**/*.rb
  app/models/**/*.rb
  !app/models/legacy/**/*.rb  # Exclude legacy
```
3. Create Composable rule sets

```markdown
# .cursor/rules/base_ruby.mdc
Description: Base Ruby standards

# .cursor/rules/rails_controllers.mdc
@base_ruby.mdc
Description: Controller-specific rules
Globs: app/controllers/**/*.rb
```

4. Structure rules by domain

```text
.cursor/rules/
  ├── rails8.mdc
  ├── models/
  │   ├── active_record.mdc
  │   └── postgresql.mdc
  ├── controllers/
  │   ├── api.mdc
  │   └── web.mdc
  └── views/
      ├── erb.mdc
      └── components.mdc
```

# YAML Format Rules:

## YAML Format

Structured, hierarchical format that's well-suited for static analysis rules

* These are written in YAML files (.yaml or .yml)
* They are more structured and machine-readable
* They are typically used for:
    * Configuration rules
    * Validation rules
    * Automated checks
    * Tool-specific configurations
    * They follow a strict key-value format


Uses a clear, declarative syntax with key-value pairs
Supports pattern-based matching with specific fields like:


`id`: Unique identifier for the rule
`pattern`: The code pattern to match
`message`: The warning/error message
`severity`: Level of importance (WARNING, ERROR, etc.)
`tags`: Categorization labels

Better for technical rules that require precise pattern matching
Easier to parse and process programmatically
Supports metadata like descriptions, justifications, and recommendations
Can include scoped matching and process guidelines

## When to use

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

# TBD

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
        * naming
        * bdd
        * framework

* Dropwizard

Most common approaches tackle these

* Enforcing coding standards across a project.
* Improving AI-generated code quality by guiding style, formatting, and structure.
* Encouraging best practices for security, error handling, and performance.
* Reducing unnecessary code review churn by having the AI follow established team

Themes 

1. Functional programming and code structure
2. Consistent naming and formatting
3. Type safety
4. Prioritizing error handling and validation
5. Testing and automation as standard practice
6. Performance and optimization awareness
1. Git commit message standards
7. Some rules govern commit hygiene, ensuring a structured history. `Use Conventional Commits (feat:, fix:, docs:, chore:). Keep messages under 60 characters.`
2. Making up for AI shortcomings. Some rules guide how AI assistants should behave when generating code.
`Don't apologize for errors—fix them. If code is incomplete, add TODO comments instead.`
