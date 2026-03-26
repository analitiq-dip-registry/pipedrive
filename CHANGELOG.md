# Changelog

## [1.0.0] - 2026-03-26

### Added
- Connector definition with OAuth2 Authorization Code authentication
- Post-auth step for automatic API domain resolution via GET /v1/users/me
- Endpoint `/deals` (GET) -- sales pipeline deals with filters and incremental sync
- Endpoint `/persons` (GET) -- contacts with filters and incremental sync
- Endpoint `/organizations` (GET) -- companies with filters and incremental sync
- Endpoint `/users` (GET) -- team members
- Endpoint `/pipelines` (GET) -- sales pipelines
- Endpoint `/stages` (GET) -- pipeline stages
