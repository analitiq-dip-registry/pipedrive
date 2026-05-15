# Changelog

## [1.1.1] - 2026-05-15

### Fixed
- bug: match Analitiq webhook API Gateway schema exactly (#7)

## [1.1.0] - 2026-04-23

### Added
- docs: link Pipedrive homepage in README intro (#5)

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
