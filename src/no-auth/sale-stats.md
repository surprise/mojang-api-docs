# Fetch sale statistics
This endpoint reveals sale statistics of numerous Mojang games.

Keep in mind that the response totals are added together for all of the products listed in the `metricKeys` array.

### Request
- **Method:** `POST`
- **Endpoint:** `/orders/statistics`
- **Full URL:** `https://api.mojang.com/orders/statistics`
- **Headers:**
  - `Accept: application/json`
  - `Content-Type: application/json`

This endpoint fetches sale statistics for the provided Mojang games. For the `metricKeys` array, you can choose one or multiple of the following sale identifiers:

```python
item_sold_minecraft # amount of copies of Minecraft NOT purchased via prepaid card / giftcode
prepaid_card_redeemed_minecraft # amount of copies of Minecraft that are purchased via prepaid card / giftcode
item_sold_cobalt # amount of copies of Cobalt NOT purchased via prepaid card / giftcode
prepaid_card_redeemed_cobalt # amount of copies of Cobalt that are purchased via prepaid card / giftcode
item_sold_scrolls # amount of copies of Scrolls sold
item_sold_dungeons # amount of copies of Minecraft Dungeons sold
```

As the POST body, you must use an array that looks similar to this (of course, adding your own sale identifiers):

```json
{
  "metricKeys": [
    "item_sold_minecraft", 
    "prepaid_card_redeemed_minecraft"
  ]
}
```

### Response
**200: OK**

Successfully listed sale statistics. If you provided an invalid product name(s), the sale statistics will all be zero.

```json
{
   "total": 37547032, // total amount of sales
   "last24h": 10469, // sales in last 24 hours
   "saleVelocityPerSeconds": 0.15333334 // decimal avg. sales per second for all provided products
}
```

**400: Bad Request**

Your request was malformed. Perhaps you listed zero products in your array, or perhaps your array does not contain the `metricKeys` object.

```json
// listed zero products in array
{
   "error": "IllegalArgumentException",
   "errorMessage": "No key provided."
}

// array doesn't contain metricKeys
{
   "error": "IllegalArgumentException",
   "errorMessage": "keys can not be null."
}
```
