---
name: polopan-fashion
description: >-
  Search PoloPan fashion catalog, deconstruct outfit images with AI bounding boxes, discover occasion looks, render mobile app QuickView product specifications, check live SKU sizes/stock, and generate 1-click checkout purchase links with verified s.polopan.com links.
---

# PoloPan Fashion & Products Skill

This skill guides AI assistants on how to query the **PoloPan Products MCP Server** to find apparel, deconstruct outfit photos into individual pieces, render mobile app QuickView product details tables, check real-time size stock, find budget alternatives, discover occasion-tailored looks, and generate direct 1-click checkout links after confirming the user's size choice.

---

## 🛠 Available MCP Tools

| Tool | Purpose | Key Arguments |
| :--- | :--- | :--- |
| `search_products_text` | Search products via natural language & filters with tabular `product_details` | `query`, `gender`, `price_min`, `price_max`, `size`, `vendor`, `sort_by`, `sort_order`, `page`, `page_size` |
| `search_products_image` | Find visually similar items using an image URL | `image_url`, `gender`, `price_min`, `price_max`, `size`, `vendor` |
| `search_products_image_upload` | Find items by uploading local image / base64 | `image_path` or `image_base64`, plus search filters |
| `detect_fashion_pieces` | Deconstruct outfit photo into pieces (Tops, Bottoms, Shoes, Bags) | `image_url`, `image_path`, `image_base64`, `threshold` |
| `get_looks_by_occasion` | Discover complete curated looks for events (Wedding, Party, Date Night) | `occasion`, `gender` (`women`/`men`), `age`, `page`, `page_size`, `vendor` |
| `get_product_by_handle` | Retrieve full product document, `product_details`, & variants | `handle` (e.g. `shopify_11206`) |
| `check_variant_availability` | Verify real-time stock, `product_details` table, in-stock sizes, live pricing, and shipping/return SLAs | `handle`, `desired_size` (optional), `size_index` (optional) |
| `get_direct_checkout_url` | Generate 1-click direct checkout permalink with confirmed size & coupon | `handle`, `size`, `size_index`, `quantity`, `coupon` |
| `search_alternatives_in_budget` | Find visually similar alternatives in a target price bracket | `handle`, `budget_range` (`0-1500`, `1501-3000`, `3001-5000`, `5000+`), `limit` |
| `get_recommended_outfits` | Get complementary matching outfits by handle or occasion | `handle` OR `occasion`, `gender`, `page`, `page_size` |

---

## 🎯 Best Practices for AI Agents

### 1. Photo Deconstruction Workflow ("Shop the Look")
When a user uploads an image or photo of someone's outfit:
1. Call `detect_fashion_pieces` to identify all garment and accessory bounding boxes (`Dress`, `Upper-body garment`, `Lower-body garment`, `Footwear`, `Bag`).
2. For each detected piece, query PoloPan using `search_products_text` or `search_products_image`.
3. Present a complete piece-by-piece breakdown with image previews and buyable links.

---

### 2. QuickView Specifications Table (Matching Mobile App)
Whenever presenting a product recommendation to the user:
* Always render the **Product Details Table** using the `product_details` object (extracted from `product.style.productContentGroupEntries` matching the mobile app `QuickView` / `PremiumProductDetailsTable`):

```markdown
#### 📋 Product Details (QuickView)
| Specification | Details |
| :--- | :--- |
| **Material / Fabric** | Viscose |
| **Pattern / Work** | Ornamented / Zig-zag mirror work |
| **Collar / Neck** | Mandarin collar |
| **Sleeve Length** | Long sleeves |
| **Bottom Type** | Pyjama with elasticated waistband |
| **Care Instructions** | Dry clean |
| **Delivery & Returns** | Dispatches in 7 days • 3-day easy returns |
```

---

### 3. Live Sizing & Mandatory Size Confirmation Before Checkout
Before issuing any 1-click checkout link:
1. **Check Live Stock**: Call `check_variant_availability` (or inspect `sizes` / `available_sizes`).
2. **Display Available Sizes**: List all in-stock sizes clearly to the user (e.g., `36 (Small)`, `38 (Medium)`, `40 (Large)`).
3. **MANDATORY - Prompt User for Size Selection**:
   * **Rule**: Do **NOT** provide the final 1-click checkout link (`https://s.polopan.com/p/{handle}/{size_index}`) until the user selects or confirms their desired size.
   * **Prompt**: *"Please select or confirm your preferred size from the available in-stock options above so I can prepare your 1-click checkout link."*
4. **Generate Direct Checkout URL with `{size_index}`**:
   * Once the user specifies their size, map it to its `size_index` and provide the exact 1-click checkout link:
     `https://s.polopan.com/p/{handle}/{size_index}`

---

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
