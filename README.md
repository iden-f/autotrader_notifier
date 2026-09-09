# AutoTrader Bot — superseded

**This repository does not work and is no longer maintained.**
The working project lives at
[`iden-f/autotrader_minimal_secrets`](https://github.com/iden-f/autotrader_minimal_secrets).

## Why this one was retired

An audit of both repositories found this one had never successfully run:

- **It pointed at the wrong website.** The code scraped `autotrader.com`
  (United States) using a `div[data-listing-id]` selector, while the README
  described `autotrader.ca` (Canada). The two sites share neither markup nor
  listing ids, so the scraper matched nothing.
- **It never found a single listing.** `seen_listings.json` is `[]` and
  `archives/` is empty, across the whole life of the repository. The last
  commit was 2025-06-24.
- **Twilio was mandatory.** `load_config()` raised unless all seven
  environment variables were set, so no SMS account meant no bot at all.
- **The workflow could not save its results.** It used `actions/checkout@v2`
  without `permissions: contents: write`, so the `git push` step would have
  been rejected with a 403 even if the scraper had worked.
- **Its one test tested nothing.** It stubbed out `requests` *and*
  `BeautifulSoup`, replacing the parser with a small regex written inside the
  test file, so it verified the stub rather than the code.

The sibling repository, by contrast, targeted `autotrader.ca` correctly and
archived 50 real listings between June and December 2025. It was the better
starting point, and it is where the work went.

## What the replacement does

Same idea, rebuilt: you paste an autotrader.ca search link and it tells you
about new listings and **price drops** over Telegram, Discord, ntfy, Slack or
email — all free. It has a dashboard, a settings UI, health alerts when
scraping breaks, and a test suite that runs against real captured pages.

See its [README](https://github.com/iden-f/autotrader_minimal_secrets#readme).

## If you are running this one

Move to the other repository. Nothing here needs migrating — this bot never
recorded any listings.

## Licence

MIT.
