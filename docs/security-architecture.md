# Security Architecture

**Project:** Inventory & Purchase Request Management System  
**Owner:** Information Assurance (IA)  
**Status:** Draft - Pending SE Review

## 1. Purpose

Describe the proposed security controls for authentication, authorization, purchase request approval, transaction integrity, and audit logging.

## 2. Security Layers

### 2.1 Authentication
- Protected API endpoints must require authentication.
- Missing or invalid credentials must be rejected.
- Authentication errors must not expose sensitive system details.

### 2.2 Authorization and RBAC
- Enforce role-based permissions on the backend.
- Deny access by default unless permission is explicitly granted.
- Verify resource ownership and permissions for every protected request.
- Do not rely only on frontend controls.

### 2.3 Purchase Request Approval
- A requester must not approve their own purchase request.
- Only authorized managers may approve or reject requests.
- Purchase orders may be created only from approved requests by authorized Purchasing Staff.
- Reject unauthorized attempts to change approval status.

### 2.4 Transaction Integrity
- Validate quantities and business rules on the server.
- Prevent negative inventory.
- Handle concurrent inventory updates using appropriate database transactions and concurrency controls.
- Reject invalid business-state transitions.

### 2.5 Audit Logging
- Record relevant security events, including denied access and approval actions.
- Include appropriate event details such as timestamp, actor identifier, action, resource identifier, and outcome.
- Never log passwords, access tokens, or other secrets.
- Restrict access to audit logs.

### 2.6 API Security Testing
- Test for IDOR/BOLA vulnerabilities.
- Test unauthorized changes to purchase request fields and status.
- Test approval bypass and self-approval prevention.
- Test concurrent inventory withdrawals and transaction consistency.

## 3. Error Handling

Use the API Error Code Convention defined in `docs/api-error-codes.md`.

Error responses must not expose stack traces, credentials, or internal implementation details.

## 4. Security Tooling

- **Semgrep:** Static analysis for source code.
- **Trivy:** Dependency, container image, and configuration scanning where applicable.
- **Git hooks:** Detect hardcoded secrets before commits.

## 5. Responsibilities and Review

The IA team proposes and reviews security requirements and controls. The SE backend team must confirm implementation details against the final architecture, API design, and database design.

This document is a draft and does not claim that the controls have already been implemented or tested.
