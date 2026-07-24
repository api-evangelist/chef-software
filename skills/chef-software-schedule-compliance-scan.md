---
name: Schedule a Chef Automate compliance scan
description: Register target nodes and create/rerun a Chef Automate scanner job to run InSpec compliance scans.
api: openapi/chef-software-compliance-scanner-jobs-jobs-openapi.json
operations: [JobsService_Create, JobsService_List, JobsService_Read, JobsService_Rerun, JobsService_Delete]
---

# Schedule a Chef Automate compliance scan

Chef Automate scanner jobs run InSpec profiles against managed nodes on a schedule or on demand.

## Auth
Send the `api-token` header. Base paths: `/api/v0/nodes` and `/api/v0/compliance/scanner/jobs`.

## Steps
1. **Register the target node(s)** — `POST /api/v0/nodes` (`NodesService_Create`, in `openapi/chef-software-nodes-nodes-openapi.json`) with connection detail and secret references, or bulk with `NodesService_BulkCreate`.
2. **Store connection secrets** — `POST /api/v0/secrets` (`SecretsService_Create`, in `openapi/chef-software-secrets-secrets-openapi.json`) and reference the secret id from the node.
3. **Create the scan job** — `POST /api/v0/compliance/scanner/jobs` (`JobsService_Create`) referencing the node(s), the InSpec profiles, and an optional `recurrence`.
4. **List / find jobs** — `POST /api/v0/compliance/scanner/jobs/search` (`JobsService_List`).
5. **Inspect a job** — `GET /api/v0/compliance/scanner/jobs/id/{id}` (`JobsService_Read`).
6. **Rerun** — `GET /api/v0/compliance/scanner/jobs/rerun/id/{id}` (`JobsService_Rerun`).
7. **Read results** — use the Read-compliance-reports skill once the job completes.

## Errors
`grpc.gateway.runtime.Error` envelope; see `errors/chef-software-problem-types.yml`.
