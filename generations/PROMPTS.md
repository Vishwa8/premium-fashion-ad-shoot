# Premium Fashion Ad Shoot: Production Prompts & Directorial Blueprint

This document specifies the exact prompt engineering standards, negative prompts, camera setups, and lighting rules for the Premium Fashion Ad Shoot production campaign.

---

## 1. Core Subject & Garment Anchors

### Influencer Identity Anchor
- **Face & Body**: Exact facial structure, eye shape, lip contour, dusky South Asian skin tone, and hair texture locked to `base/base_front.png` and `base/base_back.png`.
- **Environment**: Original upscale indoor studio / architectural room setting from `base/base_front.png`, retaining the natural depth of field, champagne silk drapery, and warm 3200K key lighting.

### Garment Specifications (Kalibherva Maroon Anarkali Gown)
- **Silhouette**: Floor-length regal Anarkali gown with voluminous circular kalis (flared panels).
- **Fabric**: Deep rich wine / royal maroon raw silk and velvet blend with delicate weight and natural drape folds.
- **Embellishment**: Fine antique gold zari thread embroidery along the round neckline, fitted bodice, and wide scalloped hem border; scattered micro-sequins catching warm ambient light.
- **Dupatta**: Cascading matching maroon dupatta draped gracefully over one shoulder and across the torso, featuring rich golden embroidered border.
- **Jewellery**: Heritage South Asian antique temple gold collection: layered choker/necklace, ornate jhumkas (drop earrings), delicate maang tikka, intricately carved gold bangles, and a subtle slim waist chain.

---

## 2. Master Image Prompts (Mockup & Poses)

### Master Front View (`mockup/front_master.png`)
```text
High-fashion editorial catalog portrait of the South Asian woman from base/base_front.png standing elegantly in the original room environment. She is wearing the luxurious Kalibherva royal maroon Anarkali gown with voluminous flared floor-length panels and an attached matching dupatta draped gracefully over her left shoulder. The gown features intricate antique gold zari embroidery along the fitted bodice, neckline, and hem border, with subtle glistening micro-sequins. Styled with traditional South Asian antique temple gold jewellery including ornate jhumka earrings, a delicate layered gold necklace, and carved bangles. The original room environment, warm ambient interior lighting, skin texture, and exact facial features are preserved identically without drift. 8k resolution, photorealistic, Hasselblad 80mm f/2.8 lens portrait.
```

### Master Back View (`mockup/back_master.png`)
```text
Rear fashion catalog view of the South Asian woman from base/base_back.png in the exact same room environment. Wearing the back of the royal maroon Kalibherva Anarkali gown, showcasing the elegant back neckline with delicate golden dori tassels, fitted rear bodice embroidery, and wide circular flared hem cascading onto the floor. Draped dupatta falls softly down the back with intricate gold scalloped borders. Matching ornate gold jhumkas visible against her neatly styled traditional braid/hairdo. Consistent lighting and room architecture, zero character drift, 8k resolution, editorial fashion photography.
```

### Dual-Scale Side-by-Side Master (`mockup/side_by_side_master.png`)
```text
A unified high-resolution editorial contact sheet with two side-by-side frames of the same woman in the identical maroon Kalibherva Anarkali gown. 
Left frame: Full-length vertical shot displaying the full silhouette, expansive flared floor-length gown hem, attached draped dupatta, and the full architectural studio environment. 
Right frame: Close-up upper-body portrait focusing on her face, sharp eye contact, micro skin texture, ornate temple gold jhumkas, and the intricate gold zari embroidery of the neckline. 
Both frames have matching warm cinematic lighting, exact character identity, and zero chromatic drift. Professional fashion catalog composite, 8k quality.
```

---

## 3. The 5 Curated Editorial Catalogue Poses (`poses/`)

1. **Pose 1 - The Dynamic Twirl (`poses/pose_01_twirl_apex.png`)**:
   - *Prompt Anchor*: "Dynamic freeze-frame capturing a graceful slow twirl, full circular Anarkali flare billowing outwards with natural fabric weight and fluid motion, dupatta floating slightly in the air, joyous yet regal facial expression, sharp focus on face and jewelry, room architecture motion blur in background, 8k resolution."
2. **Pose 2 - The Royal Symmetrical Stand (`poses/pose_02_regal_standing.png`)**:
   - *Prompt Anchor*: "Stately upright catalog pose, symmetrical front posture, hands gently resting at the waist showing carved antique gold bangles, full gown drape cascading cleanly to the floor, serene direct gaze into camera, high-end ethnic luxury campaign framing."
3. **Pose 3 - The Dupatta Drape & Jewelry Accent (`poses/pose_03_dupatta_accent.png`)**:
   - *Prompt Anchor*: "Mid-shot editorial angle, one hand delicately holding the scalloped golden border of the maroon dupatta near the collarbone, highlighting the gold rings and bangles, soft warm key light illuminating the jhumkas and neckline embroidery."
4. **Pose 4 - The Editorial 3/4 Silhouette (`poses/pose_04_profile_glance.png`)**:
   - *Prompt Anchor*: "Three-quarter angle portrait, body turned 45 degrees, head gracefully tilted back towards the camera with a subtle contemplative expression, showing the three-dimensional structure of the Anarkali kalis and the drape along the shoulder."
5. **Pose 5 - The Over-the-Shoulder Turn (`poses/pose_05_cinematic_turn.png`)**:
   - *Prompt Anchor*: "Cinematic over-the-shoulder turn, woman turned three-quarters away showing back bodice embroidery and dupatta cascade, looking back over her shoulder directly into the camera lens with a captivating gaze, dramatic depth of field."

---

## 4. Video Motion Prompts (Veo 3.1 & Omni)

### Motion Directorial Script
```text
Cinematic slow-motion 24fps fashion commercial film shot on Arri Alexa LF. 
A gorgeous South Asian woman wearing a deep maroon Kalibherva Anarkali gown with antique gold zari embroidery gracefully performs a fluid, deliberate 360-degree rotation in an opulent interior setting. The heavy velvet and silk fabric responds to gravity with authentic cloth dynamics, billowing softly during the turn without stretching or unnatural warping. Camera orbits smoothly at eye level, capturing the shimmering gold embroidery catching the warm ambient lighting. Seamless movement, zero character morphing, photorealistic skin and fabric textures, 4k ultra-high definition.
```

### Universal Negative Prompts
```text
(worst quality, low quality:1.4), plastic skin, airbrushed, cartoon, CGI, 3D render, deformed hands, extra fingers, missing fingers, mutated anatomy, face drift, identity change, distorted clothing, unrealistic cloth stretching, rubbery fabric, blurry, flickering, temporal jitter, oversaturated, color banding, watermark, text, signature.
```
