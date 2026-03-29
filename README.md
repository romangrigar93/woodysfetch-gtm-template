# Woody's Fetch — Conversion Tracking (GTM Template)

Google Tag Manager template for tracking purchase and add-to-cart conversions from [Woody's Fetch](https://woodysfetch.com) product recommendation widgets.

## What it does

- **Purchase tracking** — sends order data (order ID, value, product IDs, quantities) to Woody's Fetch when a GA4 `purchase` event fires
- **Add-to-cart tracking** — sends product data when a GA4 `add_to_cart` event fires
- **Widget click capture** — listens for clicks on Woody's Fetch widget buttons and pushes a GA4 `add_to_cart` event into the dataLayer
- **Consent Mode v2 compatible** — conversion data is sent to your own Woody's Fetch endpoint, not to Google

## Installation

### From GTM Community Gallery (recommended)

1. In GTM go to **Templates** > **Search Gallery** > search for **Woody's Fetch**
2. Click **Add to workspace**
3. Create a new tag using the template

### Manual import

1. Download `template.tpl` from this repository
2. In GTM go to **Templates** > **Tag Templates** > **New**
3. Click the three-dot menu > **Import**
4. Select the downloaded `template.tpl` and save

## Configuration

| Field | Required | Description |
|-------|----------|-------------|
| **Shop API Key** | Yes | Your Woody's Fetch API key (Settings > Integration in the admin panel) |
| **Track purchase conversions** | — | Enable purchase event tracking (default: on) |
| **Track add-to-cart events** | — | Enable add-to-cart event tracking (default: on) |
| **Capture widget button clicks** | — | Auto-push GA4 add_to_cart events from widget clicks (default: on) |
| **Debug mode** | — | Log payloads to the browser console |

### Custom variable overrides

By default the tag reads from the standard GA4 ecommerce dataLayer (`ecommerce.transaction_id`, `ecommerce.items[]`, etc.). If your shop uses a non-standard dataLayer structure, expand **Custom Variable Overrides** in the tag settings to map your own GTM variables.

## Trigger setup

Create these triggers for the tag:

| Trigger type | Event name | Purpose |
|-------------|------------|---------|
| Custom Event | `purchase` | Fires on completed orders |
| Custom Event | `add_to_cart` | Fires on add-to-cart actions |

If you only need one of the two events, create just that trigger and disable the other in the tag settings.

## How it works

1. The tag reads session and click data from the `_wf_tracking` cookie
2. On a matching event it builds a conversion payload from the GA4 ecommerce dataLayer (or your custom overrides)
3. A lightweight helper script (`woodysfetch.com/js/gtm-helper.js`) handles the actual POST request and enriches the payload with sessionStorage data that the GTM sandbox cannot access directly

## License

Apache 2.0 — see [LICENSE](LICENSE).
