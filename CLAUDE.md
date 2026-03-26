---
name: Pipedrive
description: >
  Sales CRM and pipeline management platform for tracking deals, contacts, and sales activities.
type: api
---

# Pipedrive

Pipedrive is a sales-focused CRM platform that provides data on deals, persons (contacts), organizations, users, pipelines, and stages. The API follows REST conventions and returns JSON responses.

## Authentication

### OAuth2 Authorization Code
- Client app required: yes (register at Pipedrive Marketplace)
- Scopes: deals:read, contacts:read, users:read (configured during app registration, not passed in the authorize URL)
- Token expiry: 3600 seconds (1 hour)
- Refresh token expiry: 60 days of non-use

### API Key (alternative, not used in this connector)
- Header format: `x-api-token: ${api_key}`
- Obtained from Pipedrive Settings > Personal preferences > API

## Post-Auth Steps

After OAuth2 authentication, the connector calls `GET https://api.pipedrive.com/v1/users/me` (the generic Pipedrive host, not the company-specific domain) to retrieve the `company_domain` field (e.g., `yourcompany`), which is stored as the `api_domain` variable and used to construct the company-specific API base URL (`https://${api_domain}.pipedrive.com/api/v1/`).

## Available Endpoints

| Endpoint | Method | Description | Status |
|----------|--------|-------------|--------|
| /deals   | GET    | List and filter deals in the sales pipeline | Defined |
| /persons | GET    | List and filter contact persons | Defined |
| /organizations | GET | List and filter organizations (companies) | Defined |
| /users   | GET    | List users (team members) in the Pipedrive account | Defined |
| /pipelines | GET  | List sales pipelines | Defined |
| /stages    | GET  | List stages within pipelines | Defined |

## Rate Limits

- 80 requests per 2 seconds (burst limit per token)
- Daily token budget based on subscription plan and seat count

## Caveats

- The base URL is company-specific, resolved via `GET /v1/users/me` after OAuth. It follows the pattern `https://${api_domain}.pipedrive.com/api/v1/`.
- Pipedrive uses a token-based rate limiting system where different endpoints consume different numbers of tokens. The connector is configured for 80 requests per 2-second window, but actual limits may vary by endpoint cost.
- Refresh tokens expire after 60 days of non-use. Long-idle connections will need to re-authenticate.
- The `/deals`, `/persons`, and `/organizations` endpoints use offset-based pagination with `start` and `limit` query parameters (max 500 per request). The `additional_data.pagination` response object indicates whether more items are available.
- The `/users`, `/pipelines`, and `/stages` endpoints return all records in a single response and do not support pagination.
