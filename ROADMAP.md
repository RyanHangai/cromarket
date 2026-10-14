# CroMarket — Development Roadmap

_Under construction._ This document tracks the project's progress from concept to release. Check off each step as it is completed.

## Phase 1 — Requirements & Planning

- [ ] Define target users and use cases
- [ ] Write functional requirements (what the app does)
- [ ] Write non-functional requirements (performance, security, offline use)
- [ ] Choose the platforms: desktop **web app** and **proprietary mobile app**
- [ ] Select the tech stack (Python, SQL, frontend framework)
- [ ] Define the notification delivery channel (push, desktop, in-app)
- [ ] Set scope for the first release (MVP)

## Phase 2 — Database Modeling

- [ ] Define the core entities (Items, Categories, Purchases, Reminders, Users)
- [ ] Establish relationships between entities (1-to-many, many-to-many)
- [ ] Design the `items` table (name, category, interval, quantity)
- [ ] Design the `categories` table (dairy, produce, pantry, etc.)
- [ ] Design the `purchases` table (item, quantity, date purchased)
- [ ] Define interval rules: minimum **1 day**, maximum **90 days**
- [ ] Define the quantity scaling rule (more units → longer interval)
- [ ] Create the ER diagram
- [ ] Write the SQL schema / migrations

## Phase 3 — Core Logic

- [ ] Implement CRUD for items and categories
- [ ] Implement purchase logging
- [ ] Implement interval calculation (interval × quantity)
- [ ] Implement "next restock date" calculation
- [ ] Implement the due-items query (what to buy today)

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
- [ ] Settings view (intervals, notifications)

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
