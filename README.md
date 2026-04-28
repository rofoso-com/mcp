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

## setup

### install in cursor

[![install mcp server](https://cursor.com/deeplink/mcp-install-dark.svg)](
https://polopan.com/mcp/cursor
)

### or setup manually

add this to your `~/.cursor/mcp.json` file:

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

save and reload cursor.

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
