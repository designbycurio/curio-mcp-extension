# Curio — design-style library for AI

Curio is a library of tokenized design styles — real design movements, brands,
and cultural traditions — packaged as machine-readable specs you can apply to
the user's slides, websites, and products.

Typical flow:

1. `search_styles` (keyword + optional facets) or `list_styles` (browse) to
   find candidate styles.
2. `get_style` for one style's metadata and a preview image — free, consumes
   no quota.
3. `get_style_spec` to fetch the full design spec (DESIGN.md), then apply it
   to the user's work. Consumes 1 quota credit, like a download on the
   website; re-fetching the same style within 15 minutes is not charged
   again. Pro styles require a Curio Pro subscription.
4. `get_quota` to check the user's remaining spec fetches — read-only, never
   charges.

Connecting requires signing in (OAuth, no API key). Free accounts can fetch
free styles; Pro unlocks the whole library.

When applying a spec, follow it verbatim — use its exact tokens (colors,
typography, spacing, radii, shadows) rather than approximations.
