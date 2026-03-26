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
- Scopes: deals:read, deals:full, contacts:read, contacts:full, leads:read, leads:full, activities:read, activities:full, products:read, products:full, admin, users:read
- Token expiry: 3600 seconds (1 hour)
- Refresh token expiry: 60 days of non-use

### API Key (alternative, not used in this connector)
- Header format: `x-api-token: ${api_key}`
- Obtained from Pipedrive Settings > Personal preferences > API

## Post-Auth Steps

The OAuth2 token response includes an `api_domain` field that contains the company-specific API domain (e.g., `yourcompany.pipedrive.com`). This is automatically resolved and applied as the base URL for all subsequent API requests.

## Available Endpoints

| Endpoint | Method | Description | Status |
|----------|--------|-------------|--------|
| /deals   | GET    | List and filter deals in the sales pipeline | Defined |
| /persons | GET    | List and filter contact persons | Defined |
| /organizations | GET | List and filter organizations (companies) | Defined |
| /users   | GET    | List users (team members) in the Pipedrive account | Defined |
| /pipelines | GET  | List sales pipelines | Defined |
| /v2/stages | GET  | List stages within pipelines (cursor-paginated, v2 API) | Defined |

## Rate Limits

- 80 requests per 2 seconds (burst limit per token)
- Daily token budget based on subscription plan and seat count

## Caveats

- The base URL is company-specific and dynamically resolved from the OAuth token response `api_domain` field. It follows the pattern `https://{company_domain}.pipedrive.com/api/v1/`.
- Pipedrive uses a token-based rate limiting system where different endpoints consume different numbers of tokens. The burst limit is approximately 80 requests per 2-second window, but complex endpoints cost more tokens.
- Refresh tokens expire after 60 days of non-use. Long-idle connections will need to re-authenticate.
- Pagination uses `start` and `limit` query parameters with a default limit of 100 and a maximum of 500 items per request.
- The API returns a `additional_data.pagination` object indicating whether more items are available.
