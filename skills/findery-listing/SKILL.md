---
name: findery-listing
description: Create optimized resale listings for The Findery using Ryan's required listing structure, pricing logic, compliance rules, category-specific specs, and fun professional sales tone.
---

# Findery Listing Skill

Use this skill whenever creating, rewriting, auditing, or improving a product listing for The Findery, especially for eBay, Shopify, Mercari, or Facebook Marketplace.

## Core Goal

Create accurate, search-optimized, buyer-friendly listings that help sell the item while protecting The Findery from bad details, bad UPCs, weak titles, missing specs, missing shipping notes, and platform compliance issues.

## Required Inputs

Ask for or infer from supplied photos/text when possible:

- Brand
- Model number or SKU
- Product type
- Finish, color, size, or variant
- Condition
- What's included
- What's missing or uncertain
- Target platform
- Known cost, retail price, or target price
- Shipping weight and box dimensions when available

## Required Behavior

1. Identify the product as accurately as possible.
2. Use brand, model number, finish, type, and important buyer search keywords.
3. Create an optimized eBay title under 80 characters when writing for eBay.
4. Never include external website links in the final listing.
5. Never include Amazon links in the final listing.
6. Double-check UPCs before including them.
7. If UPC confidence is low, say so instead of guessing.
8. Use varied condition descriptions so listings do not sound repetitive.
9. Include product-specific specs whenever relevant.
10. Include shipping details when known.
11. Finish with a buyer-friendly call to action.

## Default Listing Format

Use this structure unless the user asks for something different:

1. Optimized Title
2. Condition Description
3. Retail Price / Price Strategy
4. Short Product Description
5. Key Features
6. Specifications
7. What's Included
8. Shipping Details
9. California Proposition 65 Warning, when applicable
10. Call to Action

## Tone

Use a fun, sharp, professional resale tone. The listing should feel polished but not stiff. A little personality is good. Do not overdo it.

## Compliance Rules

- No external links.
- Do not include Amazon links.
- Do not claim factory sealed unless verified.
- Do not claim complete unless all parts are verified.
- Do not guess UPCs, dimensions, compatibility, or certifications.
- For open-box items, explain that packaging may show wear while the product may still be unused.
- Clearly state uncertainty instead of filling gaps with confident-sounding guesses.

## Pricing Rules

- For non-plumbing items, the target list price may be inflated by 15% and then placed on a 15% sale to land near the intended price.
- For plumbing items, do not inflate the list price. Use the current brand/retail sale price as the retail baseline when known, then apply the intended markdown logic.
- When comps are uncertain, provide a conservative price range and explain the reason.

## Category Rules

### Plumbing

Include when available:

- Brand
- Model number
- Finish
- Collection
- Installation type
- Flow rate
- Spout height
- Spout reach
- Base or escutcheon/back plate dimensions
- Valve compatibility
- Certifications
- UPC, only when verified
- What is included
- What is missing, if anything
- California Proposition 65 warning, when applicable

### Sinks

Include when available:

- Overall dimensions
- Inner bowl dimensions
- Bowl depth
- Mounting type
- Material
- Drain location
- Minimum cabinet size
- Included accessories
- Visible damage or cosmetic issues

### Women's Shoes

Include when available:

- Brand
- Style name
- US size
- EU/UK/AU conversions when known
- Heel height
- Upper material
- Lining material
- Insole material
- Outsole material
- Condition notes

### Clothing

Include when available:

- Brand
- Size
- Measurements when available
- Material
- Style keywords
- Condition notes
- Fit notes when useful

### Lighting

Include when available:

- Brand
- Model number
- Fixture type
- Finish
- Dimensions
- Number of lights
- Bulb type
- Voltage
- Mounting type
- Included hardware
- Shade/globe condition

## Final Quality Check

Before final answer, verify:

- Title is under 80 characters for eBay.
- No external links are included.
- UPC is either verified or marked uncertain.
- Condition description is not stale or repetitive.
- Key buyer specs are included.
- Any uncertainty is clearly stated.
- Listing copy is ready to paste without forbidden links or unsupported claims.
