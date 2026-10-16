# CroMarket — Development Roadmap

_Under construction._ This document tracks the project's progress from concept to release. Check off each step as it is completed.

## Phase 1 — Requirements & Planning

- [ ] Define target users and use cases
- [ ] Write functional requirements
- [ ] Write non-functional requirements
- [ ] Select the tech stack
- [ ] Define the notification delivery channel
- [ ] Set scope for the first release

## Phase 2 — Database Modeling

- [ ] Define the core entities
- [ ] Establish relationships between entities
- [ ] Design tables
- [ ] Define interval rules: minimum **1 day**, maximum **90 days**
- [ ] Create the ER diagram
- [ ] Write the SQL schema

## Phase 3 — Core Logic

- [ ] Implement CRUD for items and categories
- [ ] Implement purchase logging
- [ ] Implement interval calculation
- [ ] Implement "next restock date" calculation
- [ ] Implement the due-items query

## Phase 4 — Reminders & Notifications

- [ ] Implement the notification service
- [ ] Trigger notifications when an item is due
- [ ] Allow users to customize reminder intervals
- [ ] Handle notification permissions on desktop and mobile

## Phase 5 — Desktop Web App

- [ ] Scaffold the web frontend
- [ ] Shopping list view
- [ ] Item + category management views
- [ ] Purchase logging view
- [ ] Settings view

## Phase 6 — Mobile App (Proprietary)

- [ ] Scaffold the mobile application
- [ ] Reuse the backend API
- [ ] Shopping list, item management, and purchase logging screens
- [ ] Native push notifications

## Phase 7 — Testing & QA

- [ ] Unit tests for interval and quantity logic
- [ ] Integration tests for the database
- [ ] API tests
- [ ] Manual testing on desktop and mobile

## Phase 8 — Deployment

- [ ] Set up hosting for the backend and database
- [ ] Publish the desktop web app
- [ ] Release the mobile app
- [ ] Write user documentation
