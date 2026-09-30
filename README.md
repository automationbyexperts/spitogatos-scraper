# Spitogatos.gr Scraper: Greece Real Estate Listings, Prices, GPS & Agent Phone Numbers

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef)
![Agent phone](https://img.shields.io/badge/Agent%20phone-every%20listing-2ea44f)
![Spitogatos API key](https://img.shields.io/badge/Spitogatos%20API%20key-not%20needed-1C7ED6)
![Language](https://img.shields.io/badge/Language-English%20%7C%20Greek-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the Spitogatos.gr Scraper on Apify](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef)
> Scrape Greek property listings from Spitogatos.gr (apartments, houses, studios, land and commercial property, for sale or for rent) with price, price per m², GPS coordinates, photos and a **phone number for the agent or agency on every listing**. Search by place name, no URL and no Spitogatos API key needed.

**Spitogatos.gr Scraper** is a cloud scraper for **Spitogatos**, the largest real estate portal in Greece. It turns any Spitogatos search into a clean dataset, one row per property, ready for Excel, Google Sheets, a database or your own code. This repository documents the Spitogatos.gr Scraper Apify Actor: what it does, the input it takes, the data it returns, and working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/spitogatos-scraper on Apify](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/spitogatos-scraper](https://automationbyexperts.com/apify/spitogatos-scraper)
- **Actor ID for the API:** `fayoussef/spitogatos-scraper`

## What the Spitogatos scraper does

- **Sale and rental listings** across **Athens, Thessaloniki, Piraeus, Glyfada, Kifisia, Marousi, Kolonaki, Chania, Heraklion, Patras** and the rest of Greece.
- **Every property type**: apartments, studios, maisonettes, detached houses, villas, lofts, buildings, land plots, commercial space, new developments and student housing.
- **Search by place name, no URL needed.** Type `Kolonaki` or `Κολωνάκι`, pick sale or rent, add a price range, size, rooms, floor, year built, energy class, heating or features, and the Actor runs the search for you. Or paste any Spitogatos.gr search URL instead.
- **A phone number on every listing.** Spitogatos only names a specific agent on some listings. When it does not, the Actor looks up the agency and fills in the agency's own number, so `contact_telephone` is filled in on every record. In a live Thessaloniki test, 30 of 30 listings came back with a phone number, against 15 of 30 from the listing data alone.
- **Real estate agents too.** Scrape the Spitogatos agent directory (`/en/find-agents`, `/mesites`) for agency names, phones, addresses and websites by area.
- **English and Greek** Spitogatos pages both work.
- **Automatic pagination**, from one search page to thousands of listings.

It is a practical **Spitogatos API alternative**: Spitogatos has no public API, and this Actor handles the site's bot protection and proxies for you.

## Output fields: what data you get

Each property is one row with 60+ fields. The main ones:

| Field | Description |
|---|---|
| `url` / `id` | Spitogatos listing URL and ID |
| `category` | Property type (apartment, house, land, commercial...) |
| `price` / `pricePerSqMeters` | Asking price in EUR and price per m² |
| `sq_meters` / `rooms` / `no_of_bathrooms` | Floor area, rooms, bathrooms |
| `floorNumber` / `Floor Level` | Floor |
| `year_of_construction` / `renovationYear` | Year built and year renovated |
| `geographiesByLevel_*_fullName` | Region, municipality and neighbourhood |
| `latitude` / `longitude` | GPS coordinates |
| `contact_name` / `contact_telephone` / `contact_type` | The person or agency to call, and which one it is |
| `agentEmployee_firstName` / `agentEmployee_lastName` / `agentEmployee_telephone` | The named agent, when the agency assigned one |
| `agency_name` / `agency_telephone` / `agency_telephones` / `agency_contact_person` | Agency details and every published number |
| `agency_address` / `agency_website` / `agency_url` / `agent_id` | Agency address, website and Spitogatos profile |
| `images` | Full resolution photo URLs (1600x1200) |
| `description` | Full listing text |
| Amenities | Parking, storage, elevator, A/C, heating type, garden and more |

## Input

There are two ways to tell the scraper what to collect: search by filters, or paste Spitogatos.gr URLs into `start_urls` (search, listing or agent pages, English or Greek). Start URLs win when both are given, and `max_depth` sets how many result pages to scrape.

| Field | What it does |
|---|---|
| `locations` | Place names in English or Greek, e.g. `["Kolonaki", "Glyfada"]`. Partial names work |
| `listing_type` | `sale` or `rent` |
| `category` | `residential`, `commercial`, `land`, `other`, `new_development`, `student_housing` |
| `property_types` | `apartment`, `studio`, `maisonette`, `detached`, `villa`, `loft`, `building` and more |
| `price_min` / `price_max` | Price range in EUR |
| `area_min` / `area_max` | Floor area in m² |
| `rooms_min` / `rooms_max` | Number of rooms |
| `construction_year_min` / `construction_year_max` | Year built |
| `floor_min` / `floor_max` | Floor, from basement up |
| `energy_class` | `a` to `g` |
| `heating_controllers` / `heating_media` | Heating type |
| `amenities` | Features such as parking, storage, elevator, garden |
| `posted_within` / `updated_within` | Only listings posted or updated in the last 24 hours, 3 days, week, month... |
| `sort_by` / `sort_order` | Sort by relevance or price |

## Use cases

- **Greek property market research**: compare sale and rent prices and €/m² by neighbourhood across Athens, Thessaloniki and the islands.
- **Rental yield and investment analysis**: pull sale and rent listings for the same area and estimate gross yields.
- **Real estate lead generation**: build a list of active agencies and agents, with phone numbers, in a target area.
- **New listing alerts**: schedule a daily run with `posted_within: "24hours"` and catch new listings first.
- **Maps and geo analysis**: plot every listing with its GPS coordinates.
- **Relocation, students and expats**: export every rental under your budget in one sheet instead of paging through the site.

Ready-made examples you can run in one click:

- [Find apartments for sale in Kolonaki, Athens](https://apify.com/fayoussef/spitogatos-scraper/examples/kolonaki-apartments-for-sale?fpr=youssef): Searches Spitogatos.gr for apartments for sale in Kolonaki up to 300,000 EUR and returns 25 plus fields per property: price, price per square metre, floor, year, energy class, GPS coordinates, owner or agent phone number and full resolution photos. No URL to copy, just the place name.
- [Find apartments for rent in Thessaloniki under 600 EUR](https://apify.com/fayoussef/spitogatos-scraper/examples/thessaloniki-apartments-for-rent-under-600?fpr=youssef): Pulls every apartment for rent in Thessaloniki at 600 EUR a month or less from Spitogatos.gr, with floor area, floor, heating, furnished flag, the landlord or agency phone number and the listing's coordinates. Students, relocating workers and agencies get the whole market in one sheet.
- [Διαμερίσματα για ενοικίαση στο κέντρο της Αθήνας έως 800€](https://apify.com/fayoussef/spitogatos-scraper/examples/athens-center-apartments-for-rent-greek?fpr=youssef): Συλλέγει από το Spitogatos.gr αγγελίες διαμερισμάτων προς ενοικίαση στο κέντρο της Αθήνας με ενοίκιο έως 800€ και επιστρέφει πάνω από 25 πεδία ανά ακίνητο: τιμή, τετραγωνικά, όροφο, έτος κατασκευής, ενεργειακή κλάση, συντεταγμένες GPS, τηλέφωνο μεσίτη ή ιδιοκτήτη και φωτογραφίες σε υψηλή ανάλυση.
- [Κατοικίες προς πώληση στη Θεσσαλονίκη από το Spitogatos](https://apify.com/fayoussef/spitogatos-scraper/examples/thessaloniki-homes-for-sale-greek?fpr=youssef): Συλλέγει τις αγγελίες κατοικιών προς πώληση στη Θεσσαλονίκη από το Spitogatos.gr (διαμερίσματα, μονοκατοικίες, μεζονέτες) με τιμή, τετραγωνικά, όροφο, έτος κατασκευής, ενεργειακή κλάση, συντεταγμένες GPS, τηλέφωνο μεσίτη και φωτογραφίες. Ιδανικό για ανάλυση τιμών ακινήτων και εντοπισμό ευκαιριών.

## Quick start

### 1. In the browser (no code)

1. Open the Actor on Apify and click **Try for free**.
2. Type a place name in **Locations** (for example `Glyfada`), pick **Sale or rent**, a property type and a price range. Or paste a Spitogatos.gr search URL into **Start URLs**.
3. Click **Start**, then download the results as Excel, CSV or JSON from the **Output** tab.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/spitogatos-scraper").call(run_input={'locations': ['Kolonaki'],
 'listing_type': 'sale',
 'category': 'residential',
 'property_types': 'apartment',
 'price_max': 300000,
 'max_depth': 10})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

#### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/spitogatos-scraper").call({
    "locations": [
        "Kolonaki"
    ],
    "listing_type": "sale",
    "category": "residential",
    "property_types": "apartment",
    "price_max": 300000,
    "max_depth": 10
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

#### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~spitogatos-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~spitogatos-scraper/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "url": "https://www.spitogatos.gr/en/property/1218349400",
  "id": 1218349400,
  "category": "house",
  "price": 48000,
  "sq_meters": 40,
  "pricePerSqMeters": 1200,
  "rooms": 1,
  "no_of_bathrooms": 1,
  "floorNumber": 8,
  "Floor Level": 3,
  "year_of_construction": 1972,
  "renovationYear": 1982,
  "geographiesByLevel_2_fullName": "Thessaloniki - Municipality (Thessaloniki)",
  "geographiesByLevel_4_fullName": "Xirokrini - Panagia Faneromeni (Thessaloniki - Municipality)",
  "latitude": 40.646702,
  "longitude": 22.937429,
  "agent_id": 7302,
  "agentEmployee_firstName": "ΔΗΜΗΤΡΗΣ",
  "agentEmployee_lastName": "ΝΙΚΟΛΑΪΔΗΣ",
  "agentEmployee_telephone": "6975576965",
  "agency_name": "ART.HOME",
  "agency_telephone": "+302310900169",
  "agency_telephones": "+302310900169, +306973357937",
  "agency_contact_person": "Tsoulkanakis Thanos",
  "agency_url": "https://www.spitogatos.gr/en/find-agents/ART-HOME/7302",
  "contact_name": "ΔΗΜΗΤΡΗΣ ΝΙΚΟΛΑΪΔΗΣ",
  "contact_telephone": "6975576965",
  "contact_type": "agent employee",
  "images": [
    "https://m2.spitogatos.gr/329398219_1600x1200.jpg?v=20130730",
    "https://m1.spitogatos.gr/329398194_1600x1200.jpg?v=20130730"
  ],
  "description": "..."
}
```

## Integrations and automation

- **Schedule it** daily or weekly in the Apify Console to track new listings and price changes.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### Does Spitogatos have a public API?
No. Spitogatos.gr has no public API for listings. This Actor is a Spitogatos API alternative: you call one Apify endpoint and get structured JSON back, with no Spitogatos key or login.

### How do I scrape apartments for rent in Athens from Spitogatos?
Set `locations` to the area (for example `["Athens Center"]`, `["Kolonaki"]` or `["Pagkrati"]`), `listing_type` to `rent` and `property_types` to `apartment`, add `price_max`, and start the run. You can also paste a Spitogatos rental search URL into `start_urls`.

### Can I get the agent's or owner's phone number?
Yes, on every listing. `contact_telephone` holds the named agent's number when Spitogatos shows one, and the agency's own number otherwise. `contact_type` tells you which one you got, and `agency_telephones` lists every number the agency publishes.

### Can I search several areas at once?
Yes. Put as many place names in `locations` as you like. They are searched together and duplicates are removed.

### Can I filter by price, size, rooms and energy class?
Yes. Every filter from the Spitogatos search form is available: price, m², rooms, floor, year built, energy class, heating, features, and how recently the listing was posted or updated.

### Does it work with Greek place names and Greek pages?
Yes. `Κολωνάκι` and `Kolonaki` return the same area, and both English (`/en/`) and Greek Spitogatos URLs work.

### Can I scrape real estate agents and agencies?
Yes. Paste a Spitogatos agent directory URL (`/en/find-agents` or `/mesites`) or a single agent page into `start_urls` to get agency names, phones, addresses and websites.

### How many listings can I get per run?
As many as the search returns. The Actor pages through all results automatically, and `max_depth` limits the number of pages if you want fewer. Free-plan runs are capped at a small sample.

### How do I export Spitogatos data to Excel or CSV?
Open the run's **Output** tab in the Apify Console and download Excel, CSV, JSON, XML or HTML, or fetch the dataset through the API.

### Do I need my own proxy?
No. Proxies and Spitogatos's bot protection are handled inside the Actor.

### Is it legal to scrape Spitogatos.gr?
The Actor collects publicly available listing data. You are responsible for using it in line with Spitogatos.gr's terms and applicable law, including GDPR when you process contact details.

## Scraper Spitogatos στα ελληνικά

Το **Spitogatos.gr Scraper** συλλέγει αγγελίες ακινήτων από το Spitogatos.gr (διαμερίσματα, μονοκατοικίες, οικόπεδα και επαγγελματικούς χώρους, προς πώληση ή ενοικίαση) με τιμή, τιμή ανά τ.μ., τετραγωνικά, όροφο, έτος κατασκευής, ενεργειακή κλάση, συντεταγμένες GPS, φωτογραφίες και **τηλέφωνο μεσίτη ή μεσιτικού γραφείου σε κάθε αγγελία**. Γράψτε απλώς την περιοχή (π.χ. `Κολωνάκι`, `Γλυφάδα`, `Θεσσαλονίκη`), επιλέξτε πώληση ή ενοικίαση και κατεβάστε τα αποτελέσματα σε Excel, CSV ή JSON. [Δοκιμάστε το στο Apify](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef).

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related scrapers by AutomationByExperts

- [Spitogatos Cyprus Scraper (spitogatos.com.cy)](https://apify.com/fayoussef/spitogatos-cy-scraper?fpr=youssef)
- [XE.gr Greek Property Scraper](https://apify.com/fayoussef/xe-gr-scraper?fpr=youssef)
- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Canada411 Scraper: Phone Numbers & Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Wallapop Scraper: Spain, France, Italy, Portugal & UK](https://github.com/automationbyexperts/wallapop-scraper)
- [AutoScout24 Scraper: European Car Listings & Dealer Phones](https://github.com/automationbyexperts/autoscout24-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
