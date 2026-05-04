# polopan mcp server

find clothes faster, get full outfit ideas, and shop with less effort.

## what you can do

### search by words

type what you want, like "birthday dress under 3000", and get options quickly.

### search by image

upload a photo or share an image link to find similar styles.

### get complete outfit ideas

pick one item and get matching suggestions like footwear, bag, and earrings.

### find cheaper alternatives

if you like a product but want more options in your budget, ask for alternatives.

---

## setup

### install in Cursor (one-click / deeplink)

Cursor’s documented format is a **`cursor://`** deeplink ([install links](https://cursor.com/docs/mcp/install-links)), **not** `https://cursor.com/install-mcp` (that path returns **404**).

hosted HTTP (recommended — same MCP as Cloud Run, no local Node):

[![install PoloPan MCP (hosted)](https://cursor.com/deeplink/mcp-install-dark.svg)](cursor://anysphere.cursor-deeplink/mcp/install?name=polopan-products&config=eyJ0eXBlIjoiaHR0cCIsInVybCI6Imh0dHBzOi8vbWNwLXNlcnZlci5wb2xvcGFuLmNvbS9tY3AiLCJoZWFkZXJzIjp7fX0=)

**Primary link** (`mcp-server.polopan.com`):

`cursor://anysphere.cursor-deeplink/mcp/install?name=polopan-products&config=eyJ0eXBlIjoiaHR0cCIsInVybCI6Imh0dHBzOi8vbWNwLXNlcnZlci5wb2xvcGFuLmNvbS9tY3AiLCJoZWFkZXJzIjp7fX0=`

**Alternate** (direct Cloud Run hostname, same service):

`cursor://anysphere.cursor-deeplink/mcp/install?name=polopan-products&config=eyJ0eXBlIjoiaHR0cCIsInVybCI6Imh0dHBzOi8vcG9sb3Bhbi1tY3AtcHJvZHVjdHMtMTA0MDUyMDQwMjMwMC5hc2lhLXNvdXRoZWFzdDEucnVuLmFwcC9tY3AiLCJoZWFkZXJzIjp7fX0=`

**Browser fallback** (HTTPS landing page that redirects into Cursor — use **`en-US`** path; config uses standard base64 **with** padding):

`https://cursor.com/en-US/install-mcp?name=polopan-products&config=eyJ0eXBlIjoiaHR0cCIsInVybCI6Imh0dHBzOi8vbWNwLXNlcnZlci5wb2xvcGFuLmNvbS9tY3AiLCJoZWFkZXJzIjp7fX0=`

#### is `polopan.com/mcp/cursor` the same as hosted MCP?

not necessarily. links whose `config=` decodes to **`{"type":"stdio","command":"npx","args":["-y","polopan-products-mcp"]}`** install the **local npm stdio** binary — not the HTTP server. example:

`https://cursor.com/en-US/install-mcp?name=polopan-products&config=eyJ0eXBlIjoic3RkaW8iLCJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsInBvbG9wYW4tcHJvZHVjdHMtbWNwIl19`

that matches your pasted URL: it points at **npx + polopan-products-mcp**, not at Cloud Run. for uninterrupted hosted MCP, `config` must use **`type":"http"`** and your **`…/mcp`** URL (links above). update **`polopan.com/mcp/cursor`** to use **`cursor://…/mcp/install`** or **`https://cursor.com/en-US/install-mcp`** with an **`http`** config if marketing should match hosted docs.

### recommended for uninterrupted connection: hosted MCP (manual)

add this to your `~/.cursor/mcp.json`:

**canonical domain**

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

**or direct Cloud Run URL**

```json
{
  "mcpServers": {
    "polopan-products": {
      "type": "http",
      "url": "https://polopan-mcp-products-1040520402300.asia-southeast1.run.app/mcp",
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

### find from image

```text
use this image and find similar products.
then show only pants or trousers style options with links and sizes.
if exact trousers are not available, show the closest bottom-wear options.
```

### look for cheaper options

```text
i want a printed shirt in the 1501-3000 budget range for a date night.
then give me best complete outfits based on the top option to complete the set.
```

### wedding guest outfits

```text
i need outfit ideas for a wedding evening function.
give me 10 complete looks in xl to 3xl.
split into: under 5k, 5k-10k, and premium.
include footwear, bag, and earrings in every look.
```
