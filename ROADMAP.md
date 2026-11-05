# CroMarket — Development Roadmap

This document tracks the project's progress from concept to release. Check off each step as it is completed. References like BR-01 point to the [business rules](docs/business-rules/business-rules.md).

## Phase 1 — Requirements & Planning

- [x] Create the repository with license and README (EN and PT-BR)
- [x] Write the business rules (EN and PT-BR)
- [x] Choose the platform order: mobile app first, then web app
- [x] Define the notification channels: push alerts and in-app notices
- [x] Choose the base: Python and Docker
- [ ] Define target users and use cases
- [ ] Write non-functional requirements (performance, security, privacy of minors' data under LGPD)
- [ ] Decide the offline scope: view-only, or editing too
- [ ] Select the rest of the stack: database engine, API framework, mobile framework, web framework, cloud provider
- [ ] Define the MVP scope
- [ ] Define the team workflow: branches, pull requests, commit convention (`CONTRIBUTING.md`)

## Phase 2 — Database Modeling

- [ ] Define the core entities: workspace, member, product, package, batch, consumption period, shopping list, purchase, notification, activity log
- [ ] Establish relationships between entities
- [ ] Decide how records are identified (UUID or auto-increment) and how changes are tracked (`updated_at`, soft delete)
- [ ] Decide which values are stored and which are calculated (stock, run-out date)
- [ ] Model consumption as periods that are never edited retroactively (BR-07)
- [ ] Create the ER diagram
- [ ] Write the data dictionary
- [ ] Write the SQL schema / migrations
- [ ] Prepare seed data: default shelf lives and packages, with their sources (BR-05)

## Phase 3 — Backend & Infrastructure

- [ ] Set up the Python project structure
- [ ] Create the Docker setup (`Dockerfile`, `docker-compose`, `.env.example`)
- [ ] Set up the API used by the mobile and web apps
- [ ] Implement authentication and workspace access
- [ ] Set up automated checks on pull requests (CI)

## Phase 4 — Core Logic

- [ ] CRUD for workspaces, members, and roles (BR-10)
- [ ] CRUD for products and packages (BR-08)
- [ ] Shopping list and purchase flow: check items, finish the list, create batches (BR-11)
- [ ] Daily stock calculation, including the 4 p.m. cutoff (BR-01)
- [ ] Consumption order across batches, earliest expiry first (BR-06)
- [ ] Expired batches (BR-02)
- [ ] Default shelf lives and user adjustments (BR-05)
- [ ] Consumption changes and schedules, including overlaps (BR-07)
- [ ] Run-out date and expiry date calculation
- [ ] Automatic entry into the next purchases list (BR-09)
- [ ] Teen changes pending adult validation (BR-10)
- [ ] Activity log: who changed what

## Phase 5 — Notifications

- [ ] Daily scheduler that finds the notifications due
- [ ] Alerts (push) and notices (in app) for restocking and expiration (BR-03)
- [ ] Configurable advance notice: first alert, second alert, and an optional third (BR-04)
- [ ] Same-day duplicates and alerts whose date has already passed (BR-04)
- [ ] Notifications tab: pending validations for adults, activity log for guardians (BR-10)
- [ ] Push notification permissions on mobile

## Phase 6 — Mobile App

- [ ] Scaffold the mobile application
- [ ] Connect to the backend API
- [ ] Shopping list screens: checklist and finishing the list
- [ ] Stock and batch screens, with the calendar history
- [ ] Consumption and schedule screens
- [ ] Workspace, members, and settings screens (time zone, advance notices)
- [ ] Notifications tab and native push

## Phase 7 — Web App

- [ ] Scaffold the web frontend
- [ ] Connect to the backend API
- [ ] Shopping list, stock, and batch views
- [ ] Consumption and schedule views
- [ ] Workspace, members, and settings views
- [ ] Notifications tab

## Phase 8 — Testing & QA

Unit tests are written together with the logic in Phases 4 and 5. This phase checks everything working together.

- [ ] Unit tests built from the examples in the business rules (BR-01 to BR-11)
- [ ] Edge cases: time zones, same-day alerts, overlapping schedules, expired batches
- [ ] Integration tests for the database
- [ ] API tests
- [ ] Manual testing on mobile and desktop

## Phase 9 — Deployment

- [ ] Host the backend and database with Docker
- [ ] Publish the web app
- [ ] Release the mobile app (stores or direct install)
- [ ] Write user documentation

## Future ideas (after the MVP)

- Partial offline use: view-only first, then editing with sync
- Recognize the product, brand, and expiry date from a photo, using an AI model
- Times (not only dates) in consumption schedules