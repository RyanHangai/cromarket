# CroMarket
__Under construction__

Built with Python and SQL that automates your shopping list and reminds you when to restock items.

## Overview

CroMarket is a shopping assistant that keeps track of what you buy and tells you when it's time to buy it again. Instead of maintaining a static shopping list by hand, you simply log each item whenever you purchase it. CroMarket then uses that purchase history, combined with a restock interval you choose, to calculate the next date the item should appear on your list.

The idea is simple: the rhythm at which you consume a product determines when you need more of it. If you buy milk once a week, CroMarket will remind you to restock it every week. It turns shopping into a self-maintaining cycle — **purchase, record, wait, get reminded, purchase again** — so you stop running out of the things you actually use.

CroMarket is designed to run on the devices you already carry:

- **Desktop** — available as a **web app**, accessible from any modern browser.
- **Mobile** — available as a **proprietary mobile application** built for phones and tablets.

## Features

- **Automated Tracking**: Log items whenever you purchase them.
- **Reminders**: Get a **notification** when an item is due to be restocked, based on its interval.
- **Configurable Intervals**: Set a custom restock time per item, with a minimum of **1 day** and a maximum of **90 days**.
- **Quantity & Stock**: Track how many units you buy and scale the restock interval accordingly. Buying more of an item makes it last longer before the next reminder.
- **Item Categories**: Organize products by type (dairy, produce, pantry, etc.).

## How Intervals and Quantity Work

Each item has a restock interval that you define yourself, anywhere between **1** and **90 days**. The interval is then scaled by the **quantity** you purchased: buying more units lasts proportionally longer, so the next reminder is pushed further out.

| Item | Quantity bought | Interval per unit | Next reminder |
| ---- | --------------- | ----------------- | ------------- |
| Milk | 1               | 1 week            | 1 week later  |
| Milk | 2               | 1 week            | 2 weeks later |

In other words, if one carton of milk lasts you a week, buying two means you won't need more for two weeks.

## Roadmap

See [`ROADMAP.md`](ROADMAP.md) for the step-by-step development plan, from requirements and database modeling through to release.
