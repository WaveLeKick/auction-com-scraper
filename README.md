[Auction Com Scraper](https://apify.com/memo23/auction-com-scraper?fpr=data)

# Auction.com Scraper

**Unlock the Full Power of Auction.com Property Data** - Track, analyze, and monitor Auction.com listings with a scraper built for search result pages, URL-based filters, and structured real-estate output. Whether you are following bank-owned inventory, foreclosure activity, nearby search results, or pricing and occupancy trends, this actor turns Auction.com listing data into a usable dataset for research, lead generation, and market analysis.

*"From active online auctions to filtered foreclosure and bank-owned inventory, we turn Auction.com's listing data into your competitive advantage."*

## Overview

The Auction.com Scraper extracts structured property listing data from Auction.com URLs. It supports search result URLs, direct property detail URLs, and internally built search URLs based on Auction.com path filters. The actor maps Auction.com URL segments to the GraphQL payloads used by the site and returns flattened records ready for export to JSON or CSV.

## What does Auction.com Scraper do?

The Auction.com Scraper is a powerful tool that enables you to:

### Comprehensive Data Collection

- **Property Listings**

- Extract listing IDs, listing URLs, address data, photos, auction dates, and sale type
- Capture property characteristics such as beds, baths, square footage, lot size, and year built
- Gather auction signals like opening bid, starting bid, online vs live auction, and reserve visibility
- Track listing features such as buyer premium availability, occupancy status, financing availability, broker coop, and first look flags
- Collect property value fields such as estimated resale value when available
- **Search Context**

- Parse Auction.com URL filters into structured GraphQL filters
- Preserve listing state across online auction, foreclosure, bank-owned, and coming soon inventory
- Support real-estate filter dimensions such as property type, occupancy, beds, baths, sqft, price, sale format, and market-insight tags

### Advanced Scraping Capabilities

- **URL-to-GraphQL Mapping**: Converts Auction.com search URLs into the GraphQL filters used by the site
- **Pagination Handling**: Automatically follows additional result pages when the GraphQL search reports more pages
- **Efficient Processing**: Processes only new or unseen listings in monitoring mode
- **Flexible Filtering**: Supports hardcoded mapping for many Auction.com filter suffixes used in real search URLs
- **Structured Output**: Returns flattened, competitor-style listing records for easy downstream use

### Flexible Scraping Options

- **Search Results**: Scrape all property listings from an Auction.com search URL

- Example: `https://www.auction.com/residential/IL/Chicago_ct/active_lt/online,in_person,remote_bid,offer_af`
- **ZIP-Code Search**: Scrape listings inside a single ZIP (and nearby properties when `nearby_search` is on)

- Example: `https://www.auction.com/residential/07605_zp/`
- **State or County Search**: Scrape using a 2-letter state code or `*_co` county slug as the only geo scope

- State example: `https://www.auction.com/residential/NJ/`
- County example: `https://www.auction.com/residential/CA/Los-Angeles_co/`
- **Filtered Searches**: Apply Auction.com path filters directly in the start URL

- Example: `https://www.auction.com/residential/IL/Chicago_ct/active_lt/offer,direct_offer,remote_bid,in_person,online_af/auction_date_order,resi_sort_v2_st/y_fa/y_nbs/100_nsr`
- **Direct Property Details**: Scrape a single Auction.com property detail URL directly

- Example: `https://www.auction.com/details/638-e-91st-st-chicago-il-2037268`
- **Built Search URLs**: Build one search URL from state, city, listing type, and sale format inputs when `startUrls` is empty

### Supported URL Geo Scopes

The parser identifies path segments by suffix, so any combination of geo scope + filter segments works as long as at least one geo scope is present:

| Segment pattern | Meaning | Example |
| --- | --- | --- |
| `XX` (2 uppercase letters) | State | `NJ`, `IL` |
| `*_ct` | City | `Chicago_ct` |
| `*_co` | County | `Los-Angeles_co` |
| `*_zp` | ZIP code | `07605_zp` |
| `*_lt` | Listing type | `active_lt` |
| `*_af` | Sale formats | `online,in_person_af` |

For ZIP-based URLs the actor automatically resolves a `geo_location` (lat/lon) for the ZIP centroid via [zippopotam.us](https://api.zippopotam.us/) so `nearby_search` returns properties around the ZIP. You can override this by appending `?geo_location=lat,lon` to the start URL.

This tool is ideal for:

- Auction inventory research and monitoring
- Tracking bank-owned and foreclosure property trends
- Building structured property datasets for analysis or resale
- Monitoring new or changed inventory over time
- Supporting lead generation, acquisitions, and market intelligence workflows

## Features

- **Comprehensive Data Extraction**: Detailed property listing, auction, and search-filter data
- **GraphQL-Based Collection**:

- **Search Results**: Scrape all listings from Auction.com search results (e.g., `https://www.auction.com/residential/IL/Chicago_ct/active_lt/online,in_person,remote_bid,offer_af`)
- **ZIP / State / County Search**: Use a 2-letter state code, a `*_co` county slug, or a `*_zp` ZIP code as the geo scope (e.g., `https://www.auction.com/residential/07605_zp/`)
- **Direct Detail URLs**: Scrape an individual property from a detail page URL (e.g., `https://www.auction.com/details/638-e-91st-st-chicago-il-2037268`)
- **Flattened Output**: Return a normalized record per property instead of raw nested GraphQL payloads
- **Flexible Input**: Supports multiple input formats:

- Search result URLs copied directly from Auction.com
- Direct property detail URLs copied from Auction.com
- Built search URLs from Auction.com path inputs
- Advanced Auction.com filter URLs with many supported path suffixes
- **Automatic Pagination**: Handles multi-page GraphQL result sets automatically
- **Efficient Processing**: Concurrent scraping with configurable concurrency settings
- **Reliable Performance**: Built-in retry mechanisms and proxy support
- **Structured Data Export**: Download property listing data in JSON or CSV format for analysis

## How to Use

### Scraping Property Listings

To scrape Auction.com property listings:

1. **Set Up**: Ensure you have an Apify account and access to the Apify platform.
2. **Configure Input**: Provide one or more Auction.com search URLs, direct property detail URLs, or build one search URL using state/city inputs:

- `https://www.auction.com/residential/IL/Chicago_ct/active_lt/online,in_person,remote_bid,offer_af`
- `https://www.auction.com/residential/IL/Chicago_ct/active_lt/offer,direct_offer,remote_bid,in_person,online_af/auction_date_order,resi_sort_v2_st/y_fa/y_nbs/100_nsr`
- `https://www.auction.com/residential/07605_zp/` (ZIP-only search)
- `https://www.auction.com/residential/NJ/` (state-only search)
- `https://www.auction.com/residential/CA/Los-Angeles_co/` (county search)
- `https://www.auction.com/details/638-e-91st-st-chicago-il-2037268`
3. **Adjust Settings**: Configure options like max items, monitoring mode, and proxy settings as needed.
4. **Run the Scraper**: Execute the scraper on the Apify platform.
5. **Data Collection**: The scraper will output flattened Auction.com property records.

## Input Configuration

Here's an example of how to set up the input for the Auction.com Scraper:

```
{
    "startUrls": [
        "https://www.auction.com/residential/IL/Chicago_ct/active_lt/offer,direct_offer,remote_bid,in_person,online_af/auction_date_order,resi_sort_v2_st/y_fa/y_nbs/100_nsr",
        "https://www.auction.com/residential/07605_zp/",
        "https://www.auction.com/details/638-e-91st-st-chicago-il-2037268"
    ],
    "searchLimit": 500,
    "sort": "auction_date_order,resi_sort_v2",
    "nearbySearch": true,
    "nearbySearchRadius": 50,
    "requiresAggregation": true,
    "maxItems": 1000,
    "monitoringMode": false,
    "maxConcurrency": 5,
    "minConcurrency": 1,
    "maxRequestRetries": 5,
    "proxy": {
        "useApifyProxy": true
    }
}
```

### Input Fields Explanation

- `startUrls`: Array of Auction.com URLs. Supported values include search URLs (city, ZIP, county, or state-scoped — see Supported URL Geo Scopes) and direct property detail URLs. If provided, these URLs are used as-is.
- `propertyCategory`: Category used when building a search URL internally (for example, `residential`).
- `propertyState`: State code used when building a search URL (for example, `IL`).
- `propertyCity`: City used when building a search URL (for example, `Chicago`).
- `listingType`: Listing type used when building a search URL (for example, `active`).
- `assetEventTypes`: Sale format values used when building a search URL.
- `searchLimit`: Number of records requested per GraphQL search request.
- `sort`: Sort string sent to the GraphQL filters.
- `nearbySearch`: Controls the default GraphQL `nearby_search` value.
- `nearbySearchRadius`: Default nearby-search radius when the URL does not override it.
- `requiresAggregation`: Whether to request the aggregation block in the search response.
- `maxItems`: Maximum number of listings to emit.
- `monitoringMode`: When enabled, only emits listings not seen in previous runs.
- `maxConcurrency`: Maximum number of requests processed simultaneously.
- `minConcurrency`: Minimum number of requests processed simultaneously.
- `maxRequestRetries`: Number of retries for failed requests.
- `proxy`: Proxy settings for enhanced scraping reliability.

## Monitoring Mode

When `monitoringMode` is enabled, the scraper will only collect new listings that haven't been seen in previous runs. This is useful for:

- Tracking newly published or newly discovered property listings
- Building a historical archive of Auction.com inventory
- Monitoring cities or filter combinations without duplicating already-seen listings

### How Monitoring Mode Works

1. The scraper maintains a record of previously scraped Auction.com listing IDs
2. On subsequent runs with `monitoringMode: true`, it checks each listing against this record
3. Only unseen listings are processed and added to the output
4. The record is updated with any new listing IDs found

## Output Structure

The scraper provides flattened Auction.com property listing records. The output includes listing identity, property attributes, auction timing, sale metadata, and useful booleans for filtering and analysis.

### Sample JSON Output

```
{
  "id": "2037268",
  "url": "https://www.auction.com/details/638-e-91st-st-chicago-il-2037268",
  "primary_photo_url": "https://adc-tenbox-prod.imgix.net/resi/propertyImages/755499/755499_ext_1.v1.jpeg?auto=compress,format",
  "address": "638 E 91ST ST, CHICAGO, IL 60619, COOK COUNTY",
  "country_primary_subdivision": "IL",
  "country_secondary_subdivision": "COOK",
  "municipality": "CHICAGO",
  "postal_code": "60619",
  "street_description": "638 E 91ST ST",
  "beds": 2,
  "baths": 1,
  "sqft": 846,
  "lot_sqft": 0.07,
  "year_built": 1922,
  "property_type": "SINGLE_FAMILY_HOME",
  "property_type_group": "SINGLE_FAMILY",
  "opening_bid": 35000,
  "est_resale_value": null,
  "starting_bid_amount": 35000,
  "auction_start_date": "2026-04-14T12:00:00Z",
  "auction_end_date": "2026-04-16T14:10:30Z",
  "saleType": "Bank Owned",
  "auctionDate": "2026-04-14",
  "auctionTime": "12:00",
  "auctionLocation": "Online Auction",
  "status": "Apr 14 - Apr 16, 2026",
  "listing_photos_count": 5,
  "is_third_party_online": null,
  "is_reserve_displayed": null,
  "broker_commission": null,
  "financing_available": null,
  "buyer_premium_available": false,
  "interior_access_allowed": false,
  "occupancy_status": "OCCUPIED",
  "is_first_look_enabled": false,
  "is_direct_offer_enabled": false,
  "scrapedTimestamp": "2026-04-14T21:35:29.932Z"
}
```

## Output Fields Explanation

This section provides a detailed breakdown of all fields in the JSON output from the Auction.com Scraper. The output is a single flattened record per listing.

### Listing Details

- `id` (String): Auction.com listing ID. Example: `"2037268"`.
- `url` (String): Full Auction.com detail page URL for the listing.
- `primary_photo_url` (String): Main listing photo URL.
- `address` (String): Combined one-line address including street, city, state, postal code, and county when available.
- `country_primary_subdivision` (String): State or primary subdivision code. Example: `"IL"`.
- `country_secondary_subdivision` (String): County name without the word `COUNTY`. Example: `"COOK"`.
- `municipality` (String): City/municipality in uppercase. Example: `"CHICAGO"`.
- `postal_code` (String): ZIP/postal code for the property.
- `street_description` (String): Street line of the property address in uppercase.

### Property Attributes

- `beds` (Number|null): Number of bedrooms.
- `baths` (Number|null): Number of bathrooms. Can be an integer or decimal such as `1.5` or `2.5`.
- `sqft` (Number|null): Interior square footage.
- `lot_sqft` (Number|null): Lot size value as returned by Auction.com.
- `year_built` (Number|null): Year the property was built.
- `property_type` (String|null): Detailed structure type code such as `SINGLE_FAMILY_HOME`, `DUPLEX_BUILDING`, or `MULTI_UNIT_BUILDING`.
- `property_type_group` (String|null): Broader structure grouping such as `SINGLE_FAMILY` or `MULTI_FAMILY`.

### Pricing And Valuation

- `opening_bid` (Number|null): Opening bid value from the listing auction block.
- `est_resale_value` (Number|null): Estimated resale/composite valuation when available.
- `starting_bid_amount` (Number|null): Starting bid amount, including online segment fallback when present.

### Auction Timing

- `auction_start_date` (ISO 8601|null): Auction start timestamp in UTC.
- `auction_end_date` (ISO 8601|null): Auction end timestamp in UTC when available.
- `auctionDate` (String|null): Date portion derived from `auction_start_date` in `YYYY-MM-DD` format.
- `auctionTime` (String|null): Time portion derived from `auction_start_date` in `HH:MM` format.
- `auctionLocation` (String|null): Human-readable auction location, usually `Online Auction` or `Live Auction`.
- `status` (String|null): Auction.com status label shown in search results, for example `Apr 14 - Apr 16, 2026`, `Apr 28`, or `Coming Soon`.

### Sale Classification

- `saleType` (String|null): Human-readable sale classification derived from Auction.com listing fields, for example `Bank Owned`, `Foreclosure`, or `Private Seller`.

### Listing Configuration Flags

- `listing_photos_count` (Number|null): Number of photos available for the listing.
- `is_third_party_online` (Boolean|null): Whether the listing is handled as a third-party online sale.
- `is_reserve_displayed` (Boolean|null): Whether reserve information is displayed.
- `broker_commission` (Number|null): Broker commission amount or value when returned.
- `financing_available` (Boolean|null): Whether financing is available for the property.
- `buyer_premium_available` (Boolean|null): Whether a buyer premium applies.
- `interior_access_allowed` (Boolean|null): Whether interior access is allowed.
- `occupancy_status` (String|null): Occupancy state such as `OCCUPIED` or `VACANT`.
- `is_first_look_enabled` (Boolean|null): Whether first-look access is enabled.
- `is_direct_offer_enabled` (Boolean|null): Whether direct offers are enabled.

### Scrape Metadata

- `scrapedTimestamp` (ISO 8601): Timestamp for when the actor produced the output row.

---

## Explore More Scrapers

If you found this Auction.com Scraper useful, be sure to check out our other scrapers and actors at [memo23's Apify profile](https://apify.com/memo23). We offer a wide range of tools to support web scraping, data collection, and automation across multiple sites and use cases.

## Support

- For issues or feature requests, please use the [Issues](https://console.apify.com/actors/7Fw4OYjfMapM6l49D/issues) section of this actor.
- If you need customization or have questions, feel free to contact the author:

- Author's website: [https://muhamed-didovic.github.io/](https://muhamed-didovic.github.io/)
- Email: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)

## Additional Services

- Request customization or whole dataset: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- If you need anything else scraped, or this actor customized, email: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- For API services of this scraper (no Apify fee, just usage fee for the API), contact: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)
- Email: [muhamed.didovic@gmail.com](mailto:muhamed.didovic@gmail.com)