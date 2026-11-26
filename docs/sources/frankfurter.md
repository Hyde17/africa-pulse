
# Frankfurter — Foreign Exchange Rates API

## Summary

Frankfurter is a free foreign-exchange API that aggregates rates from central banks and other official sources. Its v2 API supports date-specific and historical queries, currency filters, and provider filters.

By default, the API returns blended mid-market rates. These are useful for broad daily currency coverage, but they are not necessarily identical to the official rate published by a particular African central bank. Where a specific provider is required, use the provider filter and verify that the provider publishes the requested currency and date.

## Owner

- **Service:** Frankfurter
- **Documentation:** https://frankfurter.dev/
- **Currency catalogue:** https://frankfurter.dev/currencies/
- **API base URL:** https://api.frankfurter.dev/

## Documentation

- **Main documentation:** https://frankfurter.dev/
- **Currency catalogue:** https://frankfurter.dev/currencies/
- **API endpoint family:** `/v2/rates`

## Domain

Daily foreign-exchange reference rates, historical rates, and currency/provider coverage.

## Access method

REST API over HTTPS.

Example request:

```bash
curl -sS \
  "https://api.frankfurter.dev/v2/rates?base=USD&quotes=NGN,KES,EGP,ZAR,CDF"
```

## Live API verification

Tested against the Frankfurter v2 rates endpoint on 2026-11-26.

**Request:**

```http
GET https://api.frankfurter.dev/v2/rates?base=USD&quotes=NGN,KES,EGP,CDF
```

**HTTP status:** `200`

**Result:** All four requested currency pairs returned rate observations.

Trimmed response:

```json
[
  {
    "date": "2026-11-26",
    "base": "USD",
    "quote": "NGN",
    "rate": 1385.65
  },
  {
    "date": "2026-11-26",
    "base": "USD",
    "quote": "KES",
    "rate": 130.02
  },
  {
    "date": "2026-11-26",
    "base": "USD",
    "quote": "EGP",
    "rate": 54.447
  },
  {
    "date": "2026-11-26",
    "base": "USD",
    "quote": "CDF",
    "rate": 2289.11
  }
]
```

The response confirms that Frankfurter returned all four requested currency pairs on the tested date.

The rates represent units of the quote currency per one unit of the base currency. For example, the NGN observation represents 1,385.65 Nigerian naira per US dollar.

This test establishes live rate availability for the four requested pairs on the verification date. It does not establish complete historical coverage, availability on every date, or provider-specific rate availability.

**Currencies verified:** NGN, KES, EGP, CDF.

**Not verified by this request:** ZAR.

## Rate interpretation

- **Base currency:** The currency from which the rate is quoted.
- **Quote currency:** The currency in which the rate is expressed.
- **Rate:** The number of quote-currency units equivalent to one unit of the base currency.
- **Date:** The observation date returned by the API.

For example, `USD/NGN = 1385.65` means one US dollar is equivalent to 1,385.65 Nigerian naira.

## Considerations and limitations

- Blended mid-market rates should not be treated as equivalent to official central-bank rates.
- Currency catalogue availability does not guarantee that a rate observation exists for every date.
- Historical availability should be validated independently for each required currency.
- Provider-specific rates require verification of the provider's coverage and applicable terms.
- The API's broad currency coverage does not establish city-level or parallel-market coverage.
- Licensing and redistribution terms should be reviewed before publishing data sourced from the API.

## Recommendation

Frankfurter is a viable initial candidate for broad daily multi-currency ingestion. The live test on 2026-11-26 confirmed rate observations for NGN, KES, EGP, and CDF.

Use it as a blended reference-rate source, while retaining CBN and CBK as separate candidates where their official or indicative rate definitions are required.

Further validation is needed for historical coverage, provider-specific rates, ZAR availability, and redistribution requirements.
