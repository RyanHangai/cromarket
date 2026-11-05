<h1 align="center">CroMarket</h1>

<p align="center">
  🇺🇸 English | <a href="README.pt-BR.md">🇧🇷 Português</a>
</p>

A shopping assistant, built with Python and SQL, that tracks what your household buys, predicts when each product will run out or expire, and reminds you in time to plan your shopping trip.

## The problem

Many people still write their shopping list by hand and only notice something has run out, or expired, when it is already too late. CroMarket replaces the paper list with one that maintains itself.

## How it works

1. **Log a purchase.** Record the product, quantity, brand, and, if you want, the expiry date printed on the package.
2. **CroMarket creates a batch.** Each purchase becomes a batch with its own expiry date, calculated from a default shelf life for that product (adjustable).
3. **Stock decreases every day** according to your household's consumption, always using the batch that expires first.
4. **You get notified in time.** Alerts arrive 2 days and 1 day before a product runs out or a batch expires. The product is added to your next purchases list automatically.

**Example:** you buy a box of 6 milks and your household drinks 1 per day. CroMarket calculates that it runs out 6 days later, sends alerts 2 days and 1 day before, and adds the milk to your list. If you buy another box before that, it recalculates the date for you.

## Features

- **Batch tracking:** every purchase has its own brand, stock, and expiry date.
- **Two kinds of notifications:** restocking and expiration. Alerts (push) are for what is urgent; notices stay inside the app.
- **Consumption schedules:** change your consumption for visitors, vacations, or parties, for a period or from a given date on.
- **Shared workspace:** a family shares the same stock and list, with roles for adults, teens, and children.
- **Default shelf lives** based on research across several sources, which you can adjust to what you actually bought.
- **Units, weight, and volume:** products can be tracked in units, kg/g, or L/mL.
- **History:** depleted and expired batches stay on record in a calendar view.

## Platforms

The plan is to build a **mobile app** first, followed by a **website** for desktop use. Both use the same Python backend, which runs in a **Docker** container in the cloud. This keeps your data in sync between your phone and your computer and leaves the heavy processing on the server, so both devices stay light.

The idea is to allow partial use without internet, for example to check your shopping list.

## Tech stack

| Layer | Choice |
| --- | --- |
| Language | Python |
| Database | SQL (engine to be decided) |
| Infrastructure | Docker, in the cloud (provider to be decided) |
| API | To be decided |
| Mobile app | To be decided |
| Website | To be decided |

## Documentation

- [Business rules](docs/business-rules/business-rules.md) ([pt-BR](docs/business-rules/regras-de-negocio.md)): how stock, consumption, batches, and notifications work.
- [Roadmap](ROADMAP.md): the step-by-step development plan.

## Contributors

- **Renan** ([@Renanzinhu](https://github.com/Renanzinhu))
- **Ryan** ([@RyanHangai](https://github.com/RyanHangai))

## License

See the [LICENSE](LICENSE) file.