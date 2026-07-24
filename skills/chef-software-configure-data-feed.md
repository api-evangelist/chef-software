---
name: Configure a Chef Automate data-feed destination
description: Register, test, and manage outbound webhook/data-feed destinations that stream Automate data to external systems.
api: openapi/chef-software-data_feed-data_feed-openapi.json
operations: [DatafeedService_AddDestination, DatafeedService_TestDestination, DatafeedService_ListDestinations, DatafeedService_UpdateDestination, DatafeedService_DeleteDestination]
---

# Configure a Chef Automate data-feed destination

The Data Feed service forwards Automate node and compliance data to external destinations (Splunk, ServiceNow, ELK, S3-compatible, or a generic HTTPS webhook).

## Auth
Send the `api-token` header. Base path: `/api/v0/datafeed`.

## Steps
1. **Add a destination** — `POST /api/v0/datafeed/destination` (`DatafeedService_AddDestination`) with the target URL, auth (secret reference), and integration type.
2. **Test it** — `POST /api/v0/datafeed/destinations/test` (`DatafeedService_TestDestination`) to verify connectivity and credentials before enabling.
3. **List destinations** — `POST /api/v0/datafeed/destinations` (`DatafeedService_ListDestinations`).
4. **Enable/disable** — `PATCH /api/v0/datafeed/destination/enable/{id}` (`DatafeedService_EnableDestination`).
5. **Update** — `PATCH /api/v0/datafeed/destination/{id}` (`DatafeedService_UpdateDestination`).
6. **Delete** — `DELETE /api/v0/datafeed/destination/{id}` (`DatafeedService_DeleteDestination`).

## Errors
`grpc.gateway.runtime.Error` envelope; see `errors/chef-software-problem-types.yml`.
