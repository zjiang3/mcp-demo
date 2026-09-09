# mcp-demo

Combine Oracle SQLcl MCP with GitHub Copilot to troubleshoot data issues quickly.

## Goal

Use Copilot to:
- understand a data problem in natural language,
- run targeted Oracle diagnostics through SQLcl MCP,
- and turn results into actionable fixes.

## Example MCP setup

Configure an Oracle SQLcl MCP server in your Copilot-compatible MCP config:

```json
{
  "mcpServers": {
    "oracle-sqlcl": {
      "command": "sql",
      "args": [
        "-cloudconfig",
        "/path/to/wallet.zip",
        "-user",
        "APP_USER",
        "-password",
        "${ORACLE_PASSWORD}",
        "-mcp"
      ]
    }
  }
}
```

## Troubleshooting workflow

1. Describe the issue to Copilot (example: “Orders are missing for yesterday in region APAC”).
2. Ask Copilot to use `oracle-sqlcl` MCP tools to:
   - verify row counts by date/region,
   - check recent ETL/update jobs,
   - compare source and target keys for gaps.
3. Review returned SQL results with Copilot and ask for:
   - likely root cause,
   - validation queries,
   - and safe remediation SQL.

## Prompt starter

> Use the `oracle-sqlcl` MCP server to investigate this data issue.  
> First produce read-only diagnostic SQL, explain each query, run them, summarize findings, then propose a minimal-risk fix and post-fix validation queries.
