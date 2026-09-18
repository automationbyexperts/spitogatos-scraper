# Spitogatos.gr Scraper: Greek Property Listings & Agent Phones

Scrape real estate listings and Agents from Spitogatos.gr in both English and Greek. Collect prices, photos, location, and more. Easy setup, fast results, ready for Excel, JSON, or API integration

This repo shows how to call the [Spitogatos.gr Scraper: Greek Property Listings & Agent Phones](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/spitogatos-scraper on Apify](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/spitogatos-scraper](https://automationbyexperts.com/apify/spitogatos-scraper)
- **Actor ID for the API:** `fayoussef/spitogatos-scraper`

## Use cases

- [Find apartments for sale in Kolonaki, Athens](https://apify.com/fayoussef/spitogatos-scraper/examples/kolonaki-apartments-for-sale?fpr=youssef): Searches Spitogatos.gr for apartments for sale in Kolonaki up to 300,000 EUR and returns 25 plus fields per property: price, price per square metre, floor, year, energy class, GPS coordinates, owner or agent phone number and full resolution photos. No URL to copy, just the place name.
- [Find apartments for rent in Thessaloniki under 600 EUR](https://apify.com/fayoussef/spitogatos-scraper/examples/thessaloniki-apartments-for-rent-under-600?fpr=youssef): Pulls every apartment for rent in Thessaloniki at 600 EUR a month or less from Spitogatos.gr, with floor area, floor, heating, furnished flag, the landlord or agency phone number and the listing's coordinates. Students, relocating workers and agencies get the whole market in one sheet.
- [Export land plots for sale in Chania, Crete](https://apify.com/fayoussef/spitogatos-scraper/examples/crete-land-plots-for-sale?fpr=youssef): Lists plots of land for sale around Chania on Spitogatos.gr with price, area, price per square metre, coordinates and the seller's phone number. Developers and buyers hunting for buildable land in Crete use it to map what is on the market instead of paging through the site.
- [Διαμερίσματα για ενοικίαση στο κέντρο της Αθήνας έως 800€](https://apify.com/fayoussef/spitogatos-scraper/examples/athens-center-apartments-for-rent-greek?fpr=youssef): Συλλέγει από το Spitogatos.gr αγγελίες διαμερισμάτων προς ενοικίαση στο κέντρο της Αθήνας με ενοίκιο έως 800€ και επιστρέφει πάνω από 25 πεδία ανά ακίνητο: τιμή, τετραγωνικά, όροφο, έτος κατασκευής, ενεργειακή κλάση, συντεταγμένες GPS, τηλέφωνο μεσίτη ή ιδιοκτήτη και φωτογραφίες σε υψηλή ανάλυση.
- [Κατοικίες προς πώληση στη Θεσσαλονίκη από το Spitogatos](https://apify.com/fayoussef/spitogatos-scraper/examples/thessaloniki-homes-for-sale-greek?fpr=youssef): Συλλέγει τις αγγελίες κατοικιών προς πώληση στη Θεσσαλονίκη από το Spitogatos.gr (διαμερίσματα, μονοκατοικίες, μεζονέτες) με τιμή, τετραγωνικά, όροφο, έτος κατασκευής, ενεργειακή κλάση, συντεταγμένες GPS, τηλέφωνο μεσίτη και φωτογραφίες. Ιδανικό για ανάλυση τιμών ακινήτων και εντοπισμό ευκαιριών.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

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

### JavaScript / Node.js

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

### cURL (plain HTTP)

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

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Canada411 Scraper: Business Phones, Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [wallapop Scraper (Spain,Italy,Portugal)](https://github.com/automationbyexperts/wallapop-scraper)
- [AutoScout24 All-Country Scraper](https://github.com/automationbyexperts/autoscout24-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/spitogatos-scraper?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
