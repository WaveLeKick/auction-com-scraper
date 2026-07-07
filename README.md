[Auction Com Scraper](https://apify.com/fatihtahta/auction-com-scraper?fpr=data)

# Auction.com Scraper

**Slug:** fatihtahta/auction-com-scraper

## Overview

Auction.com Scraper collects structured property auction listing data, including listing identifiers, location details, pricing signals, auction timing, and key property attributes. It captures listing metadata, property summaries, and media links in a consistent JSON format suitable for analysis or enrichment. {{TARGET_SITE}} is a public marketplace for real estate auctions, making it valuable for tracking inventory, pricing movements, and market activity. Runs are automated and consistent, saving time compared to manual collection and ensuring repeatable datasets for workflows.

## Why Use This Actor

- **Market research / analytics:** Build datasets for auction inventory, pricing trends, and regional activity over time.
- **Product & content teams:** Populate listings, market summaries, and location pages with up-to-date auction data.
- **Developers / data engineering pipelines:** Feed BI tools, ETL jobs, or internal dashboards with structured records.
- **Lead gen / enrichment:** Identify properties, locations, and asset attributes to enrich CRM or prospecting data.
- **Monitoring / competitive tracking:** Track new auctions, status changes, and timing shifts across markets.

## Input Parameters

Provide any combination of URLs, queries, and filters. Leave optional fields empty to collect broader results.

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `startUrls` | `string[]` | One or more Auction.com search result pages, category pages, or listing URLs to collect. | – |
| `limit` | `integer` | Maximum number of listings to save per query. Set lower for quick sampling or higher for deeper coverage. | `50000` |

## Example Input

```
{
  "startUrls": [
    "https://www.auction.com/residential/26.361645418238187,-129.1526449272487,47.2563363379616,-102.5217855522487_bounds/active_lt/auction_date_order,resi_sort_v2_st/y_nbs",
    "https://www.auction.com/details/1-plymouth-cir-pueblo-co-1876508"
  ],
  "limit": 2000
}
```

## Output

### 6.1 Output destination

The actor writes results to an Apify dataset as JSON records. And the dataset is designed for direct consumption by analytics tools, ETL pipelines, and downstream APIs without post-processing.

### 6.2 Record envelope (all items)

Every record includes stable identifiers:

- **type** *(string, required)*
- **id** *(number, required)*
- **url** *(string, required)*

**Recommended idempotency key:** `type + ":" + id`

Use this key to deduplicate or upsert records when the same listing is discovered multiple times.

### 6.3 Examples

Example: listing (`type = "listing"`)

```
{
  "type": "listing",
  "id": 1876508,
  "url": "https://www.auction.com/details/1-plymouth-cir-pueblo-co-1876508",
  "Metadata": {
    "Listing ID": "1876508",
    "URN": "adc:listing:1876508",
    "Listing URL": "https://www.auction.com/details/1-plymouth-cir-pueblo-co-1876508",
    "Title": "1 Plymouth Cir, Pueblo, CO 81003, Pueblo County",
    "Source URL": "https://www.auction.com/residential/26.361645418238187,-129.1526449272487,47.2563363379616,-102.5217855522487_bounds/active_lt/auction_date_order,resi_sort_v2_st/y_nbs",
    "Seed Type": "url",
    "Seed Value": "https://www.auction.com/residential/26.361645418238187,-129.1526449272487,47.2563363379616,-102.5217855522487_bounds/active_lt/auction_date_order,resi_sort_v2_st/y_nbs",
    "Listing Status Group": "ACTIVE",
    "Listing Status": "SALE_PENDING",
    "Listing Status Label": "Jan 07"
  },
  "Pricing": {
    "Seller Current Value": 236000
  },
  "Vendor": {
    "Product Type": "TRUSTEE",
    "Is Reserve Displayed": false,
    "Buyer Premium Available": false,
    "Occupancy Status": "OCCUPIED",
    "Asset Type": "FORECLOSURE",
    "Is Direct Offer Enabled": false,
    "Attribution Source": "AUCTION_COM",
    "Venue Type": "LIVE",
    "Event Code": "E-30203A",
    "Trustee Sale": true
  },
  "Property": {
    "Property ID": "1132161",
    "Is Newly Listed": false,
    "Address": {
      "Street": "1 PLYMOUTH CIR",
      "City": "PUEBLO",
      "State": "CO",
      "County": "Pueblo",
      "Postal Code": "81003"
    },
    "Summary": {
      "Bedrooms": 3,
      "Bathrooms": 1,
      "Square Footage": 1040,
      "Lot Size": 0.21,
      "Year Built": 1979,
      "Valuation": 231672,
      "Structure Type Code": "SINGLE_FAMILY_HOME",
      "Structure Type Group": "SINGLE_FAMILY",
      "Coordinates": {
        "Longitude": -104.6408187,
        "Latitude": 38.2962301
      }
    }
  },
  "Auction": {
    "Start Date": "2026-01-07T08:00:00Z",
    "Visible Auction Start Date Time": "2026-01-07T16:00:00Z",
    "Is Online": false
  },
  "Media": {
    "Primary Photo": "https://adc-tenbox-prod.imgix.net/resi/propertyImages/1132161/ORD00679161_13437102.v1.jpeg?auto=compress,format"
  },
  "Marketing": {
    "Tags": [
      "JANU",
      "UTRY"
    ]
  }
}
```

Example: listing (`type = "listing"`)

```
{
  "type": "listing",
  "id": 1882894,
  "url": "https://www.auction.com/details/415-kenwood-dr-pueblo-co-1882894",
  "Metadata": {
    "Listing ID": "1882894",
    "URN": "adc:listing:1882894",
    "Listing URL": "https://www.auction.com/details/415-kenwood-dr-pueblo-co-1882894",
    "Title": "415 Kenwood Drive, Pueblo, CO 81005, Pueblo County",
    "Source URL": "https://www.auction.com/residential/26.361645418238187,-129.1526449272487,47.2563363379616,-102.5217855522487_bounds/active_lt/auction_date_order,resi_sort_v2_st/y_nbs",
    "Seed Type": "url",
    "Seed Value": "https://www.auction.com/residential/26.361645418238187,-129.1526449272487,47.2563363379616,-102.5217855522487_bounds/active_lt/auction_date_order,resi_sort_v2_st/y_nbs",
    "Listing Status Group": "ACTIVE",
    "Listing Status": "SALE_PENDING",
    "Listing Status Label": "Jan 07"
  },
  "Pricing": {
    "Seller Current Value": 184000
  },
  "Vendor": {
    "Product Type": "TRUSTEE",
    "Is Reserve Displayed": false,
    "Buyer Premium Available": false,
    "Occupancy Status": "OCCUPIED",
    "Asset Type": "FORECLOSURE",
    "Is Direct Offer Enabled": false,
    "Attribution Source": "AUCTION_COM",
    "Venue Type": "LIVE",
    "Event Code": "E-30203A",
    "Trustee Sale": true
  },
  "Property": {
    "Property ID": "669665",
    "Is Newly Listed": false,
    "Address": {
      "Street": "415 KENWOOD DRIVE",
      "City": "PUEBLO",
      "State": "CO",
      "County": "Pueblo",
      "Postal Code": "81005"
    },
    "Summary": {
      "Bedrooms": 3,
      "Bathrooms": 1,
      "Square Footage": 1005,
      "Lot Size": 0.12,
      "Year Built": 1949,
      "Structure Type Code": "SINGLE_FAMILY_HOME",
      "Structure Type Group": "SINGLE_FAMILY",
      "Coordinates": {
        "Longitude": -104.642,
        "Latitude": 38.25162
      }
    }
  },
  "Auction": {
    "Start Date": "2026-01-07T08:00:00Z",
    "Visible Auction Start Date Time": "2026-01-07T16:00:00Z",
    "Is Online": false
  },
  "Media": {
    "Primary Photo": "https://adc-tenbox-prod.imgix.net/resi/propertyImages/669665/ORD00471174_1.v1.jpeg?auto=compress,format"
  },
  "Marketing": {
    "Tags": [
      "JANU",
      "UTRY",
      "RURL"
    ]
  }
}
```

## Field reference

### Listing fields (`type = "listing"`)

- **Metadata.Listing ID** *(string, required)*: Listing identifier.
- **Metadata.URN** *(string, optional)*: Unique listing URN.
- **Metadata.Listing URL** *(string, required)*: Canonical listing URL.
- **Metadata.Title** *(string, required)*: Full listing title and location.
- **Metadata.Source URL** *(string, optional)*: Source page URL.
- **Metadata.Seed Type** *(string, optional)*: Seed type label.
- **Metadata.Seed Value** *(string, optional)*: Seed input value.
- **Metadata.Listing Status Group** *(string, optional)*: High-level status group.
- **Metadata.Listing Status** *(string, optional)*: Listing status.
- **Metadata.Listing Status Label** *(string, optional)*: Status label text.
- **Pricing.Seller Current Value** *(number, optional)*: Current seller value when available.
- **Vendor.Product Type** *(string, optional)*: Auction product type.
- **Vendor.Is Reserve Displayed** *(boolean, optional)*: Whether reserve is shown.
- **Vendor.Buyer Premium Available** *(boolean, optional)*: Whether buyer premium is available.
- **Vendor.Occupancy Status** *(string, optional)*: Occupancy status label.
- **Vendor.Asset Type** *(string, optional)*: Asset type label.
- **Vendor.Is Direct Offer Enabled** *(boolean, optional)*: Direct offer availability.
- **Vendor.Attribution Source** *(string, optional)*: Attribution source label.
- **Vendor.Venue Type** *(string, optional)*: Venue type label.
- **Vendor.Event Code** *(string, optional)*: Event identifier.
- **Vendor.Trustee Sale** *(boolean, optional)*: Trustee sale indicator.
- **Property.Property ID** *(string, required)*: Property identifier.
- **Property.Is Newly Listed** *(boolean, optional)*: New listing indicator.
- **Property.Address.Street** *(string, optional)*: Street address.
- **Property.Address.City** *(string, optional)*: City.
- **Property.Address.State** *(string, optional)*: State.
- **Property.Address.County** *(string, optional)*: County.
- **Property.Address.Postal Code** *(string, optional)*: Postal code.
- **Property.Summary.Bedrooms** *(number, optional)*: Bedroom count.
- **Property.Summary.Bathrooms** *(number, optional)*: Bathroom count.
- **Property.Summary.Square Footage** *(number, optional)*: Living area size.
- **Property.Summary.Lot Size** *(number, optional)*: Lot size.
- **Property.Summary.Year Built** *(number, optional)*: Year built.
- **Property.Summary.Valuation** *(number, optional)*: Valuation amount.
- **Property.Summary.Structure Type Code** *(string, optional)*: Structure type code.
- **Property.Summary.Structure Type Group** *(string, optional)*: Structure type group.
- **Property.Summary.Coordinates.Longitude** *(number, optional)*: Longitude coordinate.
- **Property.Summary.Coordinates.Latitude** *(number, optional)*: Latitude coordinate.
- **Auction.Start Date** *(string, optional)*: Auction start date/time.
- **Auction.Visible Auction Start Date Time** *(string, optional)*: Displayed auction start date/time.
- **Auction.Is Online** *(boolean, optional)*: Online auction indicator.
- **Media.Primary Photo** *(string, optional)*: Primary photo URL.
- **Marketing.Tags** *(array[string], optional)*: Marketing tags.

## Data guarantees & handling

- **Best-effort extraction:** fields may vary by region/session/availability/UI experiments.
- **Optional fields:** null-check in downstream code.
- **Deduplication:** recommend `type + ":" + id`.

## How to Run on Apify

1. Open the Actor in Apify Console.
2. Configure your search parameters (e.g., category/practice area, state/region, optional city).
3. Set the maximum number of outputs to collect.
4. Click **Start** and wait for the run to finish.
5. Download results in JSON, CSV, Excel, or other supported formats.

## Scheduling & Automation

### Scheduling

**Automated Data Collection**

Schedule runs to keep your dataset fresh and monitor changes over time.

- Navigate to **Schedules** in Apify Console
- Create a new schedule (daily, weekly, or custom cron)
- Configure input parameters
- Enable notifications for run completion
- (Optional) Add webhooks for automated processing

### Integration Options

- **Webhooks:** Trigger downstream actions when a run completes
- **Zapier:** Connect to 5,000+ apps without coding
- **Make (Integromat):** Build multi-step automation workflows
- **Google Sheets:** Export results to a spreadsheet
- **Slack/Discord:** Receive notifications and summaries
- **Email:** Send automated reports via email

## Performance

Estimated run times:

- **Small runs (< 1,000 outputs):** ~2–3 minutes
- **Medium runs (1,000–5,000 outputs):** ~5–15 minutes
- **Large runs (5,000+ outputs):** ~15–30 minutes

Execution time varies based on filters, result volume, and how much information is returned per record.

## Compliance & Ethics

### Responsible Data Collection

This actor collects publicly available **real estate auction listing** information from {{TARGET_SITE}} for legitimate business purposes, including:

- **Real estate** research and market analysis
- **Investment scouting and property research**
- **Portfolio monitoring and valuation review**

This section is informational and not legal advice.

### Best Practices

- Use collected data in accordance with applicable laws, regulations, and the target site’s terms
- Respect individual privacy and personal information
- Use data responsibly and avoid disruptive or excessive collection
- Do not use this actor for spamming, harassment, or other harmful purposes
- Follow relevant data protection requirements where applicable (e.g., GDPR, CCPA)

## Support

For help or questions, open an issue or use the actor page on Apify. Please include the input you used (redacted if needed), the run ID, a clear expected vs. actual description, and an optional small output sample to speed up troubleshooting.