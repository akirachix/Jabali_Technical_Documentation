# Security Architecture

Security will be implemented as multiple layers rather than one control. The mobile application and web dashboard will authenticate users before protected operations. The backend API will independently verify authentication and permissions before returning or changing data. The database will enforce appropriate constraints. Integrations will use secure credentials and protected callbacks.

| Layer            | Implementation                                                                                                       | Purpose                                         |
| :--------------- | :------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------- |
| _User interface_ | Hide protected actions from users without the required role, while never treating UI hiding as the security boundary | Reduce accidental access and improve usability  |
| _API/backend_    | Authenticate every protected request and enforce role/ownership checks on the server                                 | Prevent bypass through direct API calls         |
| _Database_       | Use constraints, relationships and restricted database access; protect sensitive fields appropriately.               | Protect data integrity and limit direct access. |
| _Integrations_   | Store API credentials in environment/secret configuration and validate incoming payment callbacks.                   | Protect third-party communication.              |
| _Audit/logging_  | Record important security-sensitive actions without logging passwords, PINs or unnecessary personal data.            | Support accountability and investigation.       |
| _Operations_     | Back up important records, control administrator access and review access regularly.                                 | Maintain security and availability.             |

---

### Authentication and Password Security

Authorised users such as CFA officials, KFS officers and administrators will use authenticated accounts. Authentication will be enforced by the backend, not only by the frontend.

**Implementation Guidelines**

- _No Plain Text:_ Passwords will never be stored as plain text.
- _Hashing:_ Passwords will be hashed using a modern password-hashing algorithm such as bcrypt with an appropriate work factor.
- _Verification:_ During login, the entered password will be verified against the stored password hash; the original password will never be recovered or stored.
- _Token Issuance:_ Authentication tokens will be issued only after successful verification.
- _API Protection:_ Protected API endpoints will require a valid authentication token.
- _Token Expiry:_ Tokens will have an expiry period and should be revoked/invalidated where the product's authentication design supports it.
- _Password Resets:_ Password reset tokens, if implemented, will be short-lived, single-use and stored/handled securely.
- _Generic Errors:_ Login failures will return generic authentication errors rather than revealing whether a particular account exists.

---

### Role-Based Access Control (RBAC)

The system will enforce different permissions for CFA officials, CFA members, the general public, KFS officers, rangers and administrators.

**Implementation Guidelines**

- _Assigned Roles:_ Each authenticated account will have an assigned role.
- _Backend Enforced:_ The backend will use role/permission checks before executing protected operations.
- _Ownership Checks:_ Ownership checks will be added where necessary; for example, a member can access their own permit information but not another member's records.
- _CFA Scoping:_ CFA-scoped records will be checked against the user's assigned CFA before access is granted.
- _KFS Assignments:_ KFS users will only receive the operational information appropriate to their assignment.
- _Admin Separation:_ Administrative endpoints will be separated from ordinary user endpoints and protected more strictly.
- _True Boundary:_ Frontend role restrictions will improve the user experience, but backend authorization will remain the actual security boundary.

### Role Permissions Matrix

| Role             | Examples of Permission                                                                        |
| :--------------- | :-------------------------------------------------------------------------------------------- |
| _CFA Official_   | Create/register members; manage CFA activities; record attendance; update restoration records |
| _CFA Member_     | View own membership information; request permitted resources; receive your own confirmations. |
| _General Public_ | Submit permitted public incident reports through USSD.                                        |
| _KFS Officer_    | View authorised CFA, permit, incident and restoration monitoring information                  |
| _Administrator_  | Manage authorised system configuration and user access.                                       |

---

## National ID & Personal Data Protection

The platform collects a national ID number, phone number, and location during membership registration. These are sensitive records and will be protected at both application and data-storage levels.

**Implementation Guidelines**

- _Restricted Endpoints:_ Sensitive fields will only be returned by API endpoints that require them.
- _Schema Separation:_ API response schemas will use separate public and restricted representations so that ordinary product responses do not accidentally expose ID numbers.
- _Encryption at Rest:_ National ID numbers will be encrypted at rest where appropriate to the final deployment environment; access to the decryption key will be restricted to the application service.
- _Private Storage:_ ID and member photographs will be stored in protected/private storage rather than a publicly accessible folder.
- _Access Control:_ Database and storage permissions will prevent ordinary users from directly reading protected files.
- _Anonymized IDs:_ Reports will use non-sensitive identifiers such as membership numbers where possible instead of national ID numbers.
- _Masked Fields:_ Phone numbers will be masked in administrative views where the full number is not required.
- _Location Scoping:_ Location information will only be returned to roles that need it.

---

## Data Encryption

**Data in Transit**

- _HTTPS/TLS:_ Production web, mobile and API traffic will use HTTPS/TLS.
- _Credential Protection:_ HTTP requests containing credentials or personal information will not be accepted in production.
- _Secure Integrations:_ USSD/SMS providers and payment providers will be accessed through their supported secure integration mechanisms.
- _No Hardcoding:_ API secrets and integration credentials will not be hard-coded into source files.

**Data at Rest**

- _Environment Encryption:_ Production database and storage encryption will be enabled according to the hosting environment.
- _Application-Level Encryption:_ Highly sensitive fields such as national ID information will have application-level encryption where required.
- _Key Separation:_ Encryption keys will be stored separately from application data using protected environment variables or a secrets-management facility.
- _Repository Safety:_ Encryption keys will not be committed to GitHub.

---

### M-Pesa / Daraja Security

M-Pesa is used for CFA registration fees and permit payments. The system will treat payment status as a controlled state rather than allowing an application screen to declare that payment succeeded.

**Implementation Guidelines**

- _Secret Storage:_ Daraja consumer credentials, shortcode and passkey will be stored as protected environment/secret values.
- _Backend Initiation:_ The application will initiate the STK Push through the backend rather than exposing Daraja credentials to the mobile/web client.
- _Internal Linking:_ Each payment request will have an internal reference linking it to the registration or permit request.
- _Callback Validation:_ The backend will process the Daraja callback and update the payment status.
- _State Lifecycle:_ Payment states will include at minimum pending, successful, and failed.
- _Enforced State:_ A permit will only move to issued/paid status after the backend has confirmed successful payment.
- _Resource Validation:_ An unavailable resource will be rejected before the payment request is initiated.
- _Idempotency:_ Duplicate callbacks will be handled idempotently so the same payment cannot issue multiple permits.
- _No PIN Storage:_ M-Pesa PINs will never be collected or stored by the platform.

---

### USSD & SMS Security

**USSD Implementation**

- _Input Validation:_ Every USSD request will be validated against the expected menu option and input format.
- _Session Lifecycle:_ Session state will be maintained so users cannot skip required steps.
- _Data Privacy:_ Sensitive information will not be displayed in USSD menus.
- _Identity Verification:_ Member identity will be verified using the approved membership/phone verification process before restricted services are provided.
- _Pre-payment Verification:_ Permit eligibility and resource availability will be checked by the backend before payment.
- _Timeouts:_ USSD session timeouts will prevent abandoned sessions from remaining active indefinitely.
- _Atomic Transactions:_ Interrupted sessions will not automatically create completed permits.
- _Abuse Controls:_ Rate limiting or provider-level controls will be considered to reduce automated abuse and repeated malicious submissions.

**SMS Implementation**

- _Secret Storage:_ SMS credentials will be stored securely as environment/secret configuration.
- _Template Authorization:_ Messages will use templates approved by the product team.
- _Payload Sanitation:_ Membership and permit numbers can be sent, but national ID numbers, passwords, M-Pesa PINs and sensitive incident details will not be sent.
- _Decoupled Delivery:_ SMS delivery status will be treated separately from the underlying transaction status.
- _Failure Recovery:_ If an SMS fails, the membership/permit record will remain valid and available through the appropriate application interface.
- _Flood Controls:_ Repeated message requests will be controlled to reduce spam or accidental message flooding.

---

### Illegal Activity Reporting Security

**Implementation Guidelines**

- _Minimal Collection:_ USSD will collect only the information required to create the report.
- _Report Identification:_ The backend will assign a report identifier and timestamp.
- _Identity Separation:_ Reporter identity will be stored separately from public-facing incident information where practical.
- _Role Restriction:_ Only authorised KFS roles will receive the detailed incident information.
- _Scoped Ranger Access:_ Ranger access will be limited to the operational details needed for response.
- _No Public Search:_ Incident records will not be publicly searchable.
- _Audit Trail:_ Important incident changes will be recorded in an audit trail.
- _Edit Protection:_ Unauthorised users will not be allowed to edit or delete submitted reports.

---

### Permit Security & Business-Rule Enforcement

**Implementation Guidelines**

- _Eligibility Check:_ The backend will verify that the requester is an eligible registered member before creating a member permit.
- _Availability Check:_ The backend will check the requested resource against CFA/KFS availability and quota rules.
- _Ordered Workflow:_ The system will create the payment request only after the availability check passes.
- _Controlled Issuance:_ Permit issuance will be a backend-controlled operation triggered only after required conditions are satisfied.
- _Unique Identifiers:_ Each permit will have a unique identifier.
- _Full Linking:_ The permit will be linked to the member, resource, payment and relevant date.
- _Controlled Status:_ Permit status changes will be controlled by authorised backend operations.
- _One-Time Use:_ Expired, cancelled or already-used permits will not be treated as valid where the business rules require one-time use.

---

[9:00 AM]## Data Validation and Integrity

**Implementation Guidelines**

- _Schema Validation:_ Required fields will be validated at the API boundary using defined schemas.
- _Database Constraints:_ Database constraints will enforce required relationships and valid references.
- _Uniqueness:_ Unique constraints will be used for values that must be unique, such as membership numbers.
- _Referential Integrity:_ Foreign keys will link members, permits, payments, CFA groups and activities correctly.
- _Enumerated Categories:_ Enumerated fields will restrict values to approved categories such as PELIS, beekeeping, grazing, ecotourism, non-timber products and nursery/water management.
- _Server-Side Validation:_ Business validation will prevent invalid operations even if a malicious or modified client sends a request directly to the API.
- _Transactional Integrity:_ Transactions will be used for multi-step operations where partial completion could corrupt records.

---

## Audit Logging

The platform needs an audit trail because it manages official membership, payment, permit, incident and restoration records.

**Implementation Guidelines**

- _Tracked Actions:_ Record important actions such as member registration, permit issuance, payment-status changes, incident submission, restoration updates and administrative access changes.
- _Captured Detail:_ Capture the acting user or system process, action, affected record, timestamp and relevant outcome.
- _Sensitive Exclusions:_ Do not log passwords, M-Pesa PINs, authentication tokens or unnecessary sensitive personal data.
- _Restricted Access:_ Restrict audit-log access to authorised administrators or security/oversight personnel.
- _Tamper Protection:_ Audit records should be protected against ordinary users editing or deleting them.
- _Investigation Use:_ Use logs during incident investigation and troubleshooting.

---

### API Security

**Implementation Guidelines**

- _Required Auth:_ Protected API routes will require authentication.
- _Server-Side Authorization:_ Authorisation checks will run on the server for every protected operation.
- _Request Validation:_ Request bodies will be validated before processing.
- _Scoped Responses:_ API responses will expose only the fields appropriate for the caller's role.
- _Rate Limiting:_ Rate limiting should be applied to authentication and abuse-sensitive endpoints where supported by the deployment.
- _Consistent Responses:_ Consistent HTTP status codes and safe error messages will be used.
- _No Internal Leakage:_ Internal stack traces and database details will never be returned to normal users in production.

---

### Error Handling and Secure Logging

**Implementation Guidelines**

- _Non-Sensitive Errors:_ Users will receive clear but non-sensitive error messages.
- _No Exposure:_ Database errors, stack traces, credentials and internal configuration will not be displayed to users.
- _Business Failures:_ Expected business failures such as unavailable resources and failed payments will have specific user-facing responses.
- _Internal Logging:_ Unexpected errors will be logged internally with enough context for troubleshooting without exposing sensitive information.
- _Traceability:_ Errors should include a traceable internal reference where the product team needs to investigate a failure.

---

### Backup, Recovery and Availability

**Implementation Guidelines**

- _Scheduled Backups:_ Database backups will be scheduled according to the operational importance of membership, permit, payment, incident and restoration records.
- _Protected Backups:_ Backups will be protected using the same access and encryption principles as production data.
- _Tested Restores:_ Restore procedures will be tested rather than assuming that a backup is usable.
- _Explicit States:_ Payment and permit workflows will use explicit states so temporary provider failures do not create false successful transactions.
- _Safe Interruptions:_ USSD interruptions will leave incomplete requests incomplete rather than issuing service accidentally.

---

### Access Review and Offboarding

**Implementation Guidelines**

- _Authorised Accounts:_ Maintain a list of authorised CFA, KFS and administrator accounts.
- _Periodic Review:_ Review access when a user's responsibility changes.
- _Prompt Disabling:_ Disable access promptly when a user leaves the role.
- _Admin Scrutiny:_ Review administrator accounts more frequently because of their broader permissions.
- _No Reuse:_ Do not reuse another person's account after staff changes.

---

## Privacy-by-Design Product Flow

Security will be included in each major workflow rather than added after development.

| Workflow              | Security Built Into the Flow                                                                                                                                                      |
| :-------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Member registration_ | Authenticate CFA official → verify required information → capture consent → protect ID → create membership → payment confirmation → generate membership number → send minimal SMS |
| _Permit request_      | Identify member → validate request → check resource → if available initiate payment → confirm payment → issue unique permit → send confirmation                                   |
| _Illegal activity_    | Receive report → validate inputs → protect reporter identity → create timestamped incident → expose only to authorised KFS roles → audit actions                                  |
| _CFA activity_        | Authenticate official → validate activity data → restrict CFA scope → notify members → record attendance/restoration updates → retain history                                     |
| _KFS monitoring_      | Authenticate KFS user → enforce role/scope → show authorised summaries → protect sensitive member information → audit important actions                                           |

---

## Security Testing Plan

Security requirements will be tested as acceptance criteria before the feature is considered complete.

| Test                                                | Expected Result                                                                                                     |
| :-------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------ |
| Login with correct credentials                      | An authenticated session is created.                                                                                |
| Login with wrong password                           | Access denied; no sensitive account details revealed.                                                               |
| Password database inspection                        | Only password hashes are stored.                                                                                    |
| Member accesses another member's record             | Access denied.                                                                                                      |
| CFA official accesses unrelated restricted KFS data | Access denied.                                                                                                      |
| Unauthorised API request                            | Authentication/authorisation failure returned.                                                                      |
| National ID requested by unauthorised role          | The field is not returned.                                                                                          |
| Public request for incident details                 | Internal incident data is not exposed.                                                                              |
| Unavailable resource permit request                 | No payment initiated.                                                                                               |
| Failed M-Pesa payment                               | Permit/registration is not confirmed as paid.                                                                       |
| Pending M-Pesa payment                              | Paid service is not issued.                                                                                         |
| Repeated payment callback                           | No duplicate permit/payment action.                                                                                 |
| USSD session interruption                           | No falsely completed transaction.                                                                                   |
| SMS failure                                         | The underlying record remains intact.                                                                               |
| Former user logs in                                 | Access denied after account deactivation.                                                                           |
| Audit log access by ordinary user                   | Access denied.                                                                                                      |
| Permit request and resource available               | STK push received on payment, SMS with permit number is sent, permit record created with status completed.          |
| Permit request and resource unavailable             | No STK push is triggered; member receives a message explaining the resource is unavailable.                         |
| Member registration and successful payment          | Unique membership number generated, confirmation SMS sent, record stored and linked to database.                    |
| Daraja OAuth token request                          | 200 response with a valid bearer token, failure cases return a clear error rather than a silent retry.              |
| Payment callback handling                           | Backend updates payment status correctly and triggers the appropriate SMS regardless of success or failure outcome. |
| Illegal activity report                             | Report appears on the KFS dashboard in real time, tagged with activity type and location.                           |

---
