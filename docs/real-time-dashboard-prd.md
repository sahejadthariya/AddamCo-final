# Multi-Client Agency Reporting Platform (PRD Draft)

## 1) Product Vision
Build a secure multi-client web platform for marketing and advertising agencies to replace manual weekly/monthly reporting with always-on, real-time visibility.

The platform gives agencies one admin dashboard to manage all clients while giving each client isolated access to their own live project and performance data.

## 2) Core Goals
- Eliminate manual report creation and delivery.
- Provide transparent, real-time client visibility into production and campaign progress.
- Support operational continuity when third-party integrations fail (manual override/edit capabilities).
- Scale to many client accounts without data leakage between clients.

## 3) Primary Users
- **Agency Administrator**: manages all client workspaces, integrations, users, and data corrections.
- **Client User**: views only their organization’s reports and project activity.
- **Agency Operator (optional role)**: updates project status and campaign notes for assigned clients.

## 4) Functional Requirements

### 4.1 Multi-Tenant Account Structure
- Agency can manage multiple client accounts from one admin console.
- Client data must be tenant-isolated (logical separation at minimum; physical separation optional).
- Client users can only access data scoped to their own client account.

### 4.2 Real-Time Reporting Dashboard (Client View)
Each client dashboard should include:
- **Content Production Pipeline**
  - Status for scripting, editing, publishing.
  - Current bottlenecks and ownership.
- **Video Delivery Tracking**
  - Uploaded videos list.
  - Posted/published videos list with timestamps and destination platform(s).
- **Social Performance Metrics**
  - Views, likes, comments, shares.
  - Followers/subscribers trends.
  - Date filters and period comparisons.
- **Campaign Updates & Activity Feed**
  - Timeline of updates, changes, and notable actions.
  - Human-entered updates from agency team.

### 4.3 Admin Capabilities
- Manage all client accounts and users.
- Configure and monitor data integrations.
- Manually edit/update metrics and statuses when integrations fail.
- See platform-wide operational health and data freshness.

### 4.4 Role-Based Access Control (RBAC)
- System roles: `admin`, `operator` (optional), `client_user`.
- Permissions matrix by role and tenant scope.
- Audit logging for high-impact actions (manual data edits, permission changes, integration reconnects).

## 5) Non-Functional Requirements
- **Security**: strong authentication, secure session handling, least-privilege access.
- **Privacy**: strict tenant isolation and scoped API access.
- **Reliability**: graceful degradation if third-party APIs fail.
- **Performance**: near real-time UI refresh for active metrics.
- **Scalability**: support increasing client count and metric volume.
- **Observability**: logs, metrics, and alerts for ingestion and reporting pipelines.

## 6) Suggested Data Domains
- `tenants` (clients)
- `users`
- `roles` and `permissions`
- `content_items` (script/edit/publish lifecycle)
- `video_assets` (uploaded/posted)
- `social_metrics` (time-series)
- `campaign_updates` (timeline entries)
- `integration_sync_runs` and `integration_errors`
- `audit_logs`

## 7) Dashboard Modules (MVP)
1. Client selector (admin only)
2. Content pipeline board
3. Video upload/posting register
4. Social KPI cards + trend charts
5. Campaign activity timeline
6. Integration health + last sync indicators

## 8) Failure Handling & Manual Override
- Mark stale data when sync is delayed.
- Allow admins/operators to manually patch missing values.
- Keep immutable audit trail of manual overrides (who, when, what changed).
- Reconcile manual entries with later synced values using conflict rules.

## 9) API/Integration Expectations
- Ingest data from social and publishing tools via scheduled/background jobs.
- Normalize metrics into unified schemas per platform.
- Expose tenant-scoped APIs for dashboard rendering.
- Add webhook/event processing where available to reduce sync latency.

## 10) MVP Acceptance Criteria
- Admin can create at least 3 client accounts and invite users.
- Each client user can sign in and only see their own data.
- Dashboard displays production statuses, video lists, and social KPIs for each tenant.
- Admin can manually edit a metric/status and change is reflected in client dashboard.
- All manual edits and role changes are audit-logged.
- Integration failures do not break dashboard availability; stale indicators are shown.

## 11) Post-MVP Enhancements
- White-label branding per client.
- Automated weekly/monthly PDF snapshots (optional companion to real-time view).
- Goal tracking and pacing alerts.
- Client comment threads and approval workflows.
- Predictive performance insights.

## 12) Open Decisions
- Preferred authentication strategy (SSO vs email/password).
- Exact social platforms for v1 integrations.
- Data refresh SLA targets by metric type.
- Whether operator role is required in MVP or phase 2.
- Hosting/compliance requirements (region, retention, backups).
