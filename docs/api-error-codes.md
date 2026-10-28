
# API Error Code Convention

**Project:** Inventory & Purchase Request Management System  
**Owner:** Information Assurance (IA)  
**Status:** Draft - Pending SE Review

## 1. Purpose

Define consistent HTTP status codes for API errors and support security testing.

## 2. HTTP Status Codes

| HTTP Status | Meaning | Example |
|---|---|---|
| 400 Bad Request | Invalid input | Missing required field or invalid quantity |
| 401 Unauthorized | Authentication required or invalid | Missing or invalid access token |
| 403 Forbidden | Authenticated user lacks permission | User attempts to approve a request without approval rights |
| 404 Not Found | Resource does not exist or is not accessible under the disclosure policy | Purchase request not found |
| 409 Conflict | Request conflicts with current business state | Approving an already approved request |
| 429 Too Many Requests | Rate limit exceeded | Too many requests within a time window |
| 500 Internal Server Error | Unexpected server error | Unhandled server exception |

## 3. Security Requirements

- Do not expose stack traces, passwords, tokens, or internal system details in error responses.
- Apply authorization checks on every protected endpoint.
- Prevent users from approving their own purchase requests.
- Record relevant security events without logging secrets.
- Use consistent response formats across API endpoints.

## 4. Coordination

The IA team proposes and reviews this convention. The SE backend team must confirm and implement it consistently.
