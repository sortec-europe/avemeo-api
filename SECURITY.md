# Security policy

We take the security of the Avemeo platform, the REST API and the AI connector seriously. Thank you for helping keep customers' screens and data safe.

## Reporting a vulnerability

**Please do not open a public GitHub issue for security problems.**

Send a report to **[avemeo@sortec.sk](mailto:avemeo@sortec.sk)** with the subject `Security: <short description>`. Include:

- what you found and where (cloud, URL, endpoint or tool name),
- steps to reproduce or a proof of concept,
- the impact you believe it has,
- how we can contact you.

What happens next:

1. We confirm receipt within **3 business days**.
2. We assess the report and, for platform or connector issues, forward it to the Avemeo development team.
3. We keep you informed about the fix and agree with you on public disclosure, if any.

Please give us reasonable time to fix the issue before publishing details, and do not access, modify or delete data that is not yours while testing.

## Scope

| In scope | Out of scope |
|---|---|
| Avemeo REST API on `ds.avemeo.com` and `cloud.tvstream.sk` | Social engineering of Avemeo, SORTEC or Telekom staff |
| Avemeo AI connector (MCP) at `mcp.avemeo.com` and `mcp.tvstream.sk` | Denial-of-service testing |
| Avemeo CMS web application and players | Issues in third-party AI assistants (report those to their vendors) |
| Content of this documentation repository | Physical attacks on customer devices |

## Security design of the AI connector

For reference, the connector's safety model is described in [docs/mcp-connector.md](docs/mcp-connector.md#security): OAuth sign-in, scoped permissions, approval before every change, no deleting, audit log and prompt-injection protection.

## Keeping your own integration safe

- Use a dedicated API user with the minimum permissions needed.
- Never commit tokens, API keys or passwords to a repository; keep them in a secrets store or an `.env` file that is not published.
- Rotate credentials if you suspect a leak and revoke connector access in Avemeo when it is no longer needed.
