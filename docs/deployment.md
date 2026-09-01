## Deployment Process

Right now, the system runs in a test setup, not a live one. Moving it to production basically means making everything more permanent and stable — a real server instead of a shared laptop, a real payment account instead of a sandbox one, and a fixed web address instead of one that changes every time a tunnel restarts. Here is what that move looks like, step by step:

1. _Get a proper server._ Move off the shared development machine onto a dedicated cloud server, with PostgreSQL installed and automatic backups turned on.
2. _Keep the app running reliably._ Set it up so the FastAPI backend runs continuously in the background (using a process manager like systemd, or a container), with nginx in front of it handling secure HTTPS traffic — replacing ngrok's temporary link.
3. _Switch to a real M-Pesa account._ Move from Daraja's test app to a live one connected to an actual paybill or till number. This means applying to Safaricom and updating the app with the new live credentials.
4. _Get a permanent USSD code._ Apply through Africa's Talking for a real shortcode (shared or dedicated) to replace the temporary sandbox code used during development.
5. _Update the callback links._ Point both Daraja and Africa's Talking to the new, permanent server address instead of the old ngrok link, so payment and USSD responses reach the right place.
6. _Run one final test._ Run the full test suite, including test_permit_flow.sh, against the new production setup before switching over to live payments.
7. _Roll out the mobile app._ Share the officials' app through the Play Store, or install it directly on their phones if a more controlled rollout is preferred.

---

## Environment Setup

- Python 3 with FastAPI and its dependencies installed, along with the project's SQLAlchemy models for permits, payments, USSD sessions, members, and resources.
- A running PostgreSQL instance with the project database created and migrations applied.
- A .env file holding the Daraja and Africa's Talking credentials, callback URLs, and database connection string. Credentials should always be copied directly from the Daraja portal rather than retyped, for reasons covered above.
- For local development, ngrok installed and ran, with the resulting forwarding URL registered as the callback URL with both Daraja and the Africa's Talking USSD channel.
- For the mobile app, the Flutter SDK and an Android toolchain, plus the API base URL configured to point at the correct backend environment (local, staging, or production).
- Once the server is running, the full set of permit, payment, and USSD endpoints can be verified through FastAPI's built-in Swagger UI, which has proven to be the fastest way to sanity-check a new environment before running the mobile app or USSD flows against it.

---

## Environment Variable Reference

The following variable names are referenced by the backend configuration. Actual values are stored only in the environment-specific .env file and are never committed to source control.

| Variable                                         | Purpose                                                                                                 |
| :----------------------------------------------- | :------------------------------------------------------------------------------------------------------ |
| DARAJA_CONSUMER_KEY / DARAJA_CONSUMER_SECRET     | Daraja OAuth application credentials                                                                    |
| DARAJA_PASSKEY                                   | Used to generate the STK push password                                                                  |
| DARAJA_CALLBACK_URL                              | Public URL Daraja calls with payment results; updated whenever the ngrok tunnel restarts in development |
| AFRICASTALKING_API_KEY / AFRICASTALKING_USERNAME | Africa's Talking account credentials for SMS and USSD                                                   |
| DATABASE_URL                                     | PostgreSQL connection string for the application database                                               |

---

## Appendix

| Term         | Meaning                                                                                                                    |
| :----------- | :------------------------------------------------------------------------------------------------------------------------- |
| _CFA_        | Community Forest Association; a community body responsible for co-managing a forest area alongside KFS.                    |
| _KFS_        | Kenya Forest Service; the government body with statutory oversight of forest resources.                                    |
| _USSD_       | Unstructured Supplementary Service Data — a menu-based protocol that works on any mobile phone without internet access.    |
| _STK Push_   | Sim Tool Kit push; the M-Pesa prompt that appears on a user's phone asking them to enter their PIN to authorize a payment. |
| _Daraja API_ | Safaricom's developer API for integrating M-Pesa payments, including STK push and payment callbacks.                       |

Message Rejesha Green by Jabali
