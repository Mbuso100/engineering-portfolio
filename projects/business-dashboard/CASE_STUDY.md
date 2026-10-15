# Business Dashboard & Admin Portal

I began this project by building a reusable foundation for business applications: authenticated users, company records, role-aware administration, basic activity tracking and a dashboard shell. The goal was to avoid rebuilding those cross-cutting concerns for every operational application.

## The problem

**Uncontrolled access and scattered administration put business records at risk.**

A dashboard can display useful figures while leaving basic questions unanswered: who is allowed to view a company's records, who can manage accounts, and how administrative changes are tracked? Hiding controls in the interface is not enough to enforce those boundaries.

A dependable application needs consistent identity, company context and permission checks before client-specific workflows and reports are added.

## The solution

**A reusable foundation for company-scoped business applications**

The starter establishes a React and TypeScript interface with sign-in, a business overview, users and company settings. Its FastAPI backend implements authentication, company-scoped user queries, role checks, administrative actions and basic activity records. SQLAlchemy provides persistence, with PostgreSQL as the intended deployed database and SQLite for local development.

## Decisions behind the foundation

### Recheck identity against the database

The API validates the incoming JWT against an active user record and checks the associated company claim. Backend dependencies enforce Owner/Admin access to user administration. The user-update endpoint also checks the number of active Owners before allowing the last one to be disabled or demoted.

### Separate business-specific workflows

The company, location, user and audit entities are meant to support later operational modules without embedding restaurant or inventory terminology into the foundation. The Inventory Management application builds on that underlying approach.

### Put schema changes under migration control

The later development of this foundation uses Alembic rather than treating application startup as the deployment migration process. That separation matters when data must survive releases.

## Verification and scope

The archived starter source includes authentication, administrative endpoints and a small initial frontend. Its automated test file checks the health endpoint; it does **not** establish comprehensive automated coverage of the foundation in that early snapshot. Later inventory-development records exercise the evolved shared foundation, but those tests should not be presented as if they all belonged to the original starter release.

The recorded dashboard and admin-portal videos illustrate the user-facing direction of this application. Some UI details were developed beyond the early starter archive; I distinguish the demonstrated interface from the particular source snapshot reviewed here.

## What I would improve

I would expand targeted authentication/authorization tests on this standalone starter, verify migration and deployment paths, and replace localStorage JWT handling with an evaluated session strategy appropriate to the threat model. I would also keep admin activity logs structured and make recovery and user offboarding explicit.

## Implementation

**Backend:** Python, FastAPI, SQLAlchemy, JWT-based authentication and role checks.  
**Frontend:** React, TypeScript, Vite.  
**Data model:** companies, locations, users and audit events.

## Demonstration

[Watch the Business Dashboard demonstration](../../assets/media/business-dashboard-demo.mp4) · [View the overview recording](../../assets/media/business-dashboard-overview.mp4)

- [Dashboard](../../assets/media/business-dashboard-screen-1.webp)
- [Users](../../assets/media/business-dashboard-screen-2.webp)
- [Company settings](../../assets/media/business-dashboard-screen-3.webp)

The source belongs to Ndlovu Business Technologies and is not included in this public portfolio.
