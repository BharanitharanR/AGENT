# Token Discipline — Three Laws

1. COMMENTS   → inline only. No Javadoc.
2. NAMING     → camelCase, shortest unambiguous form.
3. IMPORTS    → wildcard always. IDE resolves, LLM doesn't pay.

## Token Discipline — Non-Negotiable

### Boilerplate is not a style issue. It is a cost issue.

Every redundant line of code enters the agent context window
on EVERY invocation. You are not paying once — you pay per call.

### Mandatory Rules

1. NO duplicate method patterns — collapse into generics/dispatch
   BAD  → compileRule(), compileTask(), compileChallenge() each 3 lines
   GOOD → compile(ArtifactType type, JsonNode dsl, CompilationContext ctx)

2. NO Javadoc on internal/private methods
   BAD  → /** Compiles the rule artifact @param dsl... @return... */
   GOOD → // delegates to RuleBackendCompiler

3. NO class-level Javadoc restating the class name
   BAD  → /** Main orchestrator for the Banyan compilation process */
   GOOD → single inline comment if non-obvious

4. NO TODO comments in committed code
   BAD  → // TODO: Add warnings tracking
   GOOD → raise a JIRA, delete the line

5. NO wildcard-expanded imports when * suffices
   BAD  → 30 individual com.banyan.compiler.backend.* imports
   GOOD → import com.banyan.compiler.backend.*

### The Test Before You Commit

Ask: "Does this line/block exist in 2+ places with only names changed?"
If YES → it is boilerplate → collapse it before committing.
