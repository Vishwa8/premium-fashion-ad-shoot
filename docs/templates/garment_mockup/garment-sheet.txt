---
name: 4-view-garment-sheet
description: Generates physically consistent, zero-defect 4-view garment reference sheets (Front 0°, 3/4 Turn 45°, Lateral Profile 90°, Back 180°) on an invisible ghost mannequin for virtual try-on, turnaround modeling, and video conditioning. Enforces strict single-side drape geometry, natural finished necklines/shoulders, and anti-bleed protocols.
---

# 4-View Garment Reference Sheet Specification

## Purpose
This skill creates production-grade, 4-view garment turnaround reference sheets in a single horizontal layout on a pure white `#FFFFFF` studio background. It enforces continuous 3D rotational perspective and realistic garment physics across all views, eliminating common AI flaws (duplicate drapes, disconnected shoulder anchors, hollow cutouts, and blurry rear embellishments).

---

## The 4 Canonical Turnaround Views (Single Horizontal Row)

```text
+-------------------+-------------------+-------------------+-------------------+
|  View 1: Front 0° |  View 2: Turn 45° | View 3: Profile 90| View 4: Back 180° |
+-------------------+-------------------+-------------------+-------------------+
```

### 1. View 1: Front View (0°)
- Full-body standing perspective on pure `#FFFFFF` background.
- Shows curved square front neckline and tailored fitted bodice.
- **Asymmetric Cowl/Shawl**: Originated at **wearer's left shoulder** (viewer's right), crosses diagonally across the chest/under waistband, and pools into fluid crescent cowl swags over the **wearer's right hip** (viewer's left).
- Lower border of cowl drape is trimmed with delicate scalloped antique gold threadwork and dangling micro-bead droplets.

### 2. View 2: Three-Quarter Turn View (45°)
- Rotated 45 degrees towards the viewer.
- **Continuous Drape Consistency**: Shows the chest crossover originating from the wearer's left shoulder in perspective, leading into the front waist.
- Fitted bodice with vertical antique gold zari and micro-sequin pinstripes.
- Circular kalis flare cascading downward.

### 3. View 3: Lateral Profile View (90°)
- Pure 90-degree lateral profile showing the draped hip side.
- Highlights the 3D depth, layered swags, and crescent folds of the cowl drape cascading down the side of the gown.
- Sleeves are cleanly finished with tailored cuffs (no hollow black voids).

### 4. View 4: Back View (180°)
- Full rear view (180° rotation from View 1).
- **Physical Shoulder Continuity**: Because the shawl is on the wearer's left shoulder, in the rear view it rests on the **viewer's left shoulder** and drapes naturally along that side.
- **Back Bodice**: Deep scoop/square back neckline, framed with crisp vertical sequin pinstripes matching the front resolution.
- **Back Closures**: Horizontal tie cord fastened across upper back with handcrafted tiered antique gold latkan bell tassels cascading down the center back.
- **Single-Side Skirt**: The opposite side of the skirt is smooth and flared with zero phantom duplicate drapes.

---

## Non-Negotiable Quality & Physics Rules

### 1. 3D Asymmetry & Single-Side Drape Lock
- When a garment features an attached cowl, shawl, or pallu, it belongs to **ONE SINGLE SHOULDER and ONE HIP ONLY**.
- **Forbidden**: Placing crescent cowl drapes on both left and right hips simultaneously (View 2 and View 3 must never both show heavy draped swags). One side is draped; the opposite side is smooth and tailored.
- **Forbidden**: Inverting or dropping the shoulder anchor in the rear view.

### 2. Sleeve, Cuff & Collar Integrity
- **No Cutout Voids**: Sleeve cuffs and arm openings must be rendered with realistic tailored fabric edges and subtle inner lining shadow—NEVER with flat black void cutouts or sliced holes.
- **No Hardware Protrusions**: Zero mannequin neck stumps, wooden pegs, chrome stands, or cylinder posts protruding above or inside the collar.
- **Continuous Shoulder Seams**: Shoulder seams, collar curves, and strap edges must be continuous, fully sewn, intact fabric without jagged white cutouts.
- **Interior Cavity**: The hollow interior opening is shaded with soft, deep charcoal-grey tones (`#3A3A3A-#5A5A5A`) defining structural 3D volume, with pure `#FFFFFF` background around the exterior.

### 3. Embellishment Resolution Consistency
- Gold zari pinstripes, sequins, and scalloped bead trims must maintain identical sharpness and resolution across all 4 views (rear view must not be blurrier than front view).

---

## Master Prompt Template

```text
A professional garment reference sheet isolated on pure white #FFFFFF background in a single horizontal row showing four full-body standing views: Front View (0°), Three-Quarter View (45°), Lateral Profile View (90°), and Back View (180°) on an invisible ghost mannequin.

STRUCTURAL LOCK:
The garment construction, seam placement, closure placement, neckline geometry, sleeve volume, waist position, hem width, tier placement, panel divisions, and silhouette proportions must match the reference image exactly.

3D ROTATIONAL PERSPECTIVE & SINGLE-SIDE DRAPE CONTINUITY:
The garment features a single asymmetric pleated cowl dupatta/shawl anchored at the wearer's left shoulder:
- View 1 (Front 0°): Shoulder anchor on wearer's left (viewer's right), crossing diagonally across torso into layered crescent cowl swags with scalloped gold trim and hanging micro-bead droplets over the wearer's right hip (viewer's left).
- View 2 (3/4 Turn 45°): Rotated 45 degrees, showing the chest crossover and shoulder drape in continuous perspective with fitted bodice and vertical sequin stripes.
- View 3 (Profile 90°): Profile view of the draped hip displaying the dimensional depth of the cowl swags. Sleeves feature clean tailored cuffs with natural interior depth.
- View 4 (Back 180°): 180-degree rear view showing the shoulder drape resting on the wearer's left shoulder (viewer's left) and flowing cleanly down. Deep scoop back neckline with crisp vertical sequin pinstripes matching front sharpness, with dual dori tie strings and tiered antique gold latkan bell tassels centered at the back. The opposite side of the skirt is clean, smooth, and flared without duplicate cowl folds.
The AI is strictly forbidden from duplicating the cowl drape on both hips or inverting shoulder anchors.

COLLAR, SLEEVE & GHOST MANNEQUIN INTEGRITY:
True invisible ghost mannequin. Shoulder seams, neckline edges, and sleeve cuffs must be solid, continuous, smoothly tailored fabric with NO jagged cutouts, black void holes, or missing cloth. There is absolutely NO visible mannequin neck cylinder, stand, post, or peg protruding above or inside the neckline opening. Interior cavities are rendered with deep charcoal-grey tones (#3A3A3A-#5A5A5A) to define 3D volume against the pure white #FFFFFF background.

GARMENT SPECIFICATIONS:
- Base: Deep imperial wine maroon (#4A0E17) premium heavy faux georgette.
- Bodice: Curved square front neckline, tailored elbow-length half sleeves, vertical antique gold zari and micro-sequin pinstripes. Matching 1.5-inch embellished waistband.
- Skirt: Voluminous 16-kali flared circular skirt pooling naturally at floor level with grounding contact shadows.

Single horizontal row, 1376x768 (Landscape 1K), photorealistic DSLR fashion studio catalog quality, diffuse lighting, grounding floor contact shadows.
```
