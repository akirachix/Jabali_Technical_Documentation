# Backend

The Rejesha Green backend provides the core services that support the Rejesha Green platform. It manages application data, handles business operations, provides REST APIs, and enables communication between client applications and the backend system.

## System Overview

The backend is responsible for:

- User authentication and authorization
- User and role management
- Community Forest Association management
- Forest zone and resource management
- Permit processing
- Payment processing
- Forest activities tracking
- Tree survival monitoring
- Incident reporting
- USSD service integration

## Technology Stack

The backend is built using:

- Python
- FastAPI
- PostgreSQL
- SQLAlchemy
- Alembic
- Pydantic
- JWT Authentication

## Architecture Layers

**Router Layer**

The Router layer handles communication between client applications and backend services.

Responsibilities:

- Defines API endpoints
- Receives HTTP requests
- Handles authentication dependencies
- Sends responses back to clients
- Connects API requests to business logic

Examples:

```
/users/
/permits/
/forest-zones/
/activities/
```

---

**Schema Layer**

Schemas define the structure of incoming requests and outgoing responses.

The backend uses Pydantic models for:

- Request validation
- Response formatting
- Data type checking
- API documentation generation

Examples:

```
UserCreate
UserResponse
PermitCreate
PermitRead
ForestZoneCreate
```

---

**Service Layer**

The service layer contains application business logic.

Responsibilities:

- Processing application rules
- Handling workflows
- Coordinating multiple operations
- Managing complex backend operations

Examples:

- Permit approval workflow
- Payment processing
- User registration logic

---

**Repository Layer**

The repository layer manages database operations.

Responsibilities:

- Creating database queries
- Retrieving records
- Updating records
- Deleting records

The repository layer communicates with PostgreSQL through SQLAlchemy.

---

**Database Layer**

The backend uses PostgreSQL as the main database.

SQLAlchemy provides:

- Database models
- ORM functionality
- Query management

Alembic manages database migrations.

Example migration command:

```bash
alembic upgrade head
```

---

## Security Architecture

The backend implements:

- JWT authentication
- Bearer token authorization
- Password hashing using bcrypt
- Role-based access control
- Rate limiting

User roles include:

- Super Admin
- Kenya Forest Service Official
- Community Forest Association Official
- Member

---

## Authentication Endpoints

Login User
POST `/auth/login`

Authenticates a user and generates access tokens.

Request:

```json
{
  "email": "user@example.com",
  "password": "password"
}
```

Response:

```json
{
  "access_token": "jwt-token",
  "refresh_token": "refresh-token",
  "token_type": "bearer"
}
```

---

**Forgot Password**

_POST `/auth/forgot-password`_

Initiates password recovery.

---

**Reset Password**

_POST `/auth/reset-password`_

Resets a user password using OTP verification.

---

### User Management

**Create User**

_POST `/users/`_

Creates a new user.

---

**Get Users**

_GET `/users/`_

Retrieves users.

---

**Get User**

_GET `/users/{user_id}`_

Retrieves a specific user.

---

**Update User**

_PATCH `/users/{user_id}`_

Updates user information.

---

**Delete User**

_DELETE `/users/{user_id}`_

Deletes a user.

---

**User Registration Endpoints**

| Endpoint                                            | Purpose                   |
| --------------------------------------------------- | ------------------------- |
| POST `/users/member`                                | Register community member |
| POST `/users/kenya-forest-service-official`         | Register KFS official     |
| POST `/users/community-forest-association-official` | Register CFA official     |

---

## Community Forest Associations

**Create CFA**

```
POST /community-forest-associations/
```

Creates a community forest association.

---

**List CFA**

```
GET /community-forest-associations/
```

Returns registered associations.

---

**Retrieve CFA**

```
GET /community-forest-associations/{cfa_id}
```

---

**Update CFA**

```
PATCH /community-forest-associations/{cfa_id}
```

---

**Delete CFA**

```
DELETE /community-forest-associations/{cfa_id}
```

---

## Forest Zones

Forest zones represent forest blocks and available resources.

---

**List Forest Zones**

```
GET /forest-zones/
```

---

**Create Forest Zone**

```
POST /forest-zones/
```

---

**Get Forest Zone**

```
GET /forest-zones/{zone_id}
```

---

**Update Forest Zone**

```
PUT /forest-zones/{zone_id}
```

---

**Delete Forest Zone**

```
DELETE /forest-zones/{zone_id}
```

---

**Resource Queries**

| Endpoint                                             | Purpose                 |
| ---------------------------------------------------- | ----------------------- |
| GET `/forest-zones/resources/{block_name}`           | Get resources by block  |
| GET `/forest-zones/available-resources/{block_name}` | Get available resources |

---

## Permit Management

**Create Permit**

```
POST /permits/
```

Creates a forest resource permit.

---

**List Permits**

```
GET /permits/
```

---

**Get Permit**

```
GET /permits/{permit_id}
```

---

**Update Permit**

```
PATCH /permits/{permit_id}
```

---

**Delete Permit**

```
DELETE /permits/{permit_id}
```

---

**Approve Permit**

```
POST /permits/{permit_id}/approve
```

---

**Member Permits**

```
GET /permits/member/{member_id}
```

Returns permits belonging to a member.

---

**Pending Payments**

```
GET /permits/payments/pending
```

---

## Payment Endpoints

**Initiate Permit Payment**

```
POST /permit-payments/{permit_id}
```

---

**Permit Payment Callback**

```
POST /permit-payments/callback
```

---

**Registration Payment**

```
POST /registration-payments/member/{member_id}
```

---

**Registration Payment Callback**

```
POST /registration-payments/callback
```

---

## Activities

Activities represent forest-related events and operations.

---

**Create Activity**

```
POST /activities/
```

---

**List Activities**

```
GET /activities/
```

---

**Upcoming Activities**

```
GET /activities/upcoming
```

---

**Activities By Zone**

```
GET /activities/zone/{zone_id}
```

---

**Retrieve Activity**

```
GET /activities/{activity_id}
```

---

**Update Activity**

```
PUT /activities/{activity_id}
```

---

**Delete Activity**

```
DELETE /activities/{activity_id}
```

---

## Tree Survival Tracking

Tracks survival rates of planted trees.

---

**Create Survival Log**

```
POST /tree-survival/
```

---

**List Survival Logs**

```
GET /tree-survival/
```

---

**Get Survival Log**

```
GET /tree-survival/{log_id}
```

---

**Update Survival Log**

```
PUT /tree-survival/{log_id}
```

---

**Delete Survival Log**

```
DELETE /tree-survival/{log_id}
```

---

## Incident Reporting

**Create Incident**

```
POST /incidents/
```

---

**List Incidents**

```
GET /incidents/
```

---

**Get Incident**

```
GET /incidents/{id}
```

---

**Update Incident**

## API Endpoints

The Rejesha Green API is organized into resource-based endpoint groups.

The API provides services for authentication, users, forest management, permits, payments, activities, reporting, and USSD communication.

---

### Authentication Endpoints

**Login User**

_POST `/auth/login`_

Authenticates a user and generates access tokens.

Request:

```json
{
  "email": "user@example.com",
  "password": "password"
}
```

Response:

```json
{
  "access_token": "jwt-token",
  "refresh_token": "refresh-token",
  "token_type": "bearer"
}
```

---

### Forgot Password

_POST `/auth/forgot-password`_

Initiates password recovery.

---

### Reset Password

_POST `/auth/reset-password`_

Resets a user password using OTP verification.

---

## User Management

**Create User**

_POST `/users/`_

Creates a new user.

---

**Get Users**

_GET `/users/`_

Retrieves users.

Supports pagination:

```
?skip=0&limit=100
```

---

**Get User**

_GET `/users/{user_id}`_

Retrieves a specific user.

---

**Update User**

_PATCH `/users/{user_id}`_

Updates user information.

---

**Delete User**

_DELETE `/users/{user_id}`_

Deletes a user.

---

## User Registration Endpoints

| Endpoint                                            | Purpose                   |
| --------------------------------------------------- | ------------------------- |
| POST `/users/member`                                | Register community member |
| POST `/users/kenya-forest-service-official`         | Register KFS official     |
| POST `/users/community-forest-association-official` | Register CFA official     |

---

### Community Forest Associations

**Create CFA**

```
POST /community-forest-associations/
```

Creates a community forest association.

---

**List CFAs**

```
GET /community-forest-associations/
```

Returns registered associations.

---

**Retrieve CFA**

```
GET /community-forest-associations/{cfa_id}
```

---

**Update CFA**

```
PATCH /community-forest-associations/{cfa_id}
```

---

**Delete CFA**

```
DELETE /community-forest-associations/{cfa_id}
```

---

### Forest Zones

Forest zones represent forest blocks and available resources.

---

**List Forest Zones**

```
GET /forest-zones/
```

---

**Create Forest Zone**

```
POST /forest-zones/
```

---

**Get Forest Zone**

```
GET /forest-zones/{zone_id}
```

---

**Update Forest Zone**

```
PUT /forest-zones/{zone_id}
```

---

**Delete Forest Zone**

```
DELETE /forest-zones/{zone_id}
```

---

### Resource Queries

| Endpoint                                             | Purpose                 |
| ---------------------------------------------------- | ----------------------- |
| GET `/forest-zones/resources/{block_name}`           | Get resources by block  |
| GET `/forest-zones/available-resources/{block_name}` | Get available resources |

---

## Permit Management

**Create Permit**

```
POST /permits/
```

Creates a forest resource permit.

---

**List Permits**

```
GET /permits/
```

---

**Get Permit**

```
GET /permits/{permit_id}
```

---

**Update Permit**

```
PATCH /permits/{permit_id}
```

---

**Delete Permit**

```
DELETE /permits/{permit_id}
```

---

**Approve Permit**

```
POST /permits/{permit_id}/approve
```

---

**Member Permits**

```
GET /permits/member/{member_id}
```

Returns permits belonging to a member.

---

**Pending Payments**

```
GET /permits/payments/pending
```

---

## Payment Endpoints

**Initiate Permit Payment**

```
POST /permit-payments/{permit_id}
```

---

**Permit Payment Callback**

```
POST /permit-payments/callback
```

---

**Registration Payment**

```
POST /registration-payments/member/{member_id}
```

---

**Registration Payment Callback**

```
POST /registration-payments/callback
```

---

## Activities

Activities represent forest-related events and operations.

---

**Create Activity**

```
POST /activities/
```

---

**List Activities**

```
GET /activities/
```

---

**Upcoming Activities**

```
GET /activities/upcoming
```

---

**Activities By Zone**

```
GET /activities/zone/{zone_id}
```

---

**Retrieve Activity**

```
GET /activities/{activity_id}
```

---

**Update Activity**

```
PUT /activities/{activity_id}
```

---

**Delete Activity**

```
DELETE /activities/{activity_id}
```

---

## Tree Survival Tracking

Tracks survival rates of planted trees.

---

**Create Survival Log**

```
POST /tree-survival/
```

---

**List Survival Logs**

```
GET /tree-survival/
```

---

**Get Survival Log**

```
GET /tree-survival/{log_id}
```

---

**Update Survival Log**

```
PUT /tree-survival/{log_id}
```

---

**Delete Survival Log**

```
DELETE /tree-survival/{log_id}
```

---

## Incident Reporting

**Create Incident**

```
POST /incidents/
```

---

**List Incidents**

```
GET /incidents/
```

---

**Get Incident**

```
GET /incidents/{id}
```

---

**Update Incident**

```
PUT /incidents/{id}
```

---

**Delete Incident**

```
DELETE /incidents/{id}
```

---

## USSD Services

**Handle USSD Request**

POST /ussd

Handles mobile USSD communication.

---

**Permit USSD Callback**

```
POST /permits/ussd/
```

Handles permit-related USSD callbacks.
PUT /incidents/{id}

---

**Delete Incident**

DELETE /incidents/{id}

---

## USSD Services

**Handle USSD Request**

POST /ussd

Handles mobile USSD communication.

---

**Permit USSD Callback**

POST /permits/ussd/

Handles permit-related USSD callbacks.

---

The Rejesha Green backend uses PostgreSQL as the primary database.

SQLAlchemy models represent the database entities while Pydantic schemas define API request and response structures.

---

## Main Entities

### User

Represents system users.

Fields include:

| Field                           | Description                    |
| ------------------------------- | ------------------------------ |
| user_id                         | Unique user identifier         |
| national_id                     | National identification number |
| first_name                      | User first name                |
| last_name                       | User last name                 |
| phone                           | Contact number                 |
| email                           | Email address                  |
| role                            | User role                      |
| membership_number               | Member identifier              |
| community_forest_association_id | Linked CFA                     |
| block_name                      | Forest block                   |
| is_active                       | Account status                 |

---

**User Roles**

Available roles:

| Role                                  |
| ------------------------------------- |
| super_admin                           |
| kenya_forest_service_official         |
| community_forest_association_official |
| member                                |

---

### Community Forest Association

Represents registered community forest organizations.

Fields:

| Field                             | Description           |
| --------------------------------- | --------------------- |
| community_forest_association_id   | Unique identifier     |
| community_forest_association_name | CFA name              |
| registration_fee                  | Membership fee        |
| is_active                         | Status                |
| created_at                        | Creation timestamp    |
| updated_at                        | Last update timestamp |

---

### Forest Zone

Represents forest blocks and available resources.

Fields:

| Field                           | Description         |
| ------------------------------- | ------------------- |
| zone_id                         | Zone identifier     |
| community_forest_association_id | Related CFA         |
| block_name                      | Forest block name   |
| resource_type                   | Available resource  |
| is_available                    | Availability status |
| resource_price                  | Resource price      |

---

### Permit

Represents resource access permits.

Fields:

| Field               | Description             |
| ------------------- | ----------------------- |
| permit_id           | Permit identifier       |
| member_id           | Requesting member       |
| forest_zone_id      | Related forest zone     |
| requested_resources | Requested resources     |
| permit_status       | Permit status           |
| payment_status      | Payment status          |
| phone_number        | Payment phone           |
| permit_number       | Generated permit number |

---

### Activity

Represents environmental activities.

Fields:

| Field              | Description           |
| ------------------ | --------------------- |
| activity_id        | Activity identifier   |
| created_by         | Creator               |
| zone_id            | Related forest zone   |
| activity_name      | Activity name         |
| scheduled_date     | Activity date         |
| description        | Activity details      |
| expected_attendees | Expected participants |
| actual_attendees   | Actual participants   |

---

### Tree Survival Log

Tracks planted tree survival.

Fields:

| Field           | Description      |
| --------------- | ---------------- |
| log_id          | Log identifier   |
| activity_id     | Related activity |
| trees_planted   | Number planted   |
| trees_surviving | Number surviving |
| dead_trees      | Number lost      |

---

### Incident Report

Stores reported forest incidents.

Fields:

| Field         | Description         |
| ------------- | ------------------- |
| incident_id   | Incident identifier |
| zone_id       | Related zone        |
| incident_type | Type of incident    |
| reported_at   | Report date         |

---

### Entity Relationships

```
User
 |
 | belongs to
 |
Community Forest Association
 |
 | manages
 |
Forest Zones
 |
 | generates
 |
Permits
 |
 | linked to
 |
Payments


Forest Zone
 |
 | contains
 |
Activities
 |
 | tracked by
 |
Tree Survival Logs
 |
 | reports
 |
Incidents
```

---

## Overview

The Rejesha Green backend uses automated testing and API validation practices to ensure that backend functionality works as expected.

The testing process focuses on:

- API endpoint correctness
- Request validation
- Database operations
- Authentication flows
- Business logic verification

---

## Testing Tools

The backend uses the following testing tools:

| Tool                | Purpose                   |
| ------------------- | ------------------------- |
| Pytest              | Automated backend testing |
| Swagger UI          | Manual API testing        |
| HTTPX               | API request testing       |
| FastAPI Test Client | Endpoint testing          |

---

### Running Tests

Run the complete test suite:

```bash
pytest
```

Run tests with detailed output:

```bash
pytest -v
```

---

## API Testing

The API can also be tested through Swagger UI.

Production:

```
https://rejesha-green-ff84657a60a9.herokuapp.com/docs
```

Local development:

```
http://localhost:8000/docs
```

Swagger allows developers to:

- View available endpoints
- Submit test requests
- Verify responses
- Test authentication

---

## Recommended Testing Areas

### Authentication Testing

Verify:

- Successful login
- Invalid credentials
- Token generation
- Protected endpoint access

---

### User Management Testing

Verify:

- User creation
- User retrieval
- User updates
- User deletion
- Role permissions

---

### Permit Testing

Verify:

- Permit creation
- Permit approval workflow
- Payment status updates
- Permit retrieval

---

### Data Validation Testing

Verify:

- Required fields
- Invalid data types
- Missing parameters
- Incorrect formats

---

## Quality Assurance Process

Before deployment:

1. Run automated tests
2. Verify database migrations
3. Test API endpoints
4. Validate authentication flows
5. Review application logs

---

### Overview

The Rejesha Green backend follows clean coding practices to improve maintainability, readability, and collaboration.

---

## Python Naming Conventions

### Files

Use lowercase names:

```
user_service.py
permit_repository.py
forest_zone_router.py
```

---

### Classes

Use PascalCase:

Example:

```python
class UserRepository:
    pass
```

---

### Functions and Variables

Use snake_case:

Example:

```python
def create_user():
    user_name = "John"
```

---

## Project Structure

The backend follows a layered organization:

```
app/
│
├── routers/
│
├── schemas/
│
├── services/
│
├── repositories/
│
├── models/
│
├── database/
│
└── core/
```

---

## Code Organization

### Routers

Responsible for:

- API endpoints
- Request handling
- Response formatting

---

### Schemas

Responsible for:

- Request validation
- Response models

---

### Services

Responsible for:

- Business rules
- Application workflows

---

### Repositories

Responsible for:

- Database queries
- CRUD operations

---

## Commit Message Format

Recommended commit format:

```
type: description
```

Examples:

```
feat: add permit approval endpoint

fix: resolve user login issue

docs: update API documentation

refactor: improve repository structure
```

---

### Recommended Commit Types

| Type     | Usage            |
| -------- | ---------------- |
| feat     | New feature      |
| fix      | Bug fix          |
| docs     | Documentation    |
| refactor | Code improvement |
| test     | Testing changes  |
| chore    | Maintenance      |

---

### Overview

The Rejesha Green backend is deployed as a production FastAPI application.

The production API documentation is available at:

```
https://rejesha-green-ff84657a60a9.herokuapp.com/docs
```

---

### Deployment Environment

Current production deployment:

| Component             | Technology |
| --------------------- | ---------- |
| Application Framework | FastAPI    |
| Server                | Uvicorn    |
| Database              | PostgreSQL |
| Migration Tool        | Alembic    |

---

### Production Requirements

The deployment environment requires:

- Python runtime
- PostgreSQL database
- Environment variables
- Installed backend dependencies
- Database migrations applied

---

# Deployment Process

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

### Configure Environment Variables

Example:

```env
DATABASE_URL=
SECRET_KEY=
ALGORITHM=
ACCESS_TOKEN_EXPIRE_MINUTES=
```

---

### Run Database Migrations

```bash
alembic upgrade head
```

---

### Start Application Server

Using Uvicorn:

```bash
uvicorn main:app
```

---

### Database Deployment

Database changes are managed using Alembic migrations.

Migration workflow:

Create migration:

```bash
alembic revision --autogenerate -m "migration message"
```

Apply migration:

```bash
alembic upgrade head
```

---

## Production

The production backend runs as a FastAPI application using Uvicorn and PostgreSQL, with Alembic responsible for database migrations. Deployment requires the production environment variables, backend dependencies, a reachable database, and an up-to-date database schema.

The deployment process consists of installing dependencies, configuring the production environment, applying database migrations, starting the application server, and verifying the deployed API. The production Swagger documentation can then be used to confirm that the API is available and its endpoints are responding correctly.

Production API: https://rejesha-green-ff84657a60a9.herokuapp.com

Swagger/OpenAPI: https://rejesha-green-ff84657a60a9.herokuapp.com/docs
