# Workflow Rules

## Flow State Management

### Track Current State

Always know where you are in the workflow:

```
Current Phase: [discovery | planning | execution | validation]
Current Agent: [agent name]
Subtask: [if applicable]
```

### Flow Interruption Detection

When user provides input, check for:

**Errors:**
- Test failures
- Type errors
- Runtime exceptions
- Build failures
- "Error", "Failed", "Exception" in output

**New Information:**
- "Actually...", "I forgot to mention...", "Also..."
- New constraints or requirements
- Corrections to previous understanding
- Scope additions or changes

## Rollback Rules

| Trigger | Rollback To | Reason |
|---------|-------------|--------|
| Test failure (logic wrong) | discovery | Need to re-understand requirements |
| Type error | execution | Implementation issue, fix in place |
| Missing dependency | discovery | Gap in understanding |
| Build failure | execution | Code issue, fix in place |
| Requirements unclear | discovery | Need more facts |
| Plan inadequate | planning | Need to re-plan approach |
| New information from user | planning | Update plan, then resume execution |
| Scope change | discovery | Re-verify full understanding |
| "Actually..." or correction | planning | Adjust approach |

### Rollback Process

1. **DETECT** - Recognize error in user-provided output
2. **CLASSIFY** - Determine error type from table above
3. **ANNOUNCE** - Tell user: "Error detected. Rolling back to [agent] to [reason]."
4. **RESET** - Load the target agent with error context
5. **CONTINUE** - Agent investigates and flow resumes

### Example: Error Rollback

```
User: [provides test output with failures]

Response:
"Test failures detected in user permissions logic.
Rolling back to **discovery** to verify requirements.

Loading discovery agent with context:
- Error: Tests failing for provider access check
- Previous understanding: [what we thought]
- Need to verify: [specific gap]"
```

### Example: New Information

```
User: "Actually, providers should also have read access to archived clients."

Response:
"New requirement detected during execution.
Rolling back to **planning** to update the plan.

Loading planning agent with context:
- New requirement: Providers need read access to archived clients
- Current progress: [completed subtasks]
- Impact: Need to add test cases and implementation for archived client access

After planning updates, will resume execution."
```
