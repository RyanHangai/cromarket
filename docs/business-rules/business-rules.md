<h1 align="center">Business Rules</h1>

<p align="center">
    <a href="../business-rules/regras-de-negocio.md">🇧🇷 Português</a>
</p>

## 1. Objective

Many people still write their shopping list by hand, on paper, and only notice something has run out or expired when it is already too late. CroMarket records what the household buys, calculates when each product will run out or expire, and sends reminders in advance, so the whole family can plan their shopping trip.

## 2. Glossary

| Term | Definition | Example |
|---|---|---|
| **Workspace** | A household's shared space. Stock, consumption, shelf lives, time zone, and the shopping list belong to it. Any change applies to the whole workspace and every member sees it. | The Silva family uses a single workspace. |
| **Member** | A person who belongs to a workspace. Has a role. | Ana, João, and Pedro. |
| **Role** | Defines what the member can do: **adult** edits everything; **teen** can edit, but the change only takes effect after an adult validates it; **child** can only view. | Ana is an adult; João is a teen. |
| **Guardian** | An adult who manages the workspace: the creator and, if they wish, one more adult they designate. Follows everything that happens in the workspace in the notifications tab. | Ana (the creator) is a guardian. |
| **Product** | A type of thing that is bought and tracked. | Milk. |
| **Item** | One unit of a product, in the measure in which it is counted (unit, kg, or liter). | 1 carton of milk. |
| **Package** | The form in which a product is bought, with the number of items it contains. Each product has an editable default package. | A box of 12 milk cartons (default); a box of 6 (another brand). |
| **Batch** | A group of items of the same product bought together. It has its own purchase date, brand, expiry date, and stock. | The box of milk bought on Oct 12. |
| **Stock** | The quantity of items of a batch (or product) still at home. | The Oct 12 batch has 5 cartons left. |
| **Consumption** | How much of the product the workspace uses per day. Can be entered directly or as "lasts N days". Accepts decimals in any measure. | 130 g of shampoo per day. |
| **Availability** | How many days the stock lasts: stock ÷ consumption per day. | 6 milks ÷ 1 per day = 6 days. |
| **Run-out date** | The day the last item of the product is consumed (stock reaches zero at the end of that day). | Consumption starts on Oct 12 with 6 days of availability: runs out on Oct 17. |
| **Default shelf life** | How many days, on average, a product lasts before expiring. It comes from research across several sources and can be adjusted. | Milk: 120 days. |
| **Expiry date** | The last day the batch is fit for consumption: purchase date + shelf life (or the date printed on the package). | Oct 12 + 120 days = Feb 9. |
| **Advance notice** | How many days before an event (run-out or expiry) the app sends each alert. Default: 2 days and 1 day, with an optional third. | Notify 2 days and 1 day before running out. |
| **Alert** | A push notification on the device, for what is urgent; it also appears as a notice in the app's notifications tab. Priority Level 1. | "Your milk runs out in 2 days." |
| **Notice** | A notification that appears only inside the app, in the notifications tab; it only advises and leaves a record. Priority Level 2. | "The milk ran out and was added to your shopping list." |
| **Next purchases list** | The list of products that need to be bought, with a checklist to mark what was bought. | Milk, rice, shampoo. |

## 3. Rules

### BR-01: Consumption reduces stock

**Rule.** Consumption is counted per day against the product's total stock and reduces it daily. Consumption is a rate and accepts decimals in any measure (for example, 0.6 unit per day). Stock never goes below zero. Consumption starts on the purchase day. Exception: if the product's stock was zero, a purchase made **after 4 p.m.** (workspace time zone) only starts being consumed the next day. If there was still stock, the purchase time makes no difference. This is the only rule that uses times; the rest of the app works with dates only.

**Formula.** Stock at the end of day D = quantity purchased − sum of the consumption of each counted day, from the first consumption day through D (inclusive).

**Example.** 6 milks bought on Oct 12 at 10 a.m., consumption of 1 per day. At the end of Oct 12, 5 are left; at the end of Oct 13, 4; and so on. If the purchase were at 5 p.m. with zero stock, the end of Oct 12 would still show 6, and consumption would start on Oct 13.

### BR-02: An expired batch sets stock to zero and preserves history

**Rule.** The expiry date itself is still valid for consumption. On the following day, the batch's remaining stock goes to zero, the batch gets the status "expired", and it stays in the history. The app recommends discarding what is left. An expired batch is not consumed.

**Example.** A batch with an expiry date of Feb 9 and 2 items left: on Feb 9 it can still be consumed; on Feb 10 the batch's stock goes to 0, its status becomes "expired", and the app tells the user to discard it.

### BR-03: Restocking and expiration notifications

**Rule.** Both event types (restocking and expiration) follow the same pattern:

1. **Alerts** at the configured advance notices (BR-04). By default, 2 days and 1 day before the event;
2. On the day of the event, only a **Notice**, to avoid bothering the user.

- **Restocking** (per product): the event is the run-out date.
- **Expiration** (per batch): the event is the expiry date, and the notifications only exist if the batch still has stock on that day. If the batch runs out before expiring, they no longer exist.

Every Alert is a push notification and also appears as a Notice in the app's notifications tab; a Notice appears only in the app. Alerts are for what is urgent; a notice only advises and leaves a record.

Whenever a purchase or a consumption change moves the run-out date, the restocking notifications are recalculated.

**Example.** Milk runs out on Oct 17 with a 2-day advance notice: alerts on Oct 15 and Oct 16, and a notice on Oct 17. The batch expires on Feb 9 (alerts on Feb 7 and Feb 8, notice on Feb 9), but since the batch ran out on Oct 17, those notifications are not sent.

### BR-04: Configurable advance notice

**Rule.** Advance notice is always in **days**, for both restocking and expiration, because both events are dates. The user configures how many days before the event each alert is sent. By default, the **first alert is 2 days before** and the **second is 1 day before**, and the user can add a **third** if they want. Each alert is independent: changing the first does not change the second. If two alerts fall on the same day, only one is sent. If an alert's date has already passed when the run-out is calculated (for example, the product runs out in 3 days and the first alert is set to 5), that alert is not sent and only applies again from the next batch; the other alerts continue normally. Since the run-out date depends on consumption, changing consumption changes the date of the restocking alerts.

**Example.** Run-out on Oct 23 with the defaults: alerts on Oct 21 and Oct 22. If the user changes only the first to 5 days, the alerts go out on Oct 18 and Oct 22. If they add a third one at 3 days, another alert goes out on Oct 20. If consumption increases and the run-out moves to Oct 20, the alerts are recalculated from the new date. If the product runs out in 3 days and the first alert is set to 5 days, the 5-day alert is not sent (its date has passed) and the 1-day alert goes out as usual. If both alerts are set to 1 day, only one is sent.

### BR-05: Default product shelf life and user adjustments

**Rule.** Each product comes with a default shelf life, in days, calculated from several sources (the sources are recorded). Each batch has its own expiry date and brand. The user can edit a batch's shelf life by entering the date printed on the package:

- the app converts the date into days (expiry date − purchase date) and that number becomes the product's new default shelf life in that workspace, applying to the following batches;
- if the user chooses **this batch only**, the default does not change.

Earlier batches never change. Adjustments apply only to that workspace. If the user does not edit a batch, it uses the current default shelf life.

**Example.** The default for milk is 120 days. The user buys 3 batches. Batch 2 has a shorter shelf life and the user edits it to 100 days: batch 3 is created with 100. If batch 3 is normal, the user edits it back to 120. If, instead, the user had chosen "this batch only" on batch 2, batch 3 would stay at 120.

### BR-06: Buying a new batch while stock is still at home

**Rule.** Each purchase creates a new batch with its own expiry date and brand. Earlier batches do not change. The product's stock is the sum of its batches. Consumption comes first from the batch with the **earliest expiry date**, even if it is not the oldest. The run-out date and the restocking alerts are recalculated; expiration alerts stay per batch.

**Example.** See section 4: the Oct 15 purchase moves the run-out date from Oct 17 to Oct 23, but does not change the expiry date of the Oct 12 batch.

### BR-07: Changing and scheduling consumption

**Rule.** Every product comes with a preset consumption, which only changes when the user edits it. Consumption can be entered in two ways:

- **directly**: for example, 130 g per day;
- **as a duration**: "this quantity lasts N days", and the app calculates consumption = quantity ÷ N.

When editing, there are three effective-date options:

1. **No date:** applies from today until the next change.
2. **With a start date:** applies from that date until the next change.
3. **With a start and end date:** applies only during that period; afterwards, consumption goes back to the previous value.

The past is never altered: history and stock already calculated remain as they are. Only the days from the effective date onward use the new consumption. Schedules work with dates, not times. If a schedule overlaps another, the most recent one applies: if both start on the same day, the earlier one is removed entirely; if the earlier one starts before, it is kept only until the day before the new one starts, and the new one applies from then on.

**Example.** Consumption of 1 milk per day. Visitors from Oct 20 to Oct 22: the user schedules 3 per day for that period, and on Oct 23 consumption goes back to 1. Another case: 1.3 kg of shampoo that lasts 10 days → 1,300 g ÷ 10 = 130 g per day. Overlap: a schedule of 3 per day from Oct 20 to Oct 25 already exists and the user creates another of 1 per day starting on Oct 23; the first applies from Oct 20 to Oct 22 and the new one from Oct 23 onward. If the new one started on Oct 20, the first would be removed.

### BR-08: Measures, quantities, and packages

**Rule.** There are three measure families: **unit**, **weight** (kg and g), and **volume** (L and mL). The conversions 1 kg = 1000 g and 1 L = 1000 mL apply. The **quantity purchased** accepts decimals in weight and volume; in units, it is always a whole number. **Consumption** is a rate and can be decimal in any measure (BR-01). Each product has a default package (milk: a box of 12 units), which the user can edit at purchase. As with shelf life (BR-05), the edit becomes the default for the following batches, or applies only to that batch. The batch records the resulting total number of items.

**Display.** Stock is shown in whole items, together with the consumption and, when the product has a measure (g, mL), the item's total. An item only leaves the count when accumulated consumption completes 1 whole item; until then, it still counts as 1. There is no rounding and no decimal of an item. Internally, the calculation (BR-01) uses the decimal value.

**Example.** The brand comes in a box of 6: the user edits the package to 6 and buys 2 boxes, so the batch has 12 units. Buying 1.5 kg of rice is valid; buying 1.5 eggs is not. Consuming 0.5 egg per day (1 every 2 days) is valid, because it is a rate. A 1,300 g shampoo with a consumption of 130 g per day: it shows as "1 bottle" (1,300 g, 130 g per day) for 10 days and only goes to 0 when the 1,300 g are consumed. Milk with 6 units and a consumption of 0.6 per day: end of day 1, still 6 (consumed 0.6); end of day 2, it goes to 5 (consumed 1.2).

### BR-09: Zero stock

**Rule.** When a product's stock reaches zero (run-out date):

- the displayed stock becomes 0;
- the app sends only a **Notice** inside the app, with no alert on the device (the alerts were already sent earlier);
- the depleted batch stays in the history (calendar).

The product is added to the **next purchases list** already at the **first restocking alert**, leaving time to plan the shopping trip. If that alert's date has already passed when the run-out is calculated, the product is added to the list immediately.

**Example.** Milk runs out on Oct 23: the milk is added to the list on Oct 21, with the first alert; on Oct 23 the stock shows as 0, the notice arrives in the app, and the batches stay in the calendar as depleted.

### BR-10: Workspace, members, and permissions

**Rule.** A workspace gathers up to 7 members (initial limit, which may change). Every change (consumption, shelf life, package, time zone) applies to the whole workspace and every member sees it. The time zone is set once in the workspace and applies to everyone. The roles are:

- **Child:** can only view.
- **Teen:** can edit everything, but the change only takes effect after **any adult** validates it. While pending, the current value keeps applying until an adult approves or rejects the change. Checking items off the next purchases list (the checklist) does not need validation (BR-11).
- **Adult:** edits everything.

The workspace **creator** is a guardian and can designate one more adult as a guardian. The **pending validations** (changes and lists finished by teens) appear in the notifications tab of **all adults**, with no push: there is no problem if it takes a while to see them. The **activity record** (who changed what) is visible **only to guardians**, does not generate pushes, and appears only in the tab. The guardians' tab combines this record with the expiration and restocking notices, organized so that they see what is close to expiring without having to scroll.

**Example.** João (teen) changes the milk consumption from 1 to 2 per day. The change stays pending and shows up in the notifications tab; Ana (adult, creator, and guardian) or Carlos (adult, not a guardian) validates it; from then on, the new consumption applies to everyone.

### BR-11: Registering a purchase from the next purchases list

**Rule.** Checking an item off the next purchases list **does not change the stock**. The purchase is only registered when the user **finishes the list**. At that moment, each checked item becomes a batch (BR-06) with the default values (package and default shelf life), and the app opens a step where the user can edit what was bought (quantity, brand, package, expiry date). This step can be skipped: the batch can be edited later, directly in the stock. Checked items leave the list, and unchecked ones stay on it, for everyone, because they have not been bought yet. If a teen finishes the list, they can check items and edit brand, quantity, and expiry date as usual, but the stock entry only takes effect after an adult validates it (BR-10).

**Example.** Ana goes to the store, checks off milk and rice, and finishes the list. The app creates a milk batch (box of 12, default shelf life) and a rice batch, and asks whether she wants to adjust anything. The milk box came with 6, so she edits it; the rice stays as it is. Had João (teen) finished the list, the batches would only enter the stock after an adult validated them.

## 4. Complete Example

Scenario: milk in a box of 6, consumption of 1 per day, default shelf life of 120 days, advance notice of 2 days (restocking and expiration). Stock at the end of each day.

| Date | Event | Batch A | Batch B | Total |
|---|---|---|---|---|
| Oct 12 | Batch A purchased (6 milks, before 4 p.m.). Expiry: Feb 9. Expected run-out: Oct 17. | 5 | – | 5 |
| Oct 13 | Consumption | 4 | – | 4 |
| Oct 14 | Consumption | 3 | – | 3 |
| Oct 15 | Batch B purchased (6 milks). Expiry: Feb 12. Consumption comes from batch A. Run-out recalculated to Oct 23. | 2 | 6 | 8 |
| Oct 16 | Consumption | 1 | 6 | 7 |
| Oct 17 | Batch A depleted (goes to the history). The product still has stock, so there is no restocking notification. | 0 | 6 | 6 |
| Oct 21 | **Restocking alert** (2 days before Oct 23). The milk is added to the next purchases list. | 0 | 2 | 2 |
| Oct 22 | **Restocking alert** (1 day before) | 0 | 1 | 1 |
| Oct 23 | Batch B depleted. Only a **Notice** in the app (BR-09). | 0 | 0 | 0 |

Notes:

- Without the Oct 15 purchase, the restocking alerts would have been sent on Oct 15 and Oct 16. The purchase recalculated them to Oct 21 and Oct 22.
- The expiration notifications (Feb 7, 8, and 9 for batch A; Feb 10, 11, and 12 for batch B) no longer exist, because both batches ran out before expiring (BR-03).

## 5. Open Questions

None at the moment. New questions go here.

## 6. Future

- Recognize the product, the brand, and, if possible, the expiry date from a photo, using an AI model. Out of scope for the MVP.
- Work with times in consumption schedules.