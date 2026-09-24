---
name: polopan-fashion
description: >-
  Search PoloPan fashion catalog, deconstruct outfit images with AI bounding boxes, discover occasion looks, check live SKU sizes/stock, and generate 1-click checkout purchase links with verified s.polopan.com links.
---

# PoloPan Fashion & Products Skill

This skill guides AI assistants on how to query the **PoloPan Products MCP Server** to find apparel, deconstruct outfit photos into individual pieces, check real-time size stock, find budget alternatives, discover occasion-tailored looks, and generate direct 1-click checkout links.

---

## 🛠 Available MCP Tools

| Tool | Purpose | Key Arguments |
| :--- | :--- | :--- |
| `search_products_text` | Search products via natural language & filters | `query`, `gender`, `price_min`, `price_max`, `size`, `vendor`, `sort_by`, `sort_order`, `page`, `page_size` |
| `search_products_image` | Find visually similar items using an image URL | `image_url`, `gender`, `price_min`, `price_max`, `size`, `vendor` |
| `search_products_image_upload` | Find items by uploading local image / base64 | `image_path` or `image_base64`, plus search filters |
| `detect_fashion_pieces` | Deconstruct outfit photo into pieces (Tops, Bottoms, Shoes, Bags) | `image_url`, `image_path`, `image_base64`, `threshold` |
| `get_looks_by_occasion` | Discover complete curated looks for events (Wedding, Party, Date Night) | `occasion`, `gender` (`women`/`men`), `age`, `page`, `page_size`, `vendor` |
| `get_product_by_handle` | Retrieve full product document & metadata | `handle` (e.g. `shopify_11206`) |
| `check_variant_availability` | Verify real-time stock, in-stock sizes, live pricing, and shipping days | `handle`, `desired_size` (optional) |
| `get_direct_checkout_url` | Generate 1-click direct checkout permalink with size & coupon | `handle`, `size`, `quantity`, `coupon` |
| `search_alternatives_in_budget` | Find visually similar alternatives in a target price bracket | `handle`, `budget_range` (`0-1500`, `1501-3000`, `3001-5000`, `5000+`), `limit` |
| `get_recommended_outfits` | Get complementary matching outfits by handle or occasion | `handle` OR `occasion`, `gender`, `page`, `page_size` |

---

## 🎯 Best Practices for AI Agents

### 1. Photo Deconstruction Workflow ("Shop the Look")
When a user uploads an image or photo of someone's outfit:
1. Call `detect_fashion_pieces` to identify all garment and accessory bounding boxes (`Dress`, `Upper-body garment`, `Lower-body garment`, `Footwear`, `Bag`).
2. For each detected piece, query PoloPan using `search_products_text` or `search_products_image`.
3. Present a complete piece-by-piece breakdown with image previews and buyable links.

### 2. Live Sizing & Stock Assurance
Before recommending any product to the user:
* Verify available sizes via `check_variant_availability` or check `available_sizes` in product payloads.
* Never recommend a size that is out of stock.

### 3. Selection -> Size Selection -> Direct 1-Click Checkout Links
* Every product includes an enriched `sizes` array with `size_index`, `size`, `available`, `inventory_quantity`, and direct `checkout_url` (`https://s.polopan.com/p/{handle}/{size_index}`).
* Use `check_variant_availability` with `desired_size` or `size_index` to verify live stock and get the exact `direct_checkout_url`.
* Use `get_direct_checkout_url` with the user's selected `size` or `size_index` (and any applicable `coupon`) to obtain the direct `https://s.polopan.com/p/{handle}/{size_index}` checkout URL so the shopper completes the purchase with 1 click.

### 4. Occasion Looks Discovery
When asked for wedding, party, club night, or vacation outfits:
* Call `get_looks_by_occasion` with the specific occasion (e.g. `occasion: "Wedding & Reception"`, `gender: "women"`).
* Each look includes full complementary components (garment + footwear + bag + jewelry).

---

## ⚙️ MCP Server Configuration

### Hosted HTTP (Cursor / Claude Desktop / Remote Agents)
```json
{
  "mcpServers": {
    "polopan-products": {
      "type": "http",
      "url": "https://mcp-server.polopan.com/mcp"
    }
  }
}
```

### Stdio / Local CLI (Node.js 18+)
```bash
npx -y polopan-products-mcp
```
