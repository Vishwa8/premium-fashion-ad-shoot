# AI Samson Character Consistency & Video Production Methodology

This document synthesizes the exact technical methodology from AI Samson's masterclasses:
1. **Video 1**: *The NEW Way To Get Perfect AI Character Consistency* (`https://www.youtube.com/watch?v=v-r-SWMiRo4`)
2. **Video 2**: *The AI Video Workflow Nobody Is Talking About* (`https://www.youtube.com/watch?v=9oCppy1gZpo`)

---

## 1. The Core Problem AI Samson Solves
When prompting diffusion models (Midjourney, Flux, Imagen) and video models (Veo, Runway, Kling):
- **Face Drift**: Moving the camera causes facial features to morph into different people.
- **Garment Drift**: Turning the character changes fabric patterns, embroidery seams, and color hues.
- **Physics Detachment**: In video models, loose fabric (like an Anarkali flare or dupatta) behaves like rubber or morphs into the background without gravitational weight.

---

## 2. Samson's 5 Fundamental Rules

### Rule 1: "Review Stills Before Anything Moves"
Never generate video from a text prompt alone or an unverified rough still. Every frame fed into the video model must already be 100% photo-real and anatomically coherent in 2D space.

### Rule 2: The Dual-Scale Master Still (Side-by-Side Reference)
Generate a single image with two panels:
- **Left Panel (Full-Body View)**: Captures total silhouette, footwear, floor drape, gown flare, and room illumination.
- **Right Panel (Close-Up Portrait)**: Captures iris reflection, skin pores, ear jhumkas, and intricate neckline embroidery.
- *Why this works*: When fed to multimodal vision models, the attention mechanism simultaneously links global proportions with micro-details.

### Rule 3: The 360° Turnaround Contact Sheet (`combine_views.png`)
Before producing dynamic motion, assemble a 4-to-5 angle contact sheet:
- `0° (Front)` -> `45° (Three-Quarter)` -> `90° (Profile)` -> `180° (Back)` -> `270° (Opposite Profile)`
- This prevents the model from hallucinating what the back of the dress looks like when she turns.

### Rule 4: The 360 Reference Video Turntable
Render two foundational turntable videos:
1. `360_turnaround_full.mp4`: The character rotating 360 degrees in full-body scale. This acts as the physics anchor for cloth simulation.
2. `360_turnaround_closeup.mp4`: The character rotating in close-up. This acts as the identity anchor for 3D facial structure.

### Rule 5: First-Frame & Last-Frame Keyframe Conditioning
When rendering scenes in Veo 3.1:
- Lock Frame 0 with the starting pose.
- Lock Frame N with the destination angle from the 360 turntable.
- Veo calculates the in-between latents strictly between these two validated endpoints, eliminating character morphing.
