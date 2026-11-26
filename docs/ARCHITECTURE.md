# Premium Fashion Ad Shoot: Technical Architecture & Infrastructure

## 1. Multi-Modal Endpoint Routing

### API Gateway (Local 9Router)
- **Host**: `http://127.0.0.1:20128/v1`
- **Vertex AI Project**: `project-fc1f91e7-d270-4adc-ab2`
- **Region**: `us-central1`
- **Authentication**: Google Cloud SDK Service Account (`vertex-9router@project-fc1f91e7-d270-4adc-ab2.iam.gserviceaccount.com`)

### Model Hierarchy
| Purpose | Model ID | Invocation Method | Resolution / Length |
| :--- | :--- | :--- | :--- |
| **Fast Prototyping (Images)** | `gemini-3.1-flash` / Fast Inpaint | Direct API / 9Router | 1024x1024 (1K) |
| **High-Fidelity Stills** | Gemini 3.1 Pro / Imagen 3 Pro | Multimodal Vision / Inpaint | 3072x5504 -> 4K |
| **Motion & Physics Testing** | `veo-3.1-fast-generate-001` | `predictLongRunning` | 720p, 4-6s |
| **Production Video Render** | `veo-3.1-generate-001` | `predictLongRunning` | 1080p / 4K, 8s (audio enabled) |

---

## 2. Zero-Drift Compositing Strategy

To guarantee zero identity and environment drift from `base/base_front.png` and `base/base_back.png`:
1. **Base Inpainting Mask**:
   - Isolates solely the garment zone.
   - 100% of the influencer's face, hair, arms, feet, and the room environment are protected by pixel-exact preservation.
2. **Garment Transfer Engine**:
   - Inpaints the Kalibherva Maroon Anarkali gown into the masked region using high-resolution Amazon product references as cross-attention anchors.
3. **Harmonization & Edge Blending**:
   - Seamless gradient feathered alpha compositing along borders ensures natural fabric shadow falloff against the studio wall and carpet.

---

## 3. Cost Management & Accountability
Every API call is metered and appended to `generations/cost_tracker.csv`:
```csv
timestamp,step,model_id,resolution,cost_usd,status,notes
```
