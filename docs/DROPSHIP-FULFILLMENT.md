# Ochema — Dropship Fulfillment System

> No stock. No warehouse. Smart ordering. Fast shipping.
> JSON product graphs + dependency chains + agent assistance.

---

## The Concept

**When someone buys a "Grimoire Pack," we don't hold inventory.**

Instead:
1. Customer buys the pack on Etsy/Shopify
2. System reads the product JSON (what's in the pack)
3. System checks each component's supplier
4. System places orders with each supplier
5. Components ship directly to customer
6. Customer receives multiple packages (or assembled if needed)

**The JSON defines what's in each pack. The graph defines where each component comes from. The agent helps the customer navigate.**

---

## Product JSON Structure

### Grimoire Pack Definition

```json
{
  "product_id": "grimoire_pack_key_of_solomon_starter",
  "name": "Key of Solomon Starter Kit",
  "tier": "starter",
  "price": 25,
  "charity_percent": 5,
  "components": [
    {
      "component_id": "printed_grimoire",
      "name": "Key of Solomon (Paperback)",
      "type": "book",
      "supplier": "ingramspark",
      "sku": "KOS-PB-2024",
      "cost": 3.50,
      "ships_together": false,
      "lead_time_days": 5,
      "tracking": true
    },
    {
      "component_id": "chime_candle",
      "name": "Protection Candle (Blue)",
      "type": "candle",
      "supplier": "aromags",
      "sku": "CANDLE-BLUE-4IN",
      "cost": 0.50,
      "ships_together": true,
      "lead_time_days": 3,
      "tracking": true
    },
    {
      "component_id": "protection_oil",
      "name": "Protection Oil (5ml)",
      "type": "oil",
      "supplier": "aromags",
      "sku": "OIL-PROTECTION-5ML",
      "cost": 1.50,
      "ships_together": true,
      "lead_time_days": 3,
      "tracking": true
    },
    {
      "component_id": "herb_bundle",
      "name": "Rosemary & Sage Bundle",
      "type": "herbs",
      "supplier": "mountainrose",
      "sku": "HERB-RS-BUNDLE",
      "cost": 0.50,
      "ships_together": true,
      "lead_time_days": 4,
      "tracking": true
    },
    {
      "component_id": "sigil_card",
      "name": "Protection Sigil Card",
      "type": "card",
      "supplier": "prodigi",
      "sku": "SIGIL-PROTECT-A5",
      "cost": 0.20,
      "ships_together": true,
      "lead_time_days": 2,
      "tracking": true
    },
    {
      "component_id": "ritual_guide",
      "name": "Ritual Instruction Guide",
      "type": "guide",
      "supplier": "prodigi",
      "sku": "GUIDE-PROTECT-A5",
      "cost": 0.20,
      "ships_together": true,
      "lead_time_days": 2,
      "tracking": true
    },
    {
      "component_id": "drawstring_bag",
      "name": "Cotton Drawstring Bag",
      "type": "packaging",
      "supplier": "alibaba",
      "sku": "BAG-COTTON-M",
      "cost": 0.30,
      "ships_together": true,
      "lead_time_days": 7,
      "tracking": false
    }
  ],
  "shipping_groups": [
    {
      "group_id": "aromags_batch",
      "supplier": "aromags",
      "components": ["chime_candle", "protection_oil"],
      "ships_together": true,
      "lead_time_days": 3
    },
    {
      "group_id": "prodigi_batch",
      "supplier": "prodigi",
      "components": ["sigil_card", "ritual_guide"],
      "ships_together": true,
      "lead_time_days": 2
    },
    {
      "group_id": "mountainrose_batch",
      "supplier": "mountainrose",
      "components": ["herb_bundle"],
      "ships_together": true,
      "lead_time_days": 4
    },
    {
      "group_id": "ingramspark_batch",
      "supplier": "ingramspark",
      "components": ["printed_grimoire"],
      "ships_together": true,
      "lead_time_days": 5
    },
    {
      "group_id": "alibaba_batch",
      "supplier": "alibaba",
      "components": ["drawstring_bag"],
      "ships_together": true,
      "lead_time_days": 7
    }
  ],
  "total_cost": 6.70,
  "estimated_delivery_days": 7,
  "packages_expected": 5
}
```

---

## Supplier Registry

```json
{
  "suppliers": {
    "aromags": {
      "name": "AromaG's Botanica",
      "url": "aromags.com",
      "type": "occult_supplies",
      "location": "Nashville, TN, USA",
      "api": null,
      "ordering": "wholesale_portal",
      "lead_time_days": 3,
      "shipping": "US domestic + international",
      "minimum_order": null,
      "notes": "25+ years in business. Wholesale available."
    },
    "mountainrose": {
      "name": "Mountain Rose Herbs",
      "url": "mountainroseherbs.com",
      "type": "herbs_oils",
      "location": "Oregon, USA",
      "api": null,
      "ordering": "wholesale_portal",
      "lead_time_days": 4,
      "shipping": "US domestic + international",
      "minimum_order": null,
      "notes": "Organic, sustainably sourced."
    },
    "prodigi": {
      "name": "Prodigi",
      "url": "prodigi.com",
      "type": "print_on_demand",
      "location": "UK, US, EU, AU",
      "api": "https://api.prodigi.com/v4.0",
      "ordering": "api",
      "lead_time_days": 2,
      "shipping": "Worldwide",
      "minimum_order": 1,
      "notes": "Native Etsy integration. API available."
    },
    "ingramspark": {
      "name": "IngramSpark",
      "url": "ingramspark.com",
      "type": "book_printing",
      "location": "Global POD",
      "api": "https://api.ingramspark.com",
      "ordering": "api",
      "lead_time_days": 5,
      "shipping": "45,000+ retailers worldwide",
      "minimum_order": 1,
      "notes": "Print on demand. Global distribution."
    },
    "alibaba": {
      "name": "Alibaba",
      "url": "alibaba.com",
      "type": "packaging_supplies",
      "location": "China",
      "api": null,
      "ordering": "manual",
      "lead_time_days": 7,
      "shipping": "Worldwide",
      "minimum_order": 100,
      "notes": "Bulk ordering. Longer lead time."
    },
    "kunaki": {
      "name": "Kunaki",
      "url": "kunaki.com",
      "type": "cd_dvd_printing",
      "location": "Nevada, USA",
      "api": "https://www.kunaki.com/api",
      "ordering": "api_xml",
      "lead_time_days": 1,
      "shipping": "Worldwide",
      "minimum_order": 1,
      "notes": "24hr production. Dropship via XML API."
    },
    "makr3d": {
      "name": "Makr3D",
      "url": "makr3d.app",
      "type": "3d_printing",
      "location": "Huddersfield, UK",
      "api": "https://makr3d.app/api/v1",
      "ordering": "api",
      "lead_time_days": 2,
      "shipping": "Worldwide",
      "minimum_order": 1,
      "notes": "24hr production. White-label. Etsy sync."
    },
    "stamprints": {
      "name": "Stamprints",
      "url": "stamprints.com",
      "type": "wax_seals",
      "location": "China/USA",
      "api": null,
      "ordering": "web_portal",
      "lead_time_days": 5,
      "shipping": "Worldwide",
      "minimum_order": 1,
      "notes": "Custom brass wax seals."
    },
    "tttjewelry": {
      "name": "TTTJewelry",
      "url": "tttjewelry.com",
      "type": "metal_jewelry",
      "location": "China",
      "api": null,
      "ordering": "wholesale",
      "lead_time_days": 14,
      "shipping": "Worldwide",
      "minimum_order": 50,
      "notes": "Brass/silver custom pieces."
    }
  }
}
```

---

## Dependency Graph

```
GRIMOIRE PACK (starter)
├── Book (IngramSpark) ──── API ────→ Printed → Shipped (5 days)
├── Candle (AromaG's) ───── Manual ──→ Wholesale order → Shipped (3 days)
├── Oil (AromaG's) ──────── Manual ──→ Same order as candle
├── Herbs (Mountain Rose) ─ Manual ──→ Wholesale order → Shipped (4 days)
├── Sigil Card (Prodigi) ── API ────→ Printed → Shipped (2 days)
├── Guide (Prodigi) ─────── API ────→ Same order as sigil card
└── Bag (Alibaba) ────────── Manual ─→ Bulk order (pre-ordered) → Shipped (7 days)

Fulfillment Flow:
1. Customer buys pack on Etsy
2. System reads JSON → knows all components
3. System checks each supplier's stock/lead time
4. System places API orders (Prodigi, IngramSpark, Makr3D, Kunaki)
5. System places manual orders (AromaG's, Mountain Rose)
6. Each supplier ships directly to customer
7. Customer receives 4-5 packages
8. Tracking numbers sent to customer
```

---

## Fulfillment Scenarios

### Scenario 1: All Suppliers Have Stock

```
Customer buys Key of Solomon Starter Kit ($25)
  → System places orders with 5 suppliers
  → Prodigi prints sigil card + guide (2 days)
  → IngramSpark prints book (5 days)
  → AromaG's ships candle + oil (3 days)
  → Mountain Rose ships herbs (4 days)
  → Alibaba ships bag (7 days, pre-ordered batch)
  → Customer receives 5 packages over 7 days
  → Total customer wait: 7 days (slowest supplier)
```

### Scenario 2: Fast Ship (Digital-Only Pack)

```
Customer buys Digital Grimoire Pack ($5)
  → System delivers PDF immediately
  → No physical shipping
  → Customer has instant access
  → Links to Amazon for physical edition
```

### Scenario 3: Pre-Assembled Option

```
Customer buys Assembled Kit ($35)
  → System orders all components to our assembly address
  → We assemble kit in-house
  → Ship as single package
  → Total wait: 10 days (assembly adds time)
  → Premium price for convenience
```

---

## The Agent

### What It Does

The Ochema agent helps customers navigate the platform:

| Task | Agent Action |
|------|-------------|
| **"I want to learn about protection spells"** | Shows relevant grimoires, YouTube videos, spell kits |
| **"What's in the Key of Solomon starter kit?"** | Lists all components, suppliers, shipping times |
| **"Generate my birth chart"** | Collects birth data, generates natal chart |
| **"What tarot spread should I use?"** | Recommends spreads based on question |
| **"Match me with someone by birth chart"** | Shows compatible practitioners |
| **"I want to buy the Deluxe edition"** | Links to Etsy/Shopify product |

### Agent Architecture

```
Customer Query
  → Intent Recognition (what do they want?)
  → Knowledge Base (grimoires, spells, products)
  → Action (recommend, generate, link, search)
  → Response (helpful, scholarly, honest)
```

### Agent Prompts

```
System: You are the Ochema assistant. You help practitioners
navigate grimoires, generate birth charts, find products, and
connect with the community. You are scholarly, warm, and honest
about what you know and don't know. You never promise magical
results. You reference historical sources when discussing spells
or rituals.

User: [query]

Assistant: [helpful response with links to relevant content]
```

---

## Fast Shipping Strategy

### The Problem
5 suppliers = 5 packages = confused customer.

### The Solutions

| Strategy | How It Works | Customer Experience |
|----------|-------------|-------------------|
| **Supplier grouping** | Order all AromaG's items together | 1 package from AromaG's |
| **Pre-ordered batches** | Alibaba items pre-ordered in bulk | Ships faster |
| **Local assembly** | Assemble kits in-house | Single package |
| **Digital-first** | Deliver digital immediately, physical ships later | Instant gratification |
| **Transparent tracking** | Show all packages + tracking numbers | Customer knows what's coming |

### Shipping Time Targets

| Component | Supplier | Lead Time |
|-----------|----------|-----------|
| Printed cards/guides | Prodigi | 2 days |
| Books | IngramSpark | 5 days |
| Candles/oils | AromaG's | 3 days |
| Herbs | Mountain Rose | 4 days |
| Packaging | Alibaba (pre-ordered) | 1-7 days |
| **Total (worst case)** | | **7 days** |
| **Total (typical)** | | **5 days** |

---

## Implementation

### Phase 1: Manual Fulfillment (Month 1)
- [ ] Create product JSONs for all packs
- [ ] Map each component to supplier
- [ ] Set up wholesale accounts (AromaG's, Mountain Rose)
- [ ] Test ordering flow manually
- [ ] Track shipping times

### Phase 2: Semi-Automated (Month 2-3)
- [ ] Connect Prodigi API (cards, guides)
- [ ] Connect IngramSpark API (books)
- [ ] Connect Makr3D API (3D prints)
- [ ] Build order routing script
- [ ] Automated tracking number collection

### Phase 3: Fully Automated (Month 4-6)
- [ ] Connect all supplier APIs
- [ ] Automated order placement on sale
- [ ] Automated tracking sync to Etsy
- [ ] Customer notification system
- [ ] Agent integration

---

## Cost Analysis

### Per Kit ($25 Starter Kit)

| Component | Supplier | Cost | Ships |
|-----------|----------|------|-------|
| Book | IngramSpark | $3.50 | 5 days |
| Candle | AromaG's | $0.50 | 3 days |
| Oil | AromaG's | $1.50 | 3 days |
| Herbs | Mountain Rose | $0.50 | 4 days |
| Sigil card | Prodigi | $0.20 | 2 days |
| Guide | Prodigi | $0.20 | 2 days |
| Bag | Alibaba | $0.30 | 7 days |
| **Materials** | | **$6.70** | |
| Shipping (avg) | Multiple | $4.00 | |
| Platform fees | Etsy | $2.50 | |
| **Total cost** | | **$13.20** | |
| **Retail price** | | **$25.00** | |
| **Profit** | | **$11.80** | |
| **Charity (5%)** | | **$1.25** | |
| **Net** | | **$10.55** | |

**Margin: 42%** (before taxes, overhead, marketing)
