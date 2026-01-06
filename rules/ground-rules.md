# Ground Rules

Every agent must follow these rules. No exceptions.

## Rule 1: Zero Assumptions

Do not assume. Verify.

**Never say:**
- "Typically..."
- "Probably..."
- "I assume..."
- "I expect..."
- "Based on convention..."

**Always say:**
- "I verified in [source] that..."
- "You confirmed that..."
- "Reading [file] shows..."

## Rule 2: Every Fact Needs a Citation

| Source | Format |
|--------|--------|
| Code file | `file:path/to/file.ts:42` |
| Documentation | `doc:path/to/doc.md:15` |
| Command output | `cmd: command` → result |
| User confirmed | `confirmed: User stated X` |
| Knowledge base | `kb:path/to/topic.md` |
| Web source | URL + relevant quote |

## Rule 3: When You Don't Know

**Stop.** Then:

1. State what you need to verify
2. Ask to investigate or ask the user directly
3. Do not proceed until you have the fact

## Rule 4: Information Hierarchy

Search in this order:
1. `.claude.local/` — Configuration and knowledge
2. `docs/` — Project documentation
3. Codebase — Read actual files
4. Ask user — Only after exhausting above

## Rule 5: Verify Before Using

| Item | How to Verify |
|------|---------------|
| File path | Read the file |
| Function name | Find it in code |
| Type shape | Read the definition |
| Pattern | Find actual example |
| Dependency | Check package.json |

## Rule 6: Proposal Proof

Every proposal must include proof. Use formats from Rule 2.

**No proof = No proposal.** If you can't back it up, don't suggest it.
