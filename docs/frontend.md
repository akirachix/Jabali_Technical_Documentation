# Frontend Web

## Overview

The Jabali Dashboard web application is the web-based interface for Kenya Forest Service (KFS) officers to monitor and manage forest conservation and restoration activities.

The frontend provides a centralized dashboard where authorized users can access information about:

- Forest activities
- Reported incidents
- CFA members
- Resource permits
- Reforestation activities and logs
- KFS officer registration
- Application settings

The interface is designed to make forest management information easier to view, monitor, and analyze through dashboards, summary information, charts, and other visual components.



## Frontend Architecture

The web frontend is built using **Next.js and React**.

The application uses the Next.js `app` directory structure, where pages and layouts are organized according to application routes.

### Main Frontend Structure

```text
JABALI_DASHBOARD/
│
├── app/
│   ├── Auth/
│   │   ├── forgot-password/
│   │   ├── login/
│   │   │   └── page.jsx
│   │   └── sign-up/
│   │       └── page.jsx
│   │
│   ├── components/
│   │   ├── Navigation/
│   │   │   └── navigation.jsx
│   │   └── TopNavbar/
│   │
│   ├── dashboard/
│   │   └── reforestationLogs/
│   │       └── settings/
│   │
│   ├── forestActivities/
│   │
│   ├── incidentReport/
│   │   └── page.jsx
│   │
│   ├── memberRegistry/
│   │   └── page.jsx
│   │
│   ├── overview/
│   │   └── page.jsx
│   │
│   ├── permitManagement/
│   │   └── page.jsx
│   │
│   ├── reforestationLogs/
│   │   └── page.jsx
│   │
│   ├── register-kfs-official/
│   │
│   ├── settings/
│   │   ├── layout.jsx
│   │   └── page.jsx
│   │
│   ├── globals.css
│   ├── layout.jsx
│   ├── page.jsx
│   └── page.tsx
│
├── components/
├── public/
├── package.json
├── package-lock.json
├── next.config.ts
├── next-env.d.ts
├── tsconfig.json
└── README.md
```

> The structure may change as new features are added. Route names and folders should remain consistent with the feature they represent.

---

## User Role

The primary user of the dashboard frontend is the:

**KFS Officer**

KFS officers use the web dashboard to:

- View forest management information
- Monitor reported incidents
- Review CFA member information
- Monitor resource permit requests
- Review reforestation information
- Monitor forest restoration activities
- Access application settings

---

##Authentication

The application contains authentication-related pages under the `Auth` directory.

**Login**

**Route:**

```text
/Auth/login
```

The login page provides the interface through which authorized users access the dashboard.

*Main responsibilities*

- Accept user credentials
- Validate authentication information
- Provide access to the dashboard after successful authentication
- Display appropriate feedback when authentication fails

**Sign Up**

**Route:**

```text
/Auth/sign-up
```

The sign-up page provides an interface for creating a user account where registration is permitted.

**Forgot Password**

**Route:**

```text
/Auth/forgot-password
```

This page supports the password recovery process.

---

## Dashboard Interface

The dashboard is the main working area of the web application.

It provides access to the major forest management modules through a consistent navigation layout.

**Dashboard Layout**

The interface is organized around:

1. Navigation sidebar
2. Top navigation bar
3. Main content area
4. Feature-specific dashboard pages

---

## Navigation Sidebar

The navigation component provides access to the main sections of the application.

The navigation is implemented as a reusable component under:

```text
app/components/Navigation/
```

*Main Navigation Items*

- Overview
- Incident Reports
- CFA Member Registry
- Forest Activities
- Permit Management
- Reforestation Logs
- Settings

The sidebar allows users to move between modules without having to manually enter routes.

---

## Top Navigation Bar

The top navigation bar provides common controls and information that are shared across dashboard pages.

It is implemented as a reusable frontend component.

Example structure:

```text
app/components/
└── TopNavbar/
```

The top navigation is designed to remain consistent across the dashboard and reduce duplication between pages.

---

## Dashboard Overview

The **Overview** page provides a high-level summary of forest management information.

**Route:**

```text
/overview
```

The overview can contain summary cards and visualizations representing important operational information.

**Information displayed**

- CFA member statistics
- Incident information
- Permit activity
- Reforestation progress
- Forest restoration activities

The overview page is intended to help KFS officers quickly understand the current state of the system.

---

## CFA Member Registry

The CFA Member Registry provides access to information about registered Community Forest Association (CFA) members.

**Route:**

```text
/memberRegistry
```

**Purpose**

The module allows officers to view and monitor registered members.

**Possible information displayed**

- Member registration information
- Member status
- Registration statistics
- Other relevant member information provided by the backend

---

## Incident Reports

The Incident Report module provides an interface for viewing reported forest-related incidents.

**Route:**

```text
/incidentReport
```

**Purpose**

The module helps KFS officers monitor reported activities that may require attention or intervention.

*Example incident categories*

- Logging
- Poaching
- Charcoal burning
- Other illegal forest activities

**Interface**

Incident information can be presented using:

- Summary information
- Tables
- Charts
- Location information
- Incident status

The frontend is responsible for presenting the information received from the backend API.

---

## Forest Activities

The Forest Activities module provides information about conservation and forest management activities.

**Route:**

```text
/forestActivities
```

*Example activities*

- Tree planting
- Forest patrols
- Clearing weeds
- Removing invasive plants
- Other restoration activities

The module can use visualizations to show how activities are distributed and monitored.

---

## Permit Management

The Permit Management module is used to monitor forest resource requests and permits.

**Route:**

```text
/permitManagement
```

**Purpose**

The page provides officers with a view of resource requests and their permit-related status.

*Resources monitored*

- Firewood
- Grass
- Bamboo
- Honey
- Medicinal plants

*Example information*

- Resource requests
- Approved requests
- Pending requests
- Rejected requests
- Permit activity trends

---

## Reforestation Logs

The Reforestation Logs module provides information about forest restoration and tree planting activities.

**Route:**

```text
/reforestationLogs
```

**Information monitored**

- Trees planted
- Surviving trees
- Deceased trees
- Restoration progress

The information can be presented using summary cards, tables, and charts to make restoration progress easier to understand.

---

## KFS Official Registration

The application includes a page for registering KFS officials.

**Route:**

```text
/register-kfs-official
```

The page provides the frontend form used to collect the required information for registering a KFS official.

---

## Settings

The Settings module provides access to application and user-related configuration.

**Route:**

```text
/settings
```

The settings interface is separated into its own layout and page components:

```text
settings/
├── layout.jsx
└── page.jsx
```

Using a separate layout allows settings-related pages to share a common structure.

---

## Reusable Frontend Components

Reusable components are used to avoid duplicating UI code across different pages.

Examples include:

```text
app/components/
├── Navigation/
│   └── navigation.jsx
└── TopNavbar/
```

**Benefits**

Reusable components help to:

- Maintain a consistent interface
- Reduce code duplication
- Make changes easier to manage
- Improve maintainability
- Provide consistent navigation across pages

---

## Frontend Technology Stack

| Technology | Purpose |
| --- | --- |
| Next.js | Frontend framework and application routing |
| React | Building reusable user interface components |
| JavaScript / JSX | Frontend application logic and components |
| TypeScript | Type-safe configuration and selected frontend files |
| CSS | Application styling and responsive layouts |
| Global CSS | Shared styling across the application |
| Chart.js / React Chart.js | Data visualization where applicable |
| npm | Dependency management and frontend scripts |

> **Note:** The project uses CSS/global CSS for styling. Tailwind CSS is not part of the current frontend implementation.

---

## Styling and Design

The frontend follows a consistent visual design based on the Jabali/Rejesha Green branding.

The design uses:

- Green as the primary brand color
- Orange as a supporting accent color
- Consistent typography
- Cards and dashboard sections
- Clear spacing and layout
- Responsive components
- Consistent navigation

Shared styles are maintained in:

```text
app/globals.css
```

The frontend design was developed to keep the dashboard clear and easy to navigate for KFS officers.

---

## Data Visualization

The dashboard uses visual data representations where appropriate.

Examples include:

- Bar charts
- Line charts
- Summary cards
- Activity distribution charts
- Progress indicators
- Tables

Charts are used to make trends and statistics easier to understand rather than presenting all information as raw data.

---

## Backend API Integration

The frontend communicates with the backend API to retrieve and submit application data.

The backend is implemented using **FastAPI**.

The frontend is responsible for:

1. Sending requests to the API.
2. Receiving API responses.
3. Processing the returned data.
4. Displaying the data in the appropriate interface.
5. Handling loading and error states.

Example frontend request pattern:

```javascript
const response = await fetch(`${API_URL}/endpoint`);

if (!response.ok) {
  throw new Error("Failed to fetch data");
}

const data = await response.json();
```

The actual API endpoints should be documented separately as the backend API develops.

---

## Responsive Design

The frontend is designed to remain usable across different screen sizes.
**Design considerations**

- Flexible dashboard layouts
- Responsive navigation
- Readable typography
- Appropriate spacing
- Responsive charts
- Accessible buttons and controls
- Consistent layout across pages

The goal is to ensure that the dashboard remains usable on desktop and smaller screens where applicable.

---

## Accessibility

Accessibility considerations include:

- Clear text hierarchy
- Readable typography
- Sufficient visual contrast
- Meaningful button labels
- Consistent navigation
- Clear form labels
- Feedback for user actions
- Keyboard-friendly interface elements where applicable

Accessibility should be considered when adding new components or modifying existing pages.

---

## Code Standards

**Components**

Functional React components are used throughout the frontend.

Example:

```jsx
function DashboardCard() {
  return (
    <div>
      <h2>Dashboard</h2>
    </div>
  );
}

export default DashboardCard;
```

Components should be separated according to their responsibility or feature.

---

## Naming Conventions

**Components**

Use **PascalCase**.

```text
DashboardCard.jsx
IncidentChart.jsx
Navigation.jsx
TopNavbar.jsx
```

**Variables and Functions**

Use **camelCase**.

```javascript
const userData = {};
const incidentData = [];

function fetchIncidents() {}
```

**Constants**

Use **SCREAMING_SNAKE_CASE** for application-wide constants where appropriate.

```javascript
const API_BASE_URL = "...";
```

### Folders and Routes

Use descriptive feature names.

```text
incidentReport/
memberRegistry/
permitManagement/
reforestationLogs/
forestActivities/
```

---

## Error and Loading States

Frontend pages that communicate with the backend should account for different API states.

*Loading state*

Display an appropriate loading indicator while information is being retrieved.

*Error state*

Display a clear message when data cannot be retrieved.

Example:

```jsx
if (loading) {
  return <p>Loading...</p>;
}

if (error) {
  return <p>Unable to load data.</p>;
}
```

*Empty state*

If the API returns no records, the interface should clearly communicate that no data is currently available.

---

## Frontend Development Workflow

Development follows a feature-based Git workflow.

A typical workflow is:

```text
1. Create a feature branch
2. Develop the frontend feature
3. Test the feature locally
4. Review the changes
5. Commit the changes
6. Push the feature branch
7. Create a Pull Request
8. Review and merge the Pull Request
```

Example branch:

```bash
git checkout -b feature/incident-report
```

Example commit:

```bash
git add .
git commit -m "feat: update incident report dashboard"
git push -u origin feature/incident-report
```

---

## Running the Frontend Locally

From the `JABALI_DASHBOARD` project directory:

**Install dependencies**

```bash
npm install
```

**Start the development server**

```bash
npm run dev
```

The application is normally available at:

```text
http://localhost:3000
```

The development server automatically reloads when frontend files are changed.

---

## Production Build

Before deployment, the application can be checked using a production build.

```bash
npm run build
```

If the build completes successfully, the application can be started using:

```bash
npm start
```

---

## Environment Variables

Environment-specific values should be stored in environment files rather than hard-coded into components.

Example:

```text
.env.local
```

For example:

```text
NEXT_PUBLIC_API_URL=<backend-api-url>
```

Environment files containing secrets or private configuration should not be committed to Git.

The project's `.gitignore` should exclude local environment files where appropriate.

---

## Deployment

The Next.js frontend is deployed using **Vercel**.

### Deployment workflow

```text
Developer
   │
   ▼
Feature Branch
   │
   ▼
Pull Request
   │
   ▼
Code Review
   │
   ▼
Merge to main
   │
   ▼
Vercel Build
   │
   ▼
Production Deployment
```

The production deployment should be connected to the repository's `main` branch.

---

## Frontend Maintenance

When adding a new frontend feature:

1. Create a feature branch.
2. Create the required route/page.
3. Reuse existing components where possible.
4. Follow the established naming conventions.
5. Keep styling consistent with `globals.css`.
6. Connect the page to the appropriate API endpoint.
7. Add loading, error, and empty states.
8. Test the page locally.
9. Check the responsive layout.
10. Commit and push the changes.
11. Create a Pull Request for review.

---

## Future Frontend Improvements

Possible future improvements include:

- Improved dashboard filtering
- More interactive charts
- Advanced incident visualization
- Improved mobile responsiveness
- Role-based frontend access control
- Better loading and error states
- Expanded accessibility support
- Additional dashboard analytics
- Improved API error handling
- Automated frontend testing

---

## Summary

The Jabali Dashboard frontend provides a centralized web interface for KFS officers to monitor forest conservation and restoration activities.

The application is built with **Next.js and React**, uses reusable components for navigation and shared UI, and communicates with the FastAPI backend to retrieve and manage application data.

The main frontend modules include:

- Authentication
- Dashboard Overview
- Incident Reports
- CFA Member Registry
- Forest Activities
- Permit Management
- Reforestation Logs
- KFS Official Registration
- Settings

The frontend follows a modular structure so that individual features can be developed, tested, and maintained independently.