---
name: api-documentation
description: Standards and conventions for writing clear, consistent API documentation
---

# API Documentation Standards

When writing or reviewing API documentation, follow these conventions.

## Structure

Each API endpoint must document:

1. **Summary** — one-line description of what the endpoint does
2. **Method & Path** — `GET /api/v1/users`
3. **Parameters** — path params, query params, request body (required/optional, type, description)
4. **Request Example** — a realistic `curl` or JSON snippet
5. **Response** — status codes, response body schema, and example
6. **Error Codes** — possible error responses with messages

## Naming Conventions

- Use RESTful nouns (plural): `/users`, `/orders`, not `/getUser`
- Use kebab-case for URL segments: `/order-items`, not `/orderItems`
- Use camelCase for JSON fields: `createdAt`, `userId`
- Boolean fields prefixed with `is`/`has`: `isActive`, `hasPermission`

## Request/Response Documentation

- Every request body field needs: name, type, required/optional, constraints, description
- Every response field needs: name, type, description
- Nullable fields marked explicitly: `string | null`
- Date/time fields follow ISO 8601 format

## Error Responses

Always document these:
- HTTP status code
- Error code string (e.g., `USER_NOT_FOUND`)
- Error message template
- When this error occurs (trigger condition)

## Example Template

```markdown
### GET /api/v1/users/:id

Retrieve a single user by ID.

**Path Parameters**

| Param | Type   | Required | Description    |
|-------|--------|----------|----------------|
| id    | string | yes      | User UUID      |

**Response `200 OK`**

| Field     | Type          | Description        |
|-----------|---------------|--------------------|
| id        | string        | User UUID          |
| name      | string        | Display name       |
| email     | string        | Email address      |
| createdAt | string (ISO)  | Creation timestamp |

```json
{
  "id": "d290f1ee-6c54-4b01-90e6-d701748f0851",
  "name": "Jane Doe",
  "email": "jane@example.com",
  "createdAt": "2025-01-15T08:30:00Z"
}
```

**Error Codes**

| Status | Code             | Message                  | When                    |
|--------|------------------|--------------------------|-------------------------|
| 404    | USER_NOT_FOUND   | User {id} not found      | ID doesn't exist        |
```

## Checklist

- [ ] All parameters have type and description
- [ ] Request and response examples are valid and realistic
- [ ] All possible error responses are documented
- [ ] Paginated endpoints document `limit`, `offset` and `total`
- [ ] Auth requirements noted (if any)
- [ ] Rate limiting documented (if applicable)
