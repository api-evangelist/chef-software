---
name: Read Chef Automate compliance reports
description: Query compliance scan results, control items, and per-node reports from Chef Automate.
api: openapi/chef-software-compliance-reporting-reporting-openapi.json
operations: [ReportingService_ListReports, ReportingService_ReadReport, ReportingService_ListNodes, ReportingService_ReadNode, ReportingService_ListControlItems]
---

# Read Chef Automate compliance reports

Chef Automate aggregates Chef InSpec compliance scan results. This skill reads that data through the Reporting service.

## Auth
Send the `api-token` header. Base path: `/api/v0/compliance/reporting`.

## Steps
1. **List reports** — `POST /api/v0/compliance/reporting/reports` (`ReportingService_ListReports`) with `filters` (by date, profile, node, environment) to find report ids.
2. **Read a report** — `POST /api/v0/compliance/reporting/reports/id/{id}` (`ReportingService_ReadReport`) for the full result including profiles and control outcomes.
3. **List scanned nodes** — `POST /api/v0/compliance/reporting/nodes/search` (`ReportingService_ListNodes`).
4. **Read one node's posture** — `GET /api/v0/compliance/reporting/nodes/id/{id}` (`ReportingService_ReadNode`).
5. **Aggregate failing controls** — `POST /api/v0/compliance/reporting/controls` (`ReportingService_ListControlItems`) to rank controls by failures across the estate.

## Errors
Responses use the `grpc.gateway.runtime.Error` envelope; see `errors/chef-software-problem-types.yml`. All list endpoints take a `filters[]` array of `{type, values[]}`.
