# 🦆 DGCP™ Controlled Vocabulary (CV) v1.0.0  
### Standardized Terms for Work Types, Tags, and Context Fields

This document establishes the **canonical vocabulary** used throughout  
the DGCP Metadata Standard (DMS), Validator, FHA Audit, and Indexing Layer.

The goal of the CV is to ensure:
- shared language  
- consistency across industries  
- global interoperability  
- fairness in interpretation  
- ethical research usability  

---

# 1. Principles of Controlled Vocabulary

DGCP’s Controlled Vocabulary is designed to be:

1. **Human-first** — All terms must be understandable by non-technical workers.  
2. **Cross-cultural** — Terms must be usable in any country.  
3. **Non-surveillance** — No terms may encode sensitive identity or GPS information.  
4. **Expandable** — New categories may be added without breaking old proofs.  
5. **Append-only** — Existing terms may not be renamed or removed.  

---

# 2. Core Vocabulary Categories

DGCP v1.0.0 defines three primary vocabulary sets:

1. **Work Types** (`work_type`)  
2. **Context Tags** (`tags`)  
3. **Environmental & Seasonal Labels**  

These categories serve as the backbone for indexing, auditing, and research.

---

# 3. WORK TYPE Vocabulary

Work types describe broad categories of human labor.  
They MUST be:

- simple  
- universal  
- non-technical  
- understandable by humans and machines  

### 3.1 Agriculture

| Term | Meaning |
|------|---------|
| `duck_care` | Feeding, cleaning, checking health of ducks |
| `egg_collection` | Collecting eggs, weighing eggs |
| `field_maintenance` | Clearing weeds, watering, soil care |
| `crop_harvest` | Harvesting crops like papaya, banana leaves |
| `animal_shelter_upkeep` | Repairing and maintaining pens, coops |
| `feeding_animals` | Feeding dogs, ducks, chickens |
| `water_management` | Managing pumps, wells, irrigation |

### 3.2 Household Survival Work

| Term | Meaning |
|------|---------|
| `food_preparation` | Preparing food from limited resources |
| `daily_survival_tasks` | Work required due to poverty constraints |
| `resource_collection` | Collecting firewood, water |

### 3.3 Infrastructure & Repair

| Term | Meaning |
|------|---------|
| `structural_repair` | Fixing roofs, fences, small shelters |
| `tool_maintenance` | Fixing equipment, simple tools |

### 3.4 Documentation & System Work

| Term | Meaning |
|------|---------|
| `proof_documentation` | Capturing photos/videos for DGCP |
| `data_entry` | Recording daily logs, weights, notes |
| `system_governance` | Writing governance, specs, protocol files |
| `indexing_preparation` | Organizing files for registry/indexer |

### 3.5 Mobility Work

| Term | Meaning |
|------|---------|
| `supply_walk` | Walking to buy food or supplies |
| `transport_light` | Carrying small loads manually |

---

# 4. TAG Vocabulary

Tags provide flexible, contextual metadata.  
These MUST remain open and human-defined, but DGCP provides a standard starter set.

### 4.1 Environmental Tags

| Tag | Meaning |
|------|---------|
| `weather:hot` | High temperature |
| `weather:cold` | Low temperature |
| `weather:rain` | Rainfall |
| `season:dry` | Dry season |
| `season:wet` | Wet season |
| `light:low` | Low light conditions |
| `temperature:<value>` | Optional numeric reading |

### 4.2 Equipment Tags

| Tag | Meaning |
|------|---------|
| `equipment:water_pump` | Using a water pump |
| `equipment:solar_light` | Solar light involved |
| `equipment:thermometer` | Low-cost thermometer used |
| `equipment:hand_tool` | Manual tools |

### 4.3 Animal Tags

| Tag | Meaning |
|------|---------|
| `animal:duck` | Duck involved |
| `animal:dog` | Dog involved |
| `animal:7_ducks` | Core symbolic group |
| `animal:puppies` | Young dogs present |

### 4.4 Contextual Hardship Tags

| Tag | Meaning |
|------|---------|
| `context:poverty_constraint` | Limited resources |
| `context:no_electricity` | Area has insufficient electricity |
| `context:manual_labor` | Work done without machines |
| `context:limited_food` | Scarce food access |

---

# 5. Location Labels (Non-GPS)

DGCP enforces **coarse labels only**.  
Example v1.0.0 labels:

| Label | Description |
|------|-------------|
| `MaMeeFarm, Lampang` | Rural agricultural lab of MaMeeFarm™ |
| `Community-Farm` | Generic small farm location |
| `Local-Village-Region` | Coarse village region |

Workers can create custom coarse labels, as long as they DO NOT include:

- GPS  
- Addresses  
- House numbers  
- Identifying data  

---

# 6. Rules for Adding New Vocabulary

New terms MUST follow:

1. **Append-only rule** — Cannot modify old terms.  
2. **Human-review rule** — All new terms approved by FHA Global Council.  
3. **Universality rule** — Term must make sense globally.  
4. **Neutrality rule** — Cannot encode identity, caste, or surveillance metadata.  

---

# 7. Versioning

Vocabulary updates follow semantic versioning:

- **Patch** (v1.0.1): Add optional new tags  
- **Minor** (v1.1.0): Add new work types  
- **Major** (v2.0.0): Only when structure changes (rare)  

Old proofs remain valid forever.

---

# 8. License

Governed under  
**MMFARM-POL-2025**  
with **CC BY-NC 4.0** compatibility.

