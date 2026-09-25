# polopan mcp server

find clothes faster, deconstruct outfit photos with AI bounding boxes, check real-time size stock, get full occasion looks, and checkout in 1 click.

## what you can do

### 1. search by words or image
* **text search**: type what you want, like *"birthday dress under 3000"*, with instant size and price filters.
* **visual search**: upload a photo or share an image link to find identical or visually similar items.

### 2. deconstruct full outfit photos ("shop the look")
* upload any photo or influencer screenshot to detect individual pieces with bounding boxes (**Dress**, **Top**, **Bottom**, **Footwear**, **Bag**) and find exact catalog matches for each piece.

### 3. real-time size stock & pricing check
* verify whether a shopper's specific size is in stock right now, get live prices with discount %, shipping SLAs, and return policies before making a recommendation.

### 4. discover full looks by occasion
* get curated, coordinated outfits (outfit + footwear + bag + jewelry) styled for specific occasions: **Wedding**, **Cocktail**, **Party**, **Date Night**, **Club Night**, **Brunch**, and **Casual**.

### 5. direct 1-click checkout links (shopify checkout kit style)
* generate instant 1-click purchase URLs with pre-selected sizes and coupon codes so shoppers skip browsing and buy immediately.

### 6. find budget alternatives
* if a user likes a product but wants options matching their budget, discover visually similar alternatives in distinct price tiers.

---

## setup

### install in cursor (deeplink)

[![install mcp server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://polopan.com/mcp/cursor)

### recommended for uninterrupted connection: hosted mcp (no local Node)

add this to your `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "polopan-products": {
      "type": "http",
      "url": "https://mcp-server.polopan.com/mcp",
      "headers": {}
    }
  }
}
```

save and reload Cursor.

### optional: local npm / npx (stdio)

if you prefer running the package on your machine:

```json
{
  "mcpServers": {
    "polopan-products": {
      "command": "npx",
      "args": ["-y", "polopan-products-mcp"]
    }
  }
}
```

requires node.js 18+. if `ERR_MODULE_NOT_FOUND` from `@modelcontextprotocol/sdk`, clear stale npx cache: `rm -rf ~/.npm/_npx/*` then run `npx` again.

---

## prompts you can copy and use

### shop the full look from a photo
```text
use polopan mcp to deconstruct this outfit photo into individual pieces (top, bottom, footwear, accessories).
then find the closest match on PoloPan for each piece in size M, check live stock, and give me direct checkout links for each item.
```

### wedding guest outfits by occasion
```text
i need outfit ideas for an evening wedding reception.
give me 5 complete looks for women with jewellery, shoes, and bag.
check available sizes and give me the direct 1-click checkout links with total price.
```

### birthday party shopping
```text
i am looking for a dress for a birthday party. i am a 27 year old girl.
use polopan mcp and give me complete outfits.
include completing outfits items in every look with links and total price.
show me budget, mid, and premium options.
```

### club night look
```text
budget is not a problem.
size is 2xl/3xl.
occasion is friends club night.
use polopan mcp and suggest 8 complete looks.
make them bold and stylish, and include total look price.
```

### look for cheaper options
```text
i want a printed shirt in the 1501-3000 budget range for a date night.
then give me best complete outfits based on the top option to complete the set.
```

---

## testing

Run the automated end-to-end test suite:
```bash
npm test
```