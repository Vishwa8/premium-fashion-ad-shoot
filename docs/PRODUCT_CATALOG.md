# Ayurti Multi-Product Catalog Architecture

## 1. System Vision & Architecture
Ayurti is designed as an industrial-grade, multi-product generative fashion pipeline with a strict **Parent-Child Architecture**:
- **Parent Level**: Holds all shared resources that are common across every product:
  - Universal influencer clean identity plates (`base/`).
  - Modular, reusable prompt templates and JSON schemas (`docs/templates/`).
  - Architectural blueprints, methodology, plan, progress tracker, and run records (`docs/`).
  - Single workspace-level `.gitignore`.
- **Child Product Packages (`products/product_XX/`)**: Holds strictly product-specific data, modularized into small, deserved chunks without any duplicate parent assets.

This guarantees:
1. **Single Source of Truth**: Every piece of data (product specs, model identity, templates) exists in exactly one authoritative location.
2. **Zero Duplication**: No duplicate base plates, global templates, or root mirrors.
3. **Separation of Concerns**: Product-specific assets are encapsulated in dedicated subdirectories (`references/`, `mockups/`, `poses/`, `videos/`, `copy/`).
4. **Infinite Scalability**: Adding `product_02`, `product_03`, etc. requires only instantiating a new package folder adhering to the child contract.

---

## 2. Directory Hierarchy Standard

```text
/mnt/1.9TB/Dev/ayuti/
├── base/                                # Universal Parent Assets (Single Source of Truth)
│   ├── base_front.png                   # Influencer front clean plate (face, jewelry, satin studio set)
│   └── base_back.png                    # Influencer back clean plate (hair, posture, satin studio set)
│
├── docs/                                # Production Blueprints, Run Records & Templates
│   ├── AI_SAMSON_METHODOLOGY.md         # 5-step character consistency & video production methodology
│   ├── ARCHITECTURE.md                  # API routing, model tiers, and compositing specifications
│   ├── PLAN.md                          # Production plan & quality verification gates
│   ├── PRODUCT_CATALOG.md               # Multi-product catalog architecture & standards
│   ├── PROGRESS.md                      # Production milestone tracker
│   ├── PROMPT_TEMPLATES.md              # Master catalog of prompt templates & schemas
│   ├── runs/                            # Execution run logs & subagent ledgers
│   │   └── 2026-11-27-premium-fashion-ad-shoot.md
│   └── templates/                       # Ingested prompt engineering library & schemas
│       ├── catalog_description/         # Luxury brand copywriting templates
│       ├── garment_mockup/              # 4-view ghost mannequin system & descriptors
│       ├── pose_and_camera/             # Pose transfer & 50+ camera angle presets
│       ├── video_generation/            # Veo 3.1 cinematography & motion safety rules
│       └── virtual_tryon/               # Identity-locked try-on schemas (v1.2 & v2.0)
│
├── products/                            # Child Products (Separation of Concerns)
│   ├── product_01/                      # Kalibherva Maroon Anarkali Gown (B0HM458PW4)
│   │   ├── product.json                 # Single source of truth for product specs
│   │   ├── references/                  # Vendor photography & detail crops (5 Amazon images)
│   │   │   ├── dress_front_full.jpg
│   │   │   ├── dress_angle_1.jpg
│   │   │   ├── dress_angle_2.jpg
│   │   │   ├── dress_detail_1.jpg
│   │   │   └── dress_detail_2.jpg
│   │   ├── mockups/                     # Isolated 3D dress sheets & locked masters
│   │   │   ├── dress_3d_front.png       # Isolated 3D dress (Front)
│   │   │   ├── dress_3d_angle_45.png    # Isolated 3D dress (45° Angle)
│   │   │   ├── dress_3d_profile_90.png  # Isolated 3D dress (90° Profile)
│   │   │   ├── dress_3d_back.png        # Isolated 3D dress (Back)
│   │   │   ├── front_master.png         # Zero-drift inpaint on base_front.png
│   │   │   ├── back_master.png          # Zero-drift inpaint on base_back.png
│   │   │   ├── closeup_portrait_native.png # Unpixelated native macro portrait
│   │   │   ├── side_by_side_master.png  # Dual-scale master contact sheet
│   │   │   └── combine_views.png        # Turnaround contact sheet (4 views)
│   │   ├── poses/                       # 5 zero-drift editorial catalog poses
│   │   ├── videos/                      # 360 loops, scene takes & commercial cut
│   │   └── copy/                        # Catalog copywriting & technical descriptors
│   │       ├── Catalog_Description.txt  # Ayurti luxury catalog description
│   │       └── garment_desc.txt         # 100-word prompt descriptor
│   │
│   ├── product_02/                      # Next onboarded garment (Template ready)
│   └── product_.../
│
└── .gitignore                           # Exclusively at workspace root (no nested .gitignore files)
```

---

## 3. Product Package Specifications (`products/product_XX/`)

Each child product package contains 6 specialized components:

### 3.1. `product.json` (Specification Single Source of Truth)
A single JSON document defining all structured product metadata:
- Product identity (`product_id`, `asin`, `title`, `brand`, `category`).
- Audience & styling guidelines (`target_audience`, `styling`).
- Colorway & undertones with hex codes (`color`).
- Fabric composition, lining, and drape physics (`fabric_blend`).
- Embroidery, zari, and embellishment specifications (`embroidery_and_zari`).
- Precise garment dimensions, kali count, and sleeve lengths (`dimensions`).
- Garment construction & neckline cuts (`construction`).
- Child paths (`paths`).

### 3.2. `references/` (Raw Source Photography)
Holds the unedited vendor photography, angle shots, and high-resolution fabric/embroidery crops used as vision conditioning anchors.

### 3.3. `mockups/` (Isolated 3D Views & Locked Masters)
Contains:
1. Isolated 4-view 3D ghost mannequin dress turnaround (`dress_3d_front.png`, `dress_3d_angle_45.png`, `dress_3d_profile_90.png`, `dress_3d_back.png`).
2. Locked front and back masters (`front_master.png`, `back_master.png`).
3. Unpixelated native macro portrait (`closeup_portrait_native.png`).
4. Dual-scale master sheet (`side_by_side_master.png`).
5. Turnaround contact sheet (`combine_views.png`).

### 3.4. `poses/` (Editorial Catalogue Poses)
Holds the 5 curated zero-drift editorial poses representing realistic catalog movements.

### 3.5. `videos/` (Video Productions)
Contains the 360° turnaround loops, individual cinematic scene takes, and final edited 25s commercial reel.

### 3.6. `copy/` (Marketing & Prompt Copy)
Contains product-specific luxury copy:
- `Catalog_Description.txt`: High-converting luxury catalog listing copy.
- `garment_desc.txt`: Concise 100-word technical garment descriptor for prompt injection.
