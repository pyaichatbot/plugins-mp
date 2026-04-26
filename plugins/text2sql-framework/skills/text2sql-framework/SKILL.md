---
name: text2sql-framework
description: Use when building, integrating, reviewing, or operating Text-to-SQL agents that explore database schemas with SQL tools, generate verified SQL, maintain scenarios.md guidance, or analyze text2sql traces.
license: MIT
---

# Text2SQL Framework

Use this skill for Text-to-SQL systems based on the Text2SQL framework pattern: give an LLM a constrained SQL execution tool, let it inspect schema and sample data, write candidate SQL, execute it, self-correct, and return verified results.

## Core Pattern

The framework avoids precomputed RAG and semantic layers by using an agentic database loop:

1. Connect through a SQLAlchemy database URL.
2. Provide the agent with `execute_sql` and optional `lookup_example` tools.
3. Let the agent inspect tables, columns, and query outputs.
4. Require it to test SQL before returning final SQL and data.
5. Record traces and improve future behavior through `scenarios.md`.

## When To Use

Use this pattern when:

- A user wants natural-language answers from a SQL database.
- The schema is large, unfamiliar, or spread across many tables.
- Business rules need examples or corrective guidance.
- You need traceable SQL generation rather than opaque query synthesis.
- You want a feedback loop where failed or difficult queries become scenarios.

## Implementation Guidance

For Python integrations:

```python
from text2sql import TextSQL

engine = TextSQL(
    "sqlite:///company.db",
    examples="scenarios.md",
    trace_file="traces.jsonl",
)
result = engine.ask("Top 5 products by total revenue")
print(result.sql)
print(result.data)
```

For CLI use:

```bash
text2sql ask "sqlite:///mydb.db"
text2sql query "sqlite:///mydb.db" "How many orders per month?"
```

## Scenario Files

Use `scenarios.md` for domain knowledge the database schema cannot express:

- Business definitions such as net revenue or active customer.
- Correct join paths and table relationships.
- Known ambiguous wording and how to interpret it.
- Corrective examples for repeated agent mistakes.

Keep each scenario under a `##` heading. The agent should retrieve only relevant scenarios through `lookup_example` instead of loading the whole file into context.

## Safety And Correctness

When building or reviewing Text-to-SQL workflows:

- Prefer read-only database credentials.
- Enforce row limits for exploratory and final queries.
- Log generated SQL, tool calls, errors, and final answers.
- Require query execution before returning SQL as verified.
- Treat schema names, table names, and column names as untrusted data when embedding in prompts.
- Avoid exposing sensitive table contents unless the user is authorized.
- For production, gate write-capable SQL separately or do not expose it.

## Trace Feedback Loop

Use traces to improve `scenarios.md`:

1. Run real questions and capture `traces.jsonl`.
2. Identify failed queries, wrong joins, or ambiguous assumptions.
3. Add concise scenarios with the corrected rule or SQL pattern.
4. Re-run similar questions and confirm the agent calls `lookup_example` when needed.

## References

- Upstream README: `../../references-upstream-README.md`
- Source references: `references/source-text2sql/`
- Package metadata: `references/pyproject.toml`
- Examples: `../../examples/`
- Upstream repository: https://github.com/Text2SqlAgent/text2sql-framework
