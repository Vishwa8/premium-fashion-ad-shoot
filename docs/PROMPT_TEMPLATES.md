# Ayurti Prompt Templates & Generation Specification Library

## Overview
This library aggregates, standardizes, and documents the proven prompt engineering systems developed and refined across the Ayurti production pipeline (extracted and unified from `/mnt/1.9TB/Ayurti/Docs/`). It establishes hard constraints, structural locks, camera presets, and cinematography parameters for commercial fashion catalog production.

---

## 1. Isolated 4-View Garment Turnaround Engine (`garment-sheet.txt`)

### Purpose
To extract garments from lifestyle photography or flat references and generate an isolated, professional 4-view turnaround reference sheet (**Front View, Left Profile, Right Profile, Back View**) on an invisible ghost mannequin against a pure white (`#FFFFFF`) background.

### Mandatory Structural & Geometry Locks
Every 4-view generation prompt MUST incorporate the following explicit safety clauses:

```text
STRUCTURAL LOCK: The garment construction, seam placement, closure placement, neckline geometry, sleeve volume, waist position, hem width, tier placement, panel divisions, and silhouette proportions must match the reference image exactly. The AI is strictly forbidden from adding, removing, or relocating seams, zippers, ties, panels, darts, gathers, pleats, closures, or structural elements.

GEOMETRY LOCK: Maintain identical proportional ratios between neckline width, shoulder width, waist position, sleeve volume, and hem width as observed in the reference image. No proportional reinterpretation allowed.
```

### Ghost Mannequin Anti-Bleed Protocol
For cutouts, neck cavities, armholes, or front/back slits:
- Interior openings and cavities MUST be rendered in **deep charcoal-grey tones (`#3A3A3A` - `#5A5A5A`)** with graduated shadows.
- **NEVER** allow the pure white `#FFFFFF` background to bleed through internal openings, which flattens the garment and ruins 3D spatial coherence.

### Global Prohibitions
- No adding or removing zippers, buttons, or ties.
- No sleeve inflation/deflation.
- No waist height shifting.
- No prompt phrases like "remove the model" or "exact as seen in image".
- No airbrushed, cartoon, or synthetic plastic CGI finishes. Must exhibit crisp textile fibers and natural weave.

---

## 2. Virtual Try-On & Identity Preservation System

### Multi-Reference Hierarchy
When compositing a garment onto our Virtual Influencer, reference priority is strictly ordered:
1. **Face & Identity Source of Truth**: `base/base_front.png` (warm golden-olive skin, dark brown wavy hair, subtle dimple).
2. **Body & Pose Source of Truth**: `base/base_front.png` / `base/base_back.png`.
3. **Garment Structure & Silhouette**: `products/<product_id>/mockup/dress_3d_front.png`.
4. **Garment Embroidery & Texture**: High-resolution detail vendor references (`dress_detail_*.jpg`).
5. **Scene & Lighting Source of Truth**: Luminous champagne satin backdrop, 3200K warm key light.

### Try-On Core Directive
```text
Use the base image as the identity, pose, body, lighting, and scene source of truth. Replace only the masked dress with the uploaded dress reference keeping everything else the same.

Preserve the exact same woman, face, skin tone, hair, expression, jewelry, hands, pose, body proportions, camera angle, full-body framing, cream satin draped background, floor drape, and sandals.

Transfer the garment faithfully: [INSERT PRECISE GARMENT DETAIL STRING]

Do not change identity, hairstyle, background, lighting, composition, or accessories. Photorealistic fashion catalog image.
```

### JSON Schema Integration (`tryon_schema_v2.json` / `model_transfer_v1.2.json`)
Allows programmatic API invocation specifying:
- `references`: Explicit mappings for closeup, full-body, garment, and scene.
- `subject.identity_lock`: 100% face and skin tone lock.
- `wardrobe.design_details`: Construction parameters, seam locations, fabric physics.
- `scene_and_lighting`: Color temperature, key/fill ratios, backdrop material folds.

---

## 3. Pose Transfer & Camera Angle Dropdown Library

### Pose Transfer Prompt Pattern
Used to generate new catalog poses without altering identity, dress, or studio background:
```text
Use base image 1 & image 2 as the identity, body, dress, lighting, and scene source of truth. Replace only the model's pose & expression with the uploaded pose reference (image 3) keeping everything else the same.

Preserve the exact same woman, face, skin tone, hair, jewelry, hands, body proportions, cream satin draped background, floor drape, and sandals.

Transfer the pose (with natural body curves like C-curve or S-curve), camera angle, framing & expression faithfully as in image 3 exactly.

Do not change identity, hairstyle, garment, background, lighting, composition, or accessories. Photorealistic fashion catalog image.
```

### Curated Camera Angle Presets (`camera-angles-dropdown-back.json`)
50+ granular presets for precise camera alignment:
- `Eye-level straight-on back shot (centered, symmetrical composition)`
- `Eye-level slight right offset (camera shifted right, back still fully visible)`
- `Shoulder-level framing (focus on upper back and neckline details)`
- `Waist-level slight upward angle (emphasizes fall and structure of dress)`
- `Eye-level shallow depth (sharp dress, soft background)`
- `Moderate low angle back (emphasizes height and flow)`

### Standard Catalog Pose Presets (`poses-dropdown.json` & `poses-dropdown-back.json`)
Extensive dropdowns defining realistic commercial poses:
- **Front & 3/4**: Relaxed standing with one hand on hip; hands holding dress sides to highlight skirt flare; 3/4 twist pose with weight shifted; walking pose paused mid-step.
- **Rear**: Straight back-facing with arms relaxed; 3/4 back with hand gently touching hair; back-facing with hands folded low; back-view holding dress edges to display rear kalis.

---

## 4. Cinematography & Video Generation (Veo 3.1)

### Cinematic System Prompt (`video-template-mockup.txt`)
Directs the diffusion video model as a world-renowned digital cinematographer specializing in 8K photorealistic product showcases:
- **Style Combination**: Layered mastery (1.4), hyper-detailed fabric textures (1.2), subtle material sheen (1.3), warm cinematic lighting (1.2).
- **Temporal Coherence**: 24/60fps blended slow-motion pacing, zero jitter, zero character or garment drifting.
- **Strict Negative Directives**:
  ```text
  extra legs, occlusion, extra fingers, identity drift, face morphing, flickering, jittering, hand position sliding, dress pattern crawling, lighting shifts, jerky neck movement, unnatural fabric stretching, fan visible in frame, blurry, low quality, deformed, cartoon, plastic skin, fabric clipping
  ```

### Motion Safety Rules
Crucial constraints embedded in all video generation JSON configs:
1. **Front-Facing Rules (`video_front_config.json`)**:
   - `body_orientation`: Keep model fully front-facing or slight 3/4 only. Never rotate enough to reveal side profile or back details.
   - `turn_limit`: No spins, no half-turns, no side reveals.
   - `face_lock`: Strict face identity lock; zero morphing.
   - `garment_lock`: No reinterpreting or introducing unseen dress details.
   - `motion_style`: Slow-motion elegance (subtle breathing, posture settling, micro-hand adjustments).
2. **Back-Facing Rules (`video_back_config.json`)**:
   - `body_orientation`: Model remains strictly back-facing (rotation <= 5 degrees). Side profile and jawline remain 100% hidden.
   - `turn_limit`: Strictly no turns, no spins, no side reveals.
   - `identity_lock`: Consistent wavy hair drape and shoulder width.
   - `garment_lock`: Exact rear seams, dori ties, and tassels locked.
3. **Fabric Dynamics (Wind-Blown Motion)**:
   - The champagne satin background fabric is permitted subtle, luxurious wind-blown ripple to infuse life into the scene without compromising garment geometry.

---

## 5. Luxury Brand Catalog Copywriter Engine (`description-template.md`)

Transforms visual assets (4-view sheet + lifestyle shot) into high-end luxury ecommerce copy:
1. **Product Title**: Regal, evocative, commercially SEO-optimized.
2. **Luxury Intro Paragraph**: Editorial prose (80–140 words) capturing mood, color, and silhouette.
3. **Design Philosophy**: Traditional craftsmanship meets contemporary couture tailoring.
4. **Fabric Story**: Yarn characteristics, tactile drape, light reflectance, lining comfort.
5. **Silhouette & Technical Details**: Neckline, sleeves, bodice darts, kali counts, slit heights, closures, hem sweep.
6. **Key Features**: 5–8 crisp technical bullet points.
7. **Occasions**: Verified styling occasions (weddings, galas, Diwali, receptions).
8. **Short Ecommerce Summary**: 1-sentence high-impact summary.
