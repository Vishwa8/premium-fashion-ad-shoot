# Premium Fashion Ad Shoot: Production Plan (Strict Zero-Drift Pipeline)

## 1. What Are We Building?
An ultra-realistic, zero-drift fashion campaign and catalogue showcasing the Virtual Influencer wearing the **Kalibherva Embellished Maroon Anarkali Gown** (`Amazon ASIN: B0HM458PW4`) in her exact native high-end studio environment (`base/base_front.png` and `base/base_back.png`).

### Strict Quality Rules & Feedback Redressal
1. **Isolated Garment Pre-Pass**: Extract the gown and create an isolated 4-view dress turnaround (Front, 45°, 90°, Back) to lock embroidery, kalis, cowl drape, and dori tassels before compositing onto the base.
2. **Zero Environment Drift**: The room background, champagne silk folds, floor pooling, and 3200K studio key light must remain 100% identical across all shots. No phantom furniture.
3. **Zero Hair & Identity Drift**: The front and back hairstyles, hairline, skin tone, jawline, and temple jewelry must match `base/base_front.png` and `base/base_back.png` exactly.
4. **Crisp Dual-Scale Master**: The close-up portrait in `side_by_side_master.png` must be rendered in native high-resolution with crisp iris highlights, skin texture, and sharp zari threadwork (no pixelated crops).
5. **Model Standard**: All subagents run on `9router/vxoa/google/gemini-3.8-flash`.

---

## 2. Phased Pipeline Order
```text
┌────────────────────────────────────────────────────────────────────────┐
│ Step 1: Isolated 4-View Dress 3D Mockup                                │
│ - Extract dress from Amazon refs (B0HM458PW4)                          │
│ - Render Front, 45° Angle, 90° Profile, Back in isolation              │
│ - Lock embroidery, micro-sequins, cowl drape, and dori tassels         │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ Step 2: Base + Garment Try-On (Locked Front & Back Masters)            │
│ - Inpaint onto base/base_front.png and base/base_back.png              │
│ - Strict verification: Hair, face, room, lighting must match 100%      │
│ - Curate and lock mockup/front_master.png and mockup/back_master.png   │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ Step 3: High-Res Dual-Scale Master & 360 Contact Sheet                 │
│ - Render native high-res facial & neckline close-up (unpixelated)      │
│ - Assemble mockup/side_by_side_master.png & mockup/combine_views.png   │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ Step 4: 5 Zero-Drift Editorial Catalogue Poses                         │
│ - Conditioned strictly on locked Front & Back Masters                  │
│ - Poses 1 to 5 with 100% identical environment and garment             │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ Step 5: 5-Panel Storyboard Matrix & Video Production (Veo 3.1)         │
│ - Keyframed turnaround videos (full body & closeup)                    │
│ - Render 5 cinematic scene takes -> Stitch final 25s commercial cut   │
│ - Clean up unnecessary files, verify, and git push                     │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 3. Directory Layout
The repository follows a strict **Parent-Child architecture** with Single Source of Truth:
- `base/`: Universal master influencer clean plates (`base_front.png`, `base_back.png`).
- `docs/`: Technical specifications, production plans, run records, and modular reusable templates (`docs/templates/`).
- `products/product_01/`: Self-contained child package for Kalibherva Maroon Anarkali Gown (`B0HM458PW4`) with modular chunks:
  - `product.json`: Single source of truth for product specifications.
  - `references/`: Raw Amazon reference photography.
  - `mockups/`: Isolated 4-view 3D turnarounds, locked front/back masters, macro portrait, dual-scale sheet, contact sheet.
  - `poses/`: 5 curated editorial catalogue poses.
  - `videos/`: 360 turnarounds & final 25s commercial cut.
  - `copy/`: Luxury catalog copy and prompt descriptors.
- `.gitignore`: Exclusively at workspace root.

---

## 4. Cost Discipline & Rate Strategy
- **Low-Cost Prototyping (Fast Tier)**:
  - Gemini Flash / fast inpainting for composition and pose validation at 1K resolution.
  - `veo-3.1-fast-generate-001` for motion dynamics and camera trajectory testing.
- **Production Render (Pro / Quality Tier)**:
  - Pro models and high-resolution upscaling (4K) only on approved candidate keyframes.
  - `veo-3.1-generate-001` in 1080p/4K for the final commercial reel.
- **Auditing**: All costs logged continuously to `generations/cost_tracker.csv`.
