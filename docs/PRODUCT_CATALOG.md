# Ayurti Multi-Product Catalog Architecture

## 1. System Vision & Architecture
Ayurti is designed as an industrial-grade, multi-product generative fashion pipeline. Rather than treating shoots as ad-hoc experiments, every garment is indexed as an independent product package under `products/product_XX/`. 

This guarantees:
1. **Isolated Product Envelopes**: All references, isolated 3D mockups, locked front/back masters, editorial poses, videos, and copywriting live together in a dedicated directory.
2. **Scalability**: New garments can be onboarded seamlessly without file collisions or naming ambiguity.
3. **Backward Compatibility**: Top-level root directories (`mockup/`, `poses/`, `videos/`) serve as clean active mirrors for the currently active campaign (Product 01), ensuring zero disruption to existing tools, pipelines, or subagents.

---

## 2. Directory Hierarchy Standard

```text
/mnt/1.9TB/Dev/ayuti/
├── base/                                # Universal studio & identity anchors
│   ├── base_front.png                   # Influencer front master (face, jewelry, satin set)
│   └── base_back.png                    # Influencer back master (hair, posture, satin set)
│
├── products/                            # Multi-Product Storage Hub
│   ├── product_01/                      # Kalibherva Maroon Anarkali Gown (B0HM458PW4)
│   │   ├── PRODUCT_INFO.md              # Technical garment specification & metadata
│   │   ├── mockup_prompt.txt            # Adapted 4-view turnaround generation prompt
│   │   ├── tryon_config.json            # Structured v2.0 virtual try-on configuration
│   │   ├── video_front_config.json      # Veo 3.1 front-view video generation schema
│   │   ├── video_back_config.json       # Veo 3.1 rear-view video generation schema
│   │   ├── references/                  # Vendor photography & detail crops
│   │   │   ├── dress_front_full.jpg
│   │   │   ├── dress_angle_1.jpg
│   │   │   ├── dress_angle_2.jpg
│   │   │   ├── dress_detail_1.jpg
│   │   │   └── dress_detail_2.jpg
│   │   ├── mockup/                      # Isolated 3D sheets & locked masters
│   │   │   ├── dress_3d_front.png       # Isolated 3D dress (Front)
│   │   │   ├── dress_3d_angle_45.png    # Isolated 3D dress (45° Angle)
│   │   │   ├── dress_3d_profile_90.png  # Isolated 3D dress (90° Profile)
│   │   │   ├── dress_3d_back.png        # Isolated 3D dress (Back)
│   │   │   ├── front_master.png         # Zero-drift inpaint on base_front.png
│   │   │   └── back_master.png          # Zero-drift inpaint on base_back.png
│   │   ├── poses/                       # 5 zero-drift editorial catalog poses
│   │   ├── videos/                      # 360 loops, scene takes & commercial cut
│   │   └── description/                 # Catalog copywriting & technical descriptors
│   │       ├── Catalog_Description.txt  # Ayurti luxury catalog description
│   │       └── garment_desc.txt         # 100-word prompt descriptor
│   │
│   ├── product_02/                      # Next onboarded garment (Template ready)
│   └── product_.../
│
├── mockup/                              # Clean mirror to active product (Product 01)
├── poses/                               # Clean mirror to active product (Product 01)
├── videos/                              # Clean mirror to active product (Product 01)
│
├── docs/                                # Production blueprints & templates
│   ├── templates/                       # Ingested prompt engineering library
│   │   ├── garment_mockup/              # 4-view ghost mannequin system & descriptors
│   │   ├── virtual_tryon/               # Identity-locked try-on schemas (v1.2 & v2.0)
│   │   ├── pose_and_camera/             # Pose transfer & 50+ camera angle presets
│   │   ├── video_generation/            # Veo 3.1 cinematography & motion safety rules
│   │   └── catalog_description/         # Luxury brand copywriting templates
│   ├── PROMPT_TEMPLATES.md              # Detailed documentation of all prompt schemas
│   ├── PRODUCT_CATALOG.md               # Multi-product catalog documentation (this file)
│   ├── AI_SAMSON_METHODOLOGY.md         # Production standards & verification gates
│   ├── ARCHITECTURE.md                  # API routing, 9Router, and compositing rules
│   └── PLAN.md                          # Milestone execution roadmap
│
└── generations/                         # Run telemetry, logs, and cost audit
    ├── cost_tracker.csv                 # Metered spend per generation step
    ├── run_logs.json                    # API payload and response ledger
    └── PROMPTS.md                       # Executed generation prompts ledger
```

---

## 3. Product 01 Catalog Record

| Field | Detail |
| :--- | :--- |
| **Product Identifier** | `product_01` |
| **Garment Title** | Kalibherva Embellished Maroon Anarkali Gown with Zari & Tassels |
| **Vendor Marketplace** | Amazon India (`ASIN: B0HM458PW4`) |
| **Fabric & Construction** | Heavy Faux Georgette with micro-crepe lining; 16 flared kalis; fitted bodice |
| **Colorway** | Imperial Maroon / Wine (`#4A0E17`) |
| **Embellishment** | Antique golden zari embroidery bib yoke, micro-sequins, sleeve border, rear latkan tassels |
| **Primary Reference Source** | `products/product_01/references/dress_front_full.jpg` |
| **Isolated Mockup Status** | **Complete** (`products/product_01/mockup/dress_3d_*.png`) |
| **Locked Masters Status** | **Complete** (`products/product_01/mockup/front_master.png`, `back_master.png`) |
| **Active Campaign** | **Yes** (mirrored at top-level `mockup/`, `poses/`, `videos/`) |

---

## 4. Standard Onboarding Procedure for New Products

When adding `product_02`, `product_03`, etc.:
1. **Directory Provisioning**:
   ```bash
   mkdir -p products/product_XX/{references,mockup,poses,videos,description}
   ```
2. **Reference Ingestion**:
   - Place front full-length, back, angle, and fabric detail vendor shots into `products/product_XX/references/`.
3. **Step 1: 4-View Isolated Turnaround Sheet**:
   - Adapt `docs/templates/garment_mockup/garment-sheet.txt` with specific neckline, kalis, and fabric descriptions.
   - Generate Front, 45°, 90°, and Back on ghost mannequin with pure white background and charcoal cavity shadows.
   - Save to `products/product_XX/mockup/`.
4. **Step 2: Base Compositing & Master Locking**:
   - Inpaint onto `base/base_front.png` and `base/base_back.png`.
   - Verify zero drift across hairstyle, skin tone, jewelry, and champagne satin backdrop.
   - Save to `products/product_XX/mockup/front_master.png` and `back_master.png`.
5. **Step 3: Dual-Scale Master & 360 Contact Sheet**:
   - Render unpixelated native high-res facial & neckline crop (`side_by_side_master.png`).
   - Assemble `combine_views.png`.
6. **Step 4: Editorial Catalog Poses**:
   - Conditioned on locked masters, select 5 poses from `docs/templates/pose_and_camera/poses-dropdown.json`.
   - Generate and verify against zero environment/jewelry drift.
7. **Step 5: Cinematography & Video Showcase**:
   - Adapt `video_front_config.json` and `video_back_config.json` for Veo 3.1 generation.
   - Execute slow push-in front and rear passes with subtle wind-blown fabric dynamics.
8. **Step 6: Luxury Copywriting**:
   - Apply `docs/templates/catalog_description/description-template.md` to produce luxury ecommerce copy in `description/Catalog_Description.txt`.
