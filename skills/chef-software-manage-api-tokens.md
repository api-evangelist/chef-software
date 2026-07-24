---
name: Manage Chef Automate API tokens
description: Create, list, inspect, and revoke Chef Automate IAM v2 API tokens used to authenticate API clients.
api: openapi/chef-software-iam-v2-tokens-openapi.json
operations: [Tokens_CreateToken, Tokens_ListTokens, Tokens_GetToken, Tokens_UpdateToken, Tokens_DeleteToken]
---

# Manage Chef Automate API tokens

Chef Automate API tokens authenticate every API client. Tokens are IAM v2 resources; a token only has access granted to it by IAM policies that name it as a member.

## Auth
Send an admin (or token-management-authorized) API token in the `api-token` header on every request. Base path: `/apis/iam/v2`.

## Steps
1. **Create a token** — `POST /apis/iam/v2/tokens` (`Tokens_CreateToken`) with `id`, `name`, and `active: true`. The response returns the token `value` once — store it securely.
2. **Grant it access** — add the token id as a member of an IAM policy (see `openapi/chef-software-iam-v2-policy-openapi.json`, `Policies_AddPolicyMembers`). A raw token with no policy can authenticate but is authorized for nothing.
3. **List tokens** — `GET /apis/iam/v2/tokens` (`Tokens_ListTokens`).
4. **Inspect a token** — `GET /apis/iam/v2/tokens/{id}` (`Tokens_GetToken`).
5. **Enable/disable or rename** — `PUT /apis/iam/v2/tokens/{id}` (`Tokens_UpdateToken`) toggling `active`.
6. **Revoke** — `DELETE /apis/iam/v2/tokens/{id}` (`Tokens_DeleteToken`).

## Errors
Errors use the `grpc.gateway.runtime.Error` envelope (`code`, `message`). `401 UNAUTHENTICATED` means a missing/invalid `api-token`; `403 PERMISSION_DENIED` means the caller's token lacks an IAM policy for the action. See `errors/chef-software-problem-types.yml`.
