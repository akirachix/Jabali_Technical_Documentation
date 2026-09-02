## Architecture Overview

Rejesha Green is a digital forest management platform that
connects CFA officials, CFA members and KFS officials through mobile,
web and USSD/SMS interfaces.

The system uses a centralized backend API to process requests,
manage application data and communicate with external services.

<div class="architecture-note">

<strong>Interactive SAD:</strong>

The editable System Architecture Diagram is available in LucidSpark.

<br>

<a
  href="https://lucid.app"
  target="_blank"
  class="md-button">
Open SAD in LucidSpark
</a>

</div>

<div class="diagram-card">

<img
src="/assets/brand/SAD.png"
alt="Rejesha Green System Architecture Diagram"
class="diagram-image"
>

<p class="diagram-caption">
  Figure 1: Rejesha Green System Architecture Diagram
</p>

</div>

## User Flows

The user flows illustrate how CFA officials and CFA members interact
with the Rejesha Green platform across the different system
functions.

<div class="architecture-note">

<strong>Interactive User Flow:</strong>

The complete user flow is available in the Miro board below.

<br>

<a
  href="https://miro.com"
  target="_blank"
  class="md-button">
Open User Flows in Miro
</a>

</div>

### CFA Official User Flow

<div class="diagram-card">

<img
src="/assets/brand/cfa-official-flow.png"
alt="CFA Official User Flow"
class="diagram-image"
>

<p class="diagram-caption">
  Figure 3: CFA Official User Flow
</p>

</div>

### CFA Member User Flow

<div class="diagram-card">

<img
src="/assets/brand/cfa-member-flow.png"
alt="CFA Member User Flow"
class="diagram-image"
>

<p class="diagram-caption">
  Figure 4: CFA Member User Flow
</p>

</div>

## Main System Components

<div class="component-grid">

<div class="component-card">

<h3>Mobile Application</h3>

<p>
Provides the main interface for CFA officials and members to access
platform services.
</p>

</div>

<div class="component-card">

<h3>USSD / SMS</h3>

<p>
Provides an alternative access channel for community members using
basic mobile phones.
</p>

</div>

<div class="component-card">

<h3>Rejesha Green API</h3>

<p>
Handles application requests, business logic, data processing and
communication with external services.
</p>

</div>

<div class="component-card">

<h3>Database</h3>

<p>
Stores users, forest zones, permits, incidents, activities and
reforestation records.
</p>

</div>

<div class="component-card">

<h3>Web Dashboard</h3>

<p>
Provides KFS officials with centralized monitoring, reporting and
analytics capabilities.
</p>

</div>

<div class="component-card">

<h3>External Services</h3>

<p>
Integrates with Daraja for M-Pesa payments and Africa's Talking for
SMS and USSD communication.
</p>

</div>

</div>

## Technology Stack

| Component          | Technology       | Purpose                     |
| ------------------ | ---------------- | --------------------------- |
| Mobile Application | Flutter / Dart   | Mobile user interface       |
| State Management   | Provider         | Application state           |
| API Communication  | Dio / HTTP       | REST API communication      |
| Web Dashboard      | Next.js / React  | KFS web interface           |
| Backend            | REST API         | Business logic and services |
| Database           | SQL              | Persistent data storage     |
| Payments           | Safaricom Daraja | M-Pesa payments             |
| Communication      | Africa's Talking | SMS / USSD                  |

## Interface Screens

<div class="screenshot-grid">

<figure>
  <img
    src="/assets/brand/member-registration.png"
    alt="Mobile Dashboard"
  >
  <figcaption>CFA home page</figcaption>
</figure>

<figure>
  <img
    src="/assets/brand/activities.png"
    alt="forest activities"
  >
  <figcaption>Forest activities creation </figcaption>
</figure>

<figure class="dashboard-screenshot">

<img
src="/assets/brand/web-dashboard.png"
alt="KFS Web Dashboard"
class="expandable-image"
>

  <figcaption>
    KFS Web Dashboard
  </figcaption>

</figure>

</div>

## Architecture Summary

The architecture provides multiple access channels while maintaining
a centralized backend and database. Mobile and USSD/SMS interfaces
allow users to access services, while the API coordinates business
logic, persistence, payments and communication. The web dashboard
provides KFS officials with centralized visibility into forest
management operations.

