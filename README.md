# Premium Fashion Ad Shoot: Ayurti

Zero-drift virtual influencer fashion campaign and catalogue production featuring the Kalibherva Embellished Maroon Anarkali Gown (`Amazon ASIN: B0HM458PW4`).

## Architecture & Hierarchy: Parent-Child Single Source of Truth

The workspace is organized into a clean **Parent-Child architecture** with strict separation of concerns and single source of truth across all products:

```text
.
├── base/                           # Universal Parent Assets (Single Source of Truth)
│   ├── base_front.png              # Master influencer front clean plate (face, jewelry, satin studio set)
│   └── base_back.png               # Master influencer back clean plate (hair, posture, satin studio set)
│
├── docs/                           # Architecture, Methodology, Run Logs & Templates
│   ├── AI_SAMSON_METHODOLOGY.md    # 5-step character consistency & video production methodology
│   ├── ARCHITECTURE.md             # API routing, model tiers, and compositing specifications
│   ├── PLAN.md                     # Production plan & quality verification gates
│   ├── PRODUCT_CATALOG.md          # Multi-product catalog architecture & standards
│   ├── PROGRESS.md                 # Production milestone tracker
│   ├── PROMPT_TEMPLATES.md         # Master catalog of prompt templates & schemas
│   ├── runs/                       # Execution run logs & subagent ledgers
│   │   └── 2026-11-27-premium-fashion-ad-shoot.md
│   └── templates/                  # Modular, reusable prompts & JSON schemas
│       ├── catalog_description/    # Luxury catalog description generators
│       ├── garment_mockup/         # 4-view ghost mannequin system & descriptors
│       ├── pose_and_camera/        # Pose transfer & 50+ camera angle presets
│       ├── video_generation/       # Veo 3.1 cinematography & motion safety rules
│       └── virtual_tryon/          # Identity-locked try-on schemas (v1.2 & v2.0)
│
├── products/                       # Child Products (Separation of Concerns, Deserved Small Chunks)
│   └── product_01/                 # Kalibherva Maroon Anarkali Gown (B0HM458PW4)
│       ├── product.json            # Master product specification metadata
│       ├── references/             # Raw vendor photography & detail crops (5 Amazon images)
│       ├── mockup/                 # 4-view 3D dress turnaround, locked masters, macro closeup, dual-scale sheet
│       │   ├── dress_3d_front.png
│       │   ├── dress_3d_angle_45.png
│       │   ├── dress_3d_profile_90.png
│       │   ├── dress_3d_back.png
│       │   ├── front_master.png
│       │   ├── back_master.png
│       │   ├── closeup_portrait_native.png
│       │   ├── side_by_side_master.png
│       │   ├── combine_views.png
│       │   └── garment_4view_sheet_1k.png
│       ├── description/            # Catalog description, garment technical descriptors & product info
│       │   ├── Catalog_Description.txt
│       │   ├── garment_desc.txt
│       │   └── PRODUCT_INFO.md
│       ├── poses/                  # Curated zero-drift editorial catalogue poses
│       ├── videos/                 # 360 turnarounds, individual scene takes & commercial cut
│       └── logs/                   # Product run logs & cost tracking
│           ├── cost_tracker.csv
│           └── run_logs.json
│
└── .gitignore                      # Exclusively at workspace root (no nested .gitignore files)
```

## Principles
1. **Single Source of Truth**: `base/` holds the canonical model identity plates. Product specs are stored solely in `products/product_XX/product.json`. Modular schemas and prompts live in `docs/templates/`.
2. **Zero Duplication**: No copies of base plates, global templates, or cross-cutting tools exist inside child product packages.
3. **Strict Separation of Concerns**: Each product package is completely self-contained in its deserved small chunks (`references/`, `mockup/`, `poses/`, `videos/`, `description/`, `logs/`).
4. **Single Root Gitignore**: Git exclusions are maintained exclusively at the workspace root `.gitignore`.
