# Changelog

## [1.6.0] - 2026-03-26

### Added
- Endpoint definition for `/stages` (GET) -- list pipeline stages with full response schema including id, order_nr, name, is_deleted, deal_probability, pipeline_id, is_deal_rot_enabled, days_to_rotten, add_time, update_time
- Offset-based pagination with `start` and `limit` parameters (max 500)
- Filter support for `pipeline_id`

## [1.5.0] - 2026-03-26

### Added
- Endpoint definition for `/organizations` (GET) -- list and filter organizations (companies) with full response schema including id, name, owner_id (expanded object), company_id, open/closed/won/lost deal counts, people_count, activities_count, email_messages_count, files_count, notes_count, followers_count, address fields (address, street_number, route, locality, admin_area_level_1/2, country, postal_code, formatted_address), add_time, update_time, visible_to, active_flag, category_id, label, label_ids, cc_email, and related activity/picture fields
- Filters: user_id, filter_id, first_char, sort
- Offset-based pagination using `start` and `limit` parameters (max 500)
- Replication filter mapping on update_time

## [1.4.0] - 2026-03-26

### Added
- Endpoint definition for `/deals` (GET) -- list and filter deals in the sales pipeline with full response schema including id, title, value, currency, status, pipeline_id, stage_id, creator_user_id (expanded object), user_id (expanded object), person_id (expanded object), org_id (expanded object), probability, expected_close_date, won_time, lost_time, close_time, lost_reason, activity/email/file/note counts, add_time, update_time, and all standard deal fields
- Filters: user_id, filter_id, stage_id, status, sort, owned_by_you
- Pagination configuration using offset-based pagination with `start` and `limit` parameters (max 500)
- Replication filter mapping on update_time

## [1.3.0] - 2026-03-26

### Added
- Endpoint definition for `/users` (GET) -- list users (team members) with full response schema including id, name, email, phone, activated, last_login, created, modified, has_created_company, access (nested array with app/admin/permission_set_id), active_flag, timezone_name, timezone_offset, role_id, icon_url, is_you, is_deleted
- No pagination required -- the endpoint returns all users in a single response

## [1.2.0] - 2026-03-26

### Added
- Endpoint definition for `/persons` (GET) -- list and filter contact persons with full response schema including id, name, first_name, last_name, email (array), phone (array), org_id (expanded object), owner_id (expanded object), deal counts, activity counts, add_time, update_time, and all standard person fields
- Filters: user_id, filter_id, first_char, sort
- Pagination configuration using offset-based pagination with `start` and `limit` parameters (max 500)
- Replication filter mapping on update_time

## [1.1.0] - 2026-03-26

### Added
- Endpoint definition for `/pipelines` (GET) -- list sales pipelines with full response schema including id, name, url_title, order_nr, active, deal_probability, add_time, update_time, and selected fields
- No pagination required -- the endpoint returns all pipelines in a single response

## [1.0.0] - 2026-03-26

### Added
- Initial connector definition with OAuth2 Authorization Code authentication
- Post-auth step for automatic API domain resolution via GET /v1/users/me
