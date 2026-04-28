# PoloPan MCP Server

Search products and generate complete fashion outfit recommendations through a production-ready MCP server.

## Supported Features

### Product Discovery

**Text Search** - Search products with optional filters like gender, size, price, vendor, and sorting.

**Image Search (URL)** - Find similar products by passing an image URL.

**Image Upload Search** - Upload a local image/base64 and run visual search.

---

### Product Intelligence

**Product by Handle** - Fetch full product details using a product handle.

**Alternatives in Budget** - Find similar products under selected budget ranges.

**Recommended Outfits** - Get complete outfit recommendations from a source product.

## Setup Instructions

### Add PoloPan MCP to Cursor

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](
cursor://anysphere.cursor-deeplink/mcp/install?name=polopan-products&config=%7B%22command%22%3A%22npx%22%2C%22args%22%3A%5B%22-y%22%2C%22%40our/polopan-products-mcp%22%5D%7D
)

### OR

**Manual Setup:** Update your `mcp.json` configuration file in `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "polopan-products": {
      "command": "npx",
      "args": ["-y", "@our/polopan-products-mcp"]
    }
  }
}
```

Save the file and reload Cursor.

## Example Prompts You Can Try

### Find by Text

```text
Find women party dresses under 3000 in size XXL.
```

### Find by Image

```text
Use this image and suggest similar tops in my size.
```

### Get Budget Alternatives

```text
For handle myntra-36901009, show alternatives in 1501-3000.
```

### Build Outfits

```text
Create 5 complete outfits from this dress for a birthday party.
```
