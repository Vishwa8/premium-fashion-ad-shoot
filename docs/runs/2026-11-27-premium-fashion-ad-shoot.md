# Run Record: Premium Fashion Ad Shoot

Date: 2026-11-27
Workspace: `/mnt/1.9TB/Dev/ayuti`
Repository: `https://github.com/Vishwa8/premium-fashion-ad-shoot`
Branch: `main`
Orchestrator: `9router/vxoa/google/gemini-3.8-flash`

## Resume here
- **State**: Parent-Child Architectural Refactor with Single Source of Truth & Separation of Concerns completed.
- **Parent Assets (Shared)**:
  - `base/`: Master clean plates (`base_front.png`, `base_back.png`) shared across all child products (zero copies in children).
  - `docs/templates/`: Modular reusable prompt schemas, camera angles, video configs, and copy generators.
  - `docs/`: Architectural blueprints, methodology, plan, progress tracker, and run records.
  - `.gitignore`: Exclusively at root level (no nested `.gitignore` files anywhere).
  - `README.md`: Workspace overview and parent-child architecture documentation.
- **Child Assets (`products/product_01/`)**:
  - `product.json`: Single source of truth for product specs (ASIN `B0HM458PW4`, title, color hex, fabric blend, zari type, target audience, dimensions).
  - `references/`: Raw vendor reference photos (5 Amazon images).
  - `mockups/`: Isolated 4-view 3D dress turnaround (`dress_3d_*.png`), locked try-on masters (`front_master.png`, `back_master.png`), unpixelated macro portrait (`closeup_portrait_native.png`), dual-scale master (`side_by_side_master.png`), and turnaround contact sheet (`combine_views.png`).
  - `poses/`: 5 editorial catalogue poses.
  - `videos/`: 360 turnarounds, individual scene takes, and final commercial cut.
  - `copy/`: Product-specific luxury catalog copy (`Catalog_Description.txt`) and 100-word prompt descriptor (`garment_desc.txt`).
- **Last green gate**: Refactored clean parent-child architecture with strict separation of concerns, single source of truth, and zero duplication. Purged redundant root-level folders (`mockup/`, `poses/`, `videos/`, `generations/`).
- **Next gate**: Step 4 Editorial Catalogue Poses generation and verification.
- **Branch**: `main`
- **HEAD sha**: `dcb232f`
- **Open findings**: 0 critical, 0 high.

---

## Active Pipeline Progress

| Step | Milestone | Status | Artifacts / Output |
| :--- | :--- | :---: | :--- |
| **Setup** | Isolated clean repo setup | **COMPLETED** | `base/base_front.png`, `base/base_back.png` (only 2 clean base images) |
| **Cleanup** | Clean `/mnt/1.9TB/Ayurti` & `/mnt/1.9TB/Dev/` | **COMPLETED** | Main disk released; only `/mnt/1.9TB/Dev/ayuti` retained |
| **Parent-Child**| Single Source of Truth & Separation of Concerns | **COMPLETED** | Parent holds `base/`, `docs/templates/`, `.gitignore`; Child holds modular `product_01/` chunks |
| **Step 1** | Isolated 4-view 3D dress mockup | **COMPLETED** | `products/product_01/mockups/dress_3d_front.png`, `angle_45.png`, `profile_90.png`, `back.png` |
| **Templates** | Ayurti Docs Ingestion | **COMPLETED** | Ingested try-on, 4-view, pose, video & catalog templates into `docs/templates/` (`dcb232f`) |
| **Step 2** | Locked Front & Back Masters | **COMPLETED** | Verified 0.0000% drift on hairstyle, face, and studio room -> `products/product_01/mockups/front_master.png`, `back_master.png` |
| **Step 3** | Crisp Dual-Scale Master & 360 Matrix | **COMPLETED** | `closeup_portrait_native.png` (1024x1024 macro), `side_by_side_master.png`, `combine_views.png` |
| **Step 4** | 5 Zero-Drift Editorial Catalogue Poses | **QUEUED** | Poses 1-5 conditioned on masters; strict room locking on Pose 4 (no foreign furniture) |
| **Step 5** | Storyboard Matrix & Veo 3.1 Videos | **QUEUED** | `storyboard_matrix.png` contact sheet + 360 turnarounds + 25s commercial cut |
