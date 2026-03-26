# Pipedrive

Connector for the Pipedrive CRM API. Enables reading deals, contacts, organizations, users, pipelines, and stages from your Pipedrive sales account.

## What is this?

This is a **connector** -- a configuration that defines how to authenticate with Pipedrive and what data endpoints are available for reading. It does not move data by itself. Instead, it is used by the [Analitiq](https://analitiq-app.com) data integration platform or the open-source `analitiq-core` engine to set up data pipelines.

## How to use this connector

There are two ways to use this connector:

### Option 1 -- Analitiq Cloud (no setup required)

All connectors from this registry are automatically available on [analitiq-app.com](https://analitiq-app.com). Simply log in, select the connector, and follow the on-screen instructions to connect your account.

### Option 2 -- Open Source (self-hosted)

All connectors are open source and free to use. To get started:

1. Clone the [analitiq-core](https://github.com/analitiq-core) repository
2. Install the Claude plugin `analitiq-plugin-dataflow`
3. Launch Claude in the root directory of `analitiq-core`
4. Tell it: *"I need to move data from X to Y"*

The `analitiq-plugin-dataflow` plugin will automatically fetch the required connectors from the [Analitiq Skill Registry](https://github.com/analitiq-skill-registry) and set up the data flow pipeline for you.

## Prerequisites

- A Pipedrive account with an active subscription
- For OAuth2 (recommended): A registered app in the [Pipedrive Marketplace Developer Hub](https://developers.pipedrive.com/) with a client ID and client secret
- For API key (alternative): Access to your personal API token from Pipedrive account settings

## Authentication

Pipedrive supports two authentication methods. This connector uses **OAuth2 Authorization Code** flow, which is the recommended approach for production integrations and marketplace apps.

### How to get your credentials (OAuth2)

1. Log in to the [Pipedrive Developer Hub](https://developers.pipedrive.com/)
2. Create a new app under "Marketplace Manager"
3. Configure the OAuth redirect URI to match your Analitiq callback URL
4. Select the required scopes: `deals:read`, `contacts:read`, `users:read`, and any additional scopes for your use case
5. Note down the **Client ID** and **Client Secret** -- these are used by the platform to authenticate on your behalf
6. When connecting through Analitiq, click "Connect to Pipedrive" and authorize the app in the browser popup

### How to get your credentials (API Key -- alternative)

1. Log in to your Pipedrive account
2. Navigate to **Settings** (gear icon) > **Personal preferences** > **API**
3. Copy your personal API token

## Available Endpoints

The table below lists all data endpoints defined by this connector. Each endpoint represents a resource you can read from.

| Endpoint | Method | Description | Status |
|----------|--------|-------------|--------|
| /deals   | GET    | List and filter deals in the sales pipeline | Defined |
| /persons | GET    | List and filter contact persons | Defined |
| /organizations | GET | List and filter organizations (companies) | Defined |
| /users   | GET    | List users (team members) in the Pipedrive account | Defined |
| /pipelines | GET  | List sales pipelines | Defined |
| /stages    | GET  | List stages within pipelines | Defined |

## Limitations

- **Rate limits** -- Pipedrive uses a token-based rate limiting system with a burst limit of approximately 80 requests per 2-second window. Daily budgets vary by subscription plan and seat count.
- **Token expiry** -- OAuth2 access tokens expire after 1 hour. Refresh tokens expire after 60 days of non-use, requiring re-authentication for idle connections.
- **Company-specific URLs** -- Each Pipedrive account has a unique API domain (e.g., `yourcompany.pipedrive.com`). The connector resolves this automatically after authentication via a call to `/v1/users/me`.
- **Pagination** -- The API returns a maximum of 500 items per request. Large datasets require multiple paginated requests.

## For AI agents

This connector includes `CLAUDE.md` and `AGENTS.md` files -- machine-readable references used by AI agents and agentic frameworks. They document authentication types, available endpoints, post-auth steps, and any caveats for programmatic use. Both files are kept identical -- `CLAUDE.md` is for Claude Code, `AGENTS.md` is for other agent frameworks.

## Create a connector to any system

You can create a new connector to any API or database using Claude and the Analitiq connector builder plugin:

1. Install [Claude Code](https://claude.ai/code)
2. Install the connector builder plugin:
   ```
   claude plugin add analitiq-skill-registry/analitiq-plugin-connector-builder
   ```
3. Launch Claude and say: *"I want to create a connector for [system name]"*
4. The plugin will interview you about the system, research its API documentation, and generate the full connector with all required files

No coding required -- the plugin handles authentication research, endpoint schema generation, and file creation automatically.

## Contributing

All connectors in this registry are community-maintained and live at [github.com/analitiq-skill-registry](https://github.com/analitiq-skill-registry). To add new endpoints or improve an existing connector, install the [connector builder plugin](https://github.com/analitiq-skill-registry/analitiq-plugin-connector-builder) and follow its instructions.

## Links

- [Pipedrive API Documentation](https://developers.pipedrive.com/docs/api/v1)
- [Analitiq Cloud](https://analitiq-app.com)
- [Analitiq Core (open source)](https://github.com/analitiq-core)
