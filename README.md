# e-conomic MCP server

Find an accounting customer and add a named contact to that existing customer.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ECONOMIC_APP_SECRET_TOKEN`
- `ECONOMIC_AGREEMENT_GRANT_TOKEN`



Credential help: https://www.e-conomic.com/developer/connect

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call economic_list_customers '{}'
```

## Use with an MCP client

Launch `node /absolute/path/e-conomic-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| economic_list_customers | Read | economic list customers |
| economic_get_customer | Read | economic get customer |
| economic_create_customer_contact | Explicit approval required | economic create customer contact |

## Concrete workflow

Find an accounting customer and add a named contact to that existing customer.

1. economic_list_customers
2. economic_get_customer
3. economic_create_customer_contact

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=e-conomic&integration=e-conomic-mcp&utm_source=github&utm_campaign=github-e-conomic-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/e-conomic/).

## Provenance and maintenance

- https://restdocs.e-conomic.com/

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
