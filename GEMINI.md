# Curio — design-style library for AI

Curio is a library of tokenized design styles — real design movements, brands,
and cultural traditions — packaged as machine-readable specs you can apply to
the user's slides, websites, and products.

Typical flow:

1. `search_styles` (keyword + optional facets) or `list_styles` (browse) to
   find candidate styles.
2. `get_style` for one style's metadata and a preview image — free.
3. `get_style_spec` to fetch the full design spec (DESIGN.md) of a style the
   user has unlocked, then apply it to the user's work. It never spends
   credits. For a style that isn't unlocked yet it returns `not_unlocked`
   with the cost (1 credit) and the user's balance.
4. If the user wants that style, ask them first. Only after they agree, call
   `unlock_style`: it spends 1 credit, unlocks the style for good and returns
   the spec. Styles they already own are never charged again; with too few
   credits it returns `insufficient_credits` and a link to buy more.
5. `get_balance` to check the user's credits — read-only.

Connecting requires signing in (OAuth, no API key). Every style costs 1
credit to unlock; credit packs never expire.

When applying a spec, follow it verbatim — use its exact tokens (colors,
typography, spacing, radii, shadows) rather than approximations.
