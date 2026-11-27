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

### Phase 6: ComfyUI Docker Containerization & Auto-Restart Window Reloader (3 Ws Framework)

#### 1. When (Trigger Condition)
When running ComfyUI on Ubuntu Linux host with Windows-packaged node dependencies, and when users click "Restart" in ComfyUI-Manager (`/manager/reboot`) or ComfyUI top menu, causing backend process replacement while leaving the browser stuck in an unresponsive "Reconnecting" banner without reloading.

#### 2. What (Technical Implementation)
- **Containerization**: Spun up a lightweight Docker container (`comfyui-local:latest`) based on `python:3.12-slim` + PyTorch CPU + OpenCV + Google GenAI dependencies. Configured via `/mnt/1.9TB/comfy/docker-compose.yml` with port `8188:8188` mounting custom nodes, models, input/output, and the workspace.
- **Universal Auto-Restart & Reloader Shield (`custom_nodes/vishwa/web/auto_restart_reloader.js`)**:
  - **Full App Disabling**: Instantly sets `pointer-events: none !important; opacity: 0.22; filter: blur(4px) grayscale(60%)` on the entire underlying UI, locking canvas clicks, menu interactions, and keyboard shortcuts.
  - **Animated Loading Shield**: Renders a high-z-index (`z-index: 2147483647`) backdrop overlay with glowing gradient circular spinner, dynamic pulsing status pill, and real-time seconds elapsed counter.
  - **Health Polling**: Continuously polls `GET /system_stats` in the background with timeout abort controllers.
  - **Auto-Reload**: The exact millisecond the backend responds with `HTTP 200 OK`, updates the badge to "Server Online!" and automatically executes `window.location.reload()`.
  - **Dual-Hooks**: Intercepts WebSocket `close` events, fetch requests to `/manager/reboot`, and DOM clicks on all restart/reboot buttons across the interface.

#### 3. Why (Root Cause & Value)
Default ComfyUI web UI relies on manual user F5 refreshes after process restart. In high-tempo fashion workflows, users frequently get stranded on the red "Reconnecting" modal without knowing if the restart succeeded or failed. The shield completely eliminates manual guesswork, protects user workflows from half-booted state errors, and provides seamless zero-touch page reloading.

---

## 2. The Core Philosophy: The Zero-Drift E-Commerce Law & The Atomic "Lego-Brick" Inpainting Architecture

### 2.1 The Non-Negotiable Zero-Drift Law & Commercial Impact
In luxury couture and e-commerce advertising, **consistency is the bedrock of commercial trust**.
- **The Catastrophic Cost of Drift**: If the model's facial features shift, skin tone oscillates, hair parting untangles, studio backdrop changes color or pleat density, or accessories morph between angles and products:
  1. **Customer Trust Collapses**: Shoppers immediately detect synthetic inconsistency, perceive the catalog as untrustworthy or fraudulent, and abandon carts.
  2. **Surging Return Rates**: Misrepresented fabric textures, incorrect drape physics, or hallucinated necklines lead directly to high return rates and customer dissatisfaction.
  3. **Brand Devaluation**: Luxury brands cannot tolerate "almost identical." Every asset must meet 100% editorial parity.

---

### 2.2 The Canonical Single Source of Truth (SSOT): Clean Base Plates
To achieve absolute consistency across hundreds of catalog SKUs, **every single product must be built on the exact same canonical base plates**:
- **Front Master**: `base/base_front.png` (Front 0° full-body view).
- **Back Master**: `base/base_back.png` (Back 180° full-body turnaround view).

#### The Clean Base Plate Standard:
1. **Try-On Friendly Neutral Garment**: The model wears a form-fitting, minimalist, neutral cream/beige slip dress. There are no ruffles, heavy folds, or preexisting embroidery to fight incoming garments.
2. **ZERO Preexisting Accessories**:
   - **Naked Neckline**: No necklaces, chokers, or chains (clean collarbone canvas).
   - **Naked Ears**: No earrings, studs, or jhumkas (clean earlobes).
   - **Naked Wrists & Hands**: No bangles, bracelets, or rings (clean hands with 5 anatomically perfect fingers).
   - **Naked Waist**: No preexisting belts, latkans, or sashes.
3. **Locked Facial & Hair Anatomy**:
   - Canonical Indian influencer facial geometry, natural warm undertone with micro-pores, neutral regal expression.
   - Right-side crisp parting leading into a textured, sleek low bun (zero loose tendrils that could blur during masking).
4. **Locked Environmental Scene**:
   - Champagne pleated satin/silk draped studio backdrop with vertical floor sweeps.
   - Neutral, diffused 3-point softbox commercial studio lighting.

---

### 2.3 The Fully Decoupled, Interchangeable "Lego-Brick" Matrix (Editorial & UGC)

The virtual fashion system operates as a **non-destructive, multi-layered compositing matrix**. Every single layer is **fully decoupled, independently editable, and interchangeable** using surgical inpainting, outpainting, relighting, and multi-model fusion—without altering or damaging any other layer.

```text
┌──────────────────────────────────────────────────────────────────────────────┐
│                    THE DECOUPLED LEGO-BRICK LAYER MATRIX                    │
├──────────────────────────────────────────────────────────────────────────────┤
│  LAYER 7: Global Environmental Harmonization (Contact shadows, reflections)   │
│     ▲                                                                        │
│  LAYER 6: Accessories & Accents (Handbag/Potli, Shoes/Mojris, Watch, Rings)  │
│     ▲                                                                        │
│  LAYER 5: Fine Jewelry (Maang Tikka, Jhumkas, Kundan Choker - bare skin lock)│
│     ▲                                                                        │
│  LAYER 4: Atomic Garment Bricks (Editable Color, Zari Pattern, Silhouette)   │
│     │     • Brick 4C: Embroidered Waist Belt / Kamarbandh / Cinch Band       │
│     │     • Brick 4B: Asymmetric Cowl Pallu / Dupatta / Trailing Cape        │
│     │     • Brick 4A: Base Gown / Bodice & Kali Skirt (Front & Back)         │
│     ▲                                                                        │
│  LAYER 3: Subject Styling & Beauty (Eye lenses, Hair dye/style, Makeup)      │
│     ▲                                                                        │
│  LAYER 2: Canonical Subject Canvas (Bare-minimum slip, universal neck/legs)  │
│     ▲                                                                        │
│  LAYER 1: Scene & Environmental Context (100% Interchangeable Background)     │
│     │     • Editorial Studio Shoot (Champagne silk, marble arches, softbox)  │
│     │     • UGC Lifestyle (Sunlit room, aesthetic cafe, festive living room) │
│     │     • Dynamic Lighting & Palette tailored to dress craftsmanship       │
│     ▲                                                                        │
│  LAYER 0: Spatial Framing & Camera Canvas (9:16 / 4:5 / 1:1, Focal Length)   │
└──────────────────────────────────────────────────────────────────────────────┘
```

---

### 2.4 Deep Dive: Layer-by-Layer Separation & Independent Editing

#### Layer 0: Spatial Framing & Camera Canvas
- **Role**: Establishes fixed optical coordinates, aspect ratio (`9:16` vertical video/reels, `4:5` Instagram feed, `1:1` e-commerce square), camera angle, and focal length (85mm portrait compression or 50mm natural perspective).
- **Invariance**: Guarantees consistent model height, horizon line, and floor distance across all catalog angles (Front 0°, 3/4 Turn 45°, Lateral Profile 90°, Back 180°).

#### Layer 1: Scene & Environmental Context (100% Interchangeable via Inpaint/Outpaint/Relight)
- **Role**: Provides the atmosphere, architectural objects, furniture props, and lighting physics tailored specifically to showcase the unique craftsmanship, embroidery, and color palette of the garment.
- **Interchangeable Modes**:
  1. **High-Fashion Editorial Shoot**: Champagne draped satin/silk backdrops, Roman plaster pedestals, minimalist architectural arches, sculptural floral installations, high-key commercial 3-point softbox studio lighting.
  2. **Authentic UGC (User-Generated Content)**: Warm sunlit aesthetic bedroom, vanity mirror corner, cozy balcony terrace, festive Diwali/wedding living room with authentic ambient bokeh, or casual urban street-style daylight.
- **Dynamic Lighting & Color Palette Modulation**:
  - The scene lighting is dynamically tuned to complement the dress (e.g., golden hour 3200K rim light to accentuate deep maroon and warm zari; crisp 5600K diffused studio light for pastel georgettes).
- **Independent Modification**:
  - The background can be completely replaced, expanded (outpainted), or relit (using IC-Light / ControlNet) **without touching a single pixel of the subject, makeup, dress, or jewelry**.

#### Layer 2: The Canonical Subject Plate (Bare-Minimum Universal Canvas)
- **Role**: Establishes the locked human anatomical foundation (facial bone structure, eye gaze, neutral regal expression, warm olive skin tone, anatomical 5-finger hands).
- **The "Universal Canvas" Undergarment**:
  - The model is dressed in a **bare-minimum, seamless, skin-tone neutral slip or strapless bodysuit**.
  - **Why Bare Minimum?**: Allows the subject to wear **any cut or silhouette of garment imaginable** without clashing underlying fabric boundaries:
    - Deep plunge necklines, high boat necks, or mandarin collars.
    - Strapless corsets, spaghetti straps, or cape sleeves.
    - Completely backless scoop cuts or low latkan tie-backs.
    - Thigh-high side slits, mini dresses, or floor-pooling 16-kali skirts.

#### Layer 3: Subject Styling & Beauty (Independent Cosmetic/Grooming Layer)
- **Role**: Allows granular beauty adjustments tailored to the mood of the campaign without altering underlying facial geometry:
  - **Eye Lenses**: Swap iris tone (deep natural obsidian, honey hazel, soft amber, smoky grey) to match garment aesthetics.
  - **Hair Dye & Micro-Styling**: Deep raven black, espresso brunette, or auburn balayage; crisp right-side part, textured low bun, or flowing loose waves.
  - **Makeup Palette**: Winged eyeliner, smoky kohl kajal, champagne gold eyeshadow micro-glitter, lip shade (deep plum, brick red, nude peach), matte vs dewy glass-skin finish.
- **Independent Modification**: Inpainted strictly within dedicated facial feature masks (eyes, lips, hair) leaving dress and background 100% untouched.

#### Layer 4: Atomic Garment Bricks (The Couture Construction Suite)
- **Role**: The core garment decomposed into modular, stackable, editable components:
  - **Brick 4A (Base Garment)**: Bodice, sleeves, kali skirt, and back cutout.
  - **Brick 4B (Draping Layer)**: Asymmetric pre-draped cowl pallu, pleated dupatta, or cascading cape.
  - **Brick 4C (Structural Cinch)**: Embroidered waist belt (*kamarbandh*), corset boning, or waistband tassels.
- **Independent In-Place Editing**:
  - **Colorway Swapping**: Recolor the maroon georgette to royal emerald or sapphire blue in seconds via masked inpainting.
  - **Pattern & Zari Modification**: Swap vertical micro-sequin pinstripes to floral botanical embroidery (*buttis*) without re-generating the underlying drape physics.
  - **Piece Swapping**: Change the drape from a cowl swag to a traditional pleated over-the-shoulder dupatta while retaining the base Anarkali gown completely intact!

#### Layer 5: Fine Jewelry (Independent Adornments)
- **Role**: Precious jewelry applied strictly onto virgin skin areas without competing with garment fabrics:
  - **Brick 5A (Neckpiece)**: Polki choker, emerald collar, temple gold rani haar, or bare neck.
  - **Brick 5B (Earrings)**: Antique gold jhumkas, chandelier drops, pearl studs, or bare ears.
  - **Brick 5C (Hair/Head Jewelry)**: Maang tikka, matha patti, passas, or decorative hair pins.

#### Layer 6: Accessories & Accents (Complete Fashion Styling)
- **Role**: Editorial props and finishing fashion accessories:
  - **Brick 6A (Handwear & Timepieces)**: Gold kadas, glass bangles, luxury chronograph watch, cocktail rings.
  - **Brick 6B (Handbags & Handhelds)**: Embellished bridal potli, structured minaudière clutch, leather tote.
  - **Brick 6C (Footwear)**: Zari embroidered mojris, nude block-heel sandals, metallic stilettos.

#### Layer 7: Global Environmental Harmonization & Physics Integration
- **Role**: The final fusion layer ensuring physical cohesion across all assembled layers:
  - Cast contact shadows under footwear and skirt hem onto the floor.
  - Realistic ambient occlusion in fabric folds and necklines.
  - Dynamic bounce light (radiosity) reflecting dress color onto nearby surfaces and skin.
  - Natural optical depth of field (DoF) separating subject from background.

---

### 2.5 Multi-Model Technology Stack: Inpaint, Outpaint, Relight & Vision QA

```text
┌─────────────────────────────────┬───────────────────────────────────────────┐
│ Function                        │ Primary Technology Engine                 │
├─────────────────────────────────┼───────────────────────────────────────────┤
│ Pixel-Locked Layer Inpainting   │ FLUX.1 Fill [dev] (ComfyUI)               │
│ Scene Outpainting & UGC Expand  │ FLUX.1 Fill + SDXL Outpaint               │
│ Environment Relighting          │ IC-Light (Consistent lighting transfer)   │
│ Semantic Mask Extraction        │ Segment Anything 2 (SAM 2) + RMBG         │
│ Ghost Mannequin & Macro Details │ Gemini / Nano Banana (High-res textures)  │
│ Editorial Copy & Descriptions   │ Gemini 2.5 Flash / Qwen 2.5 72B           │
│ Vision QA & Drift Verification  │ Automated Gemini Vision Inspection Gate   │
└─────────────────────────────────┴───────────────────────────────────────────┘
```

1. **Why FLUX.1 Fill for Surgical Inpainting**:
   - Operates strictly within explicit binary masks.
   - Preserves 100% of unmasked pixels bit-for-bit, guaranteeing **mathematical 0.0000% drift** across identity, scene, and adjacent accessories.
2. **Why Outpainting & Relighting for UGC / Editorial Switching**:
   - Outpainting models expand the environment outward to create wide-angle lifestyle context (e.g. converting a studio crop into a full sunlit room or palace terrace).
   - Relighting models (such as IC-Light) modulate the ambient lighting temperature and shadow direction across the model and dress so they naturally match the new environment.
3. **Why Gemini / Nano Banana for Macro Assets & Vision QA**:
   - Multimodal Gemini is utilized where it excels: generating high-resolution ghost mannequin turnarounds, 4-quadrant micro-texture reference sheets (sequin reflections, sheer georgette weave), and acting as an autonomous Vision QA gate to measure zero-drift compliance.

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
