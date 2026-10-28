# Role-Based Access Control (RBAC) Matrix

**Project:** Inventory & Purchase Request Management System  
**Owner:** Information Assurance (IA)  
**Status:** Draft - Pending SE Review

## 1. Purpose

Define access permissions for each user role to protect purchase requests, approvals, purchase orders, and inventory transactions.

## 2. Roles

- **Requester:** Creates and views their own purchase requests.
- **Manager:** Reviews and approves or rejects purchase requests.
- **Purchasing Staff:** Processes approved purchase requests and creates purchase orders.
- **Administrator:** Manages system configuration and user roles. Business transaction permissions must follow the approved authorization policy.

## 3. Permission Matrix

| Action | Requester | Manager | Purchasing Staff | Administrator |
|---|---|---|---|---|
| Create purchase request | Own | No | No | No by default |
| View own purchase requests | Yes | Yes | Yes | According to policy |
| View other users' requests | No | Only if authorized | Only if authorized | According to policy |
| Approve or reject purchase request | No | Yes, except own request | No | No by default |
| Modify approval status directly | No | No | No | No by default |
| Create purchase order | No | No | Only for approved requests | No by default |
| Modify inventory transactions | No | No | Only if authorized | No by default |
| Manage user roles | No | No | No | Yes |
| View audit logs | No | If authorized | If authorized | If authorized |

## 4. Security Rules

- Deny access by default unless permission is explicitly granted.
- Enforce authorization on the server for every protected endpoint.
- Prevent a requester from approving their own purchase request.
- Prevent purchase order creation from an unapproved request.
- Prevent unauthorized changes to request status, values, and inventory transactions.
- Record relevant security events without logging passwords, tokens, or other secrets.
- Do not rely only on frontend controls to enforce permissions.

## 5. Review Notes

This matrix is a draft for review by the SE backend team. Confirm the roles, ownership rules, and permissions against the final API design and business requirements before implementation.
