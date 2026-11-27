# Comprehensive Architecture, Methodology & Session Documentation

**Workspace:** `/mnt/1.9TB/Dev/ayuti`  
**Repository:** `git@github.com:Vishwa8/premium-fashion-ad-shoot.git`  
**Skills Repository:** `git@github.com:Vishwa8/fashion-tech-skills.git`  
**Lead Product:** Product 01 — Kalibherva Maroon Indo-Western Anarkali Gown (`B0HM458PW4`)

---

## 1. Executive Summary & Core Objectives

The objective of this project is to build an industrial-grade, zero-drift AI fashion advertisement and virtual try-on engine for luxury South Asian and Indo-Western couture.

### Key Pillars
1. **Zero Character & Environment Drift**: 100% identity lock across face, right-side hair parting, bun texture, skin tone, hands, temple jewelry, and champagne pleated silk studio backdrop.
2. **Physically Accurate 3D Garment Geometry**: Eliminating generative diffusion artifacts such as duplicate hip drapes, inverted shoulder anchors, hollow neck/sleeve voids, and inconsistent embroidery.
3. **Architectural Discipline & Blast Radius Control**: Strict parent-child separation of concerns, single source of truth, elimination of redundant folders, and zero runaway subagent token burn.
4. **Persistent Self-Learning Skill Engine (`fashion-tech-skills`)**: An evolving repository of prompt contracts, ComfyUI graphs, and n8n workflows that encodes lessons using the **3 Ws Framework** (What, When, Why) so mistakes are never repeated.

---

## 2. Chronological Engineering Log & Technical Decisions

### Phase 1: Repository Cleanup & Single Source of Truth
- **Decision**: Restrict all active work exclusively to `/mnt/1.9TB/Dev/ayuti`. Wiped all temporary files, experimental branches, and outputs from `/mnt/1.9TB/Ayurti`, restoring the main disk to a clean baseline.
- **Parent-Child Hierarchy**:
  - `base/`: Canonical influencer master plates (`base_front.png`, `base_back.png`). Never duplicated inside product directories.
  - `docs/templates/`: Modular prompt schemas, camera angle JSONs, Veo 3.1 video directives, and catalog copy generators.
  - `products/product_01/`: Isolated child directory holding only product-specific references, mockups, poses, and copy.
  - `.gitignore`: Enforced strictly and exclusively at the repository root.

### Phase 2: Halting Runaway Loops & Execution Discipline
- **Issue**: Autonomous subagents triggered nested command loops (`git status`, directory re-checks), consuming excess tokens and recreating duplicate folder paths (`mockup/` vs `mockups/`).
- **Action**: Completely exited `@orchestrate` mode, aborted active background sessions via the OpenCode API, purged duplicate folders, and locked canonical asset paths to `products/product_01/mockup/`. All tasks now run in direct, single-turn execution mode.

### Phase 3: The 4-View Turnaround Sheet & 3D Geometry Rules
- **Generation**: Generated `garment_4view_sheet_1k.png` (1376x768) on an invisible ghost mannequin.
- **Defects Identified & Solved**:
  1. *Hardware Protrusions*: Eliminated dark grey mannequin neck stumps and posts.
  2. *Hollow / Jagged Seams*: Restored continuous, tailored shoulder seams and natural collar curves with interior lining cavity depth (`#3A3A3A-#5A5A5A`).
  3. *Duplicate Drape Hallucination*: Solved the 3D Asymmetric Single-Side Drape Rule. When a cowl shawl originates on the wearer's left shoulder, it wraps to the right hip only; the opposite 3/4 turn (View 2) must show clean, smooth, tailored kalis with zero duplicate drapes.
  4. *Rear Shoulder Continuity*: Fixed the 180° rotation so the shoulder wrap correctly sits on the viewer's left in the rear view, framing the scoop back neckline, dori tie string, and tiered gold latkan bell tassels.

### Phase 4: The Dual-View & 4-Quadrant Macro Detail Shift
- **Bottleneck**: Squeezing 4 full-body figures into 1376×768 left only ~344 horizontal pixels per gown, blurring fine zari pinstripes, micro-sequins, and hanging bead droplets.
- **Architectural Solution**: Decoupled full-body silhouette physics from micro-texture resolution by generating:
  1. **`garment_front_back_master.png`** (1200×896, 4:3 ratio): Side-by-side Front (0°) and Back (180°) full-body view locking height, length, single-side drape, and circular kalis flare.
  2. **`garment_front_quad_details.png`** (1024×1024, 1:1 ratio): 4-quadrant macro sheet capturing front neckline/shoulder anchor, tailored bodice/sleeve embroidery, waistband with scalloped bead fringe, and hem sweep.
  3. **`garment_back_quad_details.png`** (1024×1024, 1:1 ratio): 4-quadrant macro sheet capturing rear shoulder seam, rear sleeve tailoring, scoop back neckline with dori tie knot & tiered latkan bell tassels, and rear skirt kalis.

### Phase 5: 3-Piece Set Decomposition Analysis
- Visual analysis of raw vendor references (`dress_front_full.jpg`) confirmed the ensemble is an **Indo-Western 3-Piece Pre-Draped Gown Set**:
  - **Piece 1**: Floor-Length Anarkali Gown (fitted bodice, vertical sequin pinstripes, half sleeves, scoop back with latkans, 16-kali skirt).
  - **Piece 2**: Pre-Draped Cowl Dupatta / Pallu (pleated sash anchored at left shoulder, cascading crescent cowl folds with scalloped bead fringe).
  - **Piece 3**: Embroidered Waist Belt / *Kamarbandh* (stiffened waistband with matching sequin pinstripes locking the drape at the waist).
- **Execution Layout**:
  - `components/`: Pure isolated pieces (`piece_01_gown_front_back.png`, `piece_02_cowl_pallu_drape.png`, `piece_03_embroidered_belt.png`, `components_flatlay_sheet.png`).
  - `assembled/`: Full ensemble without splitting (`ensemble_front_full.png`, `ensemble_back_full.png`, `ensemble_front_back_master.png`).

---

## 3. The Enterprise Architecture: Webapp, n8n, 9Router & Self-Learning Skills

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        1. APPLICATION LAYER                            │
│   • Webapp UI (Frontend for product uploads, catalog gallery & review) │
│   • Telegram Bot Interface (Instant notifications, tap-to-approve)     │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
┌───────────────────────────────────▼────────────────────────────────────┐
│                       2. ORCHESTRATION LAYER                           │
│   • n8n Engine (Modular event-driven pipelines, webhooks, sub-flows)   │
│   • Agent as the Brain (Vision QA gates, error correction, prompts)    │
└──────────────────┬─────────────────────────────────┬───────────────────┘
                   │                                 │
┌──────────────────▼──────────────────┐   ┌──────────▼───────────────────┐
│        3. INTELLIGENCE & ROUTING    │   │      4. COMPUTE & EXECUTION  │
│   • 9Router UI & Gateway            │   │   • Headless ComfyUI Engine  │
│     - Unified API key management    │   │     - Custom Nodes & Graphs  │
│     - Intelligent provider fallback │   │     - ControlNet / IP-Adapter│
│     - Cost & quota tracking         │   │   • Vertex AI / Veo Video API│
│     - Latency & rate-limit guards   │   │   • FFmpeg Post-Processing   │
└──────────────────┬──────────────────┘   └──────────┬───────────────────┘
                   │                                 │
┌──────────────────▼─────────────────────────────────▼───────────────────┐
│                     5. REPOSITORY & KNOWLEDGE TRUTH                    │
│   • fashion-tech-skills (Single source of truth: schemas, rules)       │
│   • Persistent "3 Ws" Learning Ledger (Self-evolving memory)          │
│   • S3 / MinIO / Local Object Store (Immutable asset URIs)             │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 4. The Self-Learning "3 Ws" Framework

To prevent AI amnesia across sessions, every mistake, visual QA failure, or human correction triggers an automated entry into `fashion-tech-skills`:

1. **WHAT failed?**: Exact technical description of the artifact (e.g. duplicate cowl drapes on both hips, sliced sleeve cuff voids, hollow shoulder seams).
2. **WHEN does it trigger?**: The geometric or prompt conditions causing the hallucination (e.g. multi-angle turnarounds on asymmetric one-shoulder garments).
3. **WHY did it happen & how was it cured?**: The underlying model bias (diffusion bilateral symmetry bias) and the exact remediation added to the skill prompt and QA assertions.

Once committed, every downstream workflow, agent, and product run automatically inherits the hardened constraints.

---

## 5. Current Workspace Directory Structure

```text
/mnt/1.9TB/Dev/ayuti/ (Vishwa8/premium-fashion-ad-shoot)
├── .gitignore                          # Single root .gitignore
├── README.md                           # Project documentation
├── base/                               # Canonical influencer master plates
│   ├── base_front.png                  # 3072x5504 Clean Front Master
│   └── base_back.png                   # 3072x5504 Clean Back Master
├── docs/
│   ├── MASTER_DOCUMENTATION.md         # Comprehensive session & architecture documentation
│   ├── templates/                      # Reusable prompt & video templates
│   │   ├── garment_mockup/garment-sheet.txt
│   │   ├── virtual_tryon/
│   │   ├── pose_and_camera/
│   │   ├── video_generation/
│   │   └── catalog_description/
│   └── runs/                           # Historical run logs
└── products/product_01/
    ├── product.json                    # Master product specs (ASIN B0HM458PW4)
    ├── references/                     # 5 raw vendor product photos
    ├── description/                    # Luxury catalog copy & prompt descriptor
    ├── mockup/                         # Production mockup assets
    │   ├── garment_4view_sheet_1k.png          # 1376x768 4-view turnaround sheet
    │   ├── garment_front_back_master.png       # 1200x896 Front (0°) & Back (180°) split master
    │   ├── garment_front_quad_details.png      # 1024x1024 4-quadrant front macro sheet
    │   └── garment_back_quad_details.png       # 1024x1024 4-quadrant back macro sheet
    ├── poses/                          # Ready for 5 catalog poses
    └── videos/                         # Ready for Veo 3.1 video generation

/mnt/1.9TB/Dev/fashion-tech-skills/ (Vishwa8/fashion-tech-skills)
├── README.md
├── .gitignore
├── ARCHITECTURE.md                     # High-level triad & 3 Ws framework specification
└── skills/
    ├── 4-view-garment-sheet/SKILL.md           # Turnaround & single-side drape physics
    └── dual-view-and-quad-details/SKILL.md     # Decoupled macro detail & split view standard
```
