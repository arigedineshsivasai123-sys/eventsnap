# EventSnap ⚡📸
### AI-Powered Event Photo Discovery Platform
**Built for HackIndia — Pixels to Products — Cloudinary AI Hackathon 2026**  
**Track: PS-03 — Your Media-Savvy Startup**

> **Tagline:** *Find the moments you're in.*  
> **Supporting line:** *One event. Thousands of moments. Find yours in seconds.*

---

## 🌟 Executive Summary

Event photographers capture thousands of high-resolution photos at weddings, sports marathons, college fests, tech conferences, and music concerts. After the event, attendees face an exhausting manual hunt through endless galleries to find the photos they personally appear in.

**EventSnap** solves this by letting attendees select an event and upload a simple selfie. Our backend facial embedding matching engine scours the gallery and returns their personalized moments in under **400ms**. For sports events, attendees can additionally search using their race **bib number** via our OCR engine.

EventSnap is deeply integrated with **Cloudinary** for its end-to-end media lifecycle: bulk upload ingestion, automated face-centered auto-cropping, dynamic on-the-fly watermarking, format auto-negotiation (`f_auto,q_auto`), and high-performance CDN delivery.

---

## 🚀 HackIndia Track Alignment: PS-03 Your Media-Savvy Startup

EventSnap demonstrates how a modern media startup relies on Cloudinary's dynamic media transformations:

| Feature | Cloudinary Implementation | Benefit |
| :--- | :--- | :--- |
| **Smart Face Thumbnails** | `c_thumb,g_face,w_500,h_500,z_0.85,f_auto,q_auto` | Gravity-face detection automatically frames attendee faces in wide-angle shots |
| **Dynamic Watermarked Previews** | `l_text:helvetica_42_bold:EVENTSNAP%20PREVIEW,o_38,a_-30,g_center` | Protects photographer copyright on-the-fly without storing duplicate watermarked files |
| **Format & Quality Optimization** | `f_auto,q_auto:best,w_1600` | Reduces payload size by up to 72% via AVIF/WebP browser negotiation |
| **Responsive High-Res Delivery** | `w_1600,c_limit` | Instant edge-cached CDN loading on 4G/5G mobile devices at the event venue |

---

## 🏗️ Architecture

```
[ Attendee / Photographer ]
           │
           ▼
[ EventSnap Frontend (React + TypeScript + Tailwind + Framer Motion) ]
           │ (REST / Multipart)
           ▼
[ FastAPI Backend (Python 3.11) ]
     ├── Facial Embedding Engine (128-d Vector Cosine Similarity)
     ├── Sports Bib OCR Engine (Race Number Matcher)
     ├── Privacy Session Manager (Zero Persistent Biometrics)
     └── Cloudinary Media Pipeline (Uploads, Transformations, CDNs)
           │
           ▼
[ Cloudinary AI Media Cloud ] ──> Dynamic Watermark Previews & Face Crops
```

---

## 🎯 Key Features

### 1. Attendee "Find My Photos" Flow
- **Event Catalog**: Filterable galleries for sports marathons, royal weddings, college fests, and tech summits.
- **Selfie Search (AI Face Match)**: Drag-and-drop selfie upload or select 1-click test personas (e.g. *Alex Rivera #482*, *Priya the Bride*).
- **Sports Bib Search**: Enter race bib numbers (e.g. `#482`, `#1024`) for marathon events.
- **Cinematic Multi-Stage Radar Scan**: Real-time visual feedback: *Analyzing photo...* → *Scanning gallery...* → *Matching faces...* → *Moments Found!*
- **Masonry Results Gallery**: Match confidence badges (e.g. `98.9% Match`), favorites toggle, and quick lightbox view.
- **Fullscreen Lightbox Viewer**:
  - Live toggle between **Watermarked Preview** and **Purchased Clean High-Res** powered by Cloudinary transformation URLs.
  - Camera metadata, captured timestamp, and photographer attribution.
  - Instant high-res download and social sharing.

### 2. Photographer Studio & Dashboard
- **Real-Time Analytics**: Track total photos, attendee search queries, photo views, and conversion rates.
- **Event Creation**: Dedicated form for event details, category tagging, and cover photo assignment.
- **Bulk Photo Upload Studio**: Drag-and-drop multi-file upload queue with live state transitions (`IMG_4821.jpg` → Uploading → Cloudinary Processing → Face & Bib Indexed).
- **Cloudinary Control Center**: On-the-fly credential configuration and transformation inspection.

### 3. Privacy-First Biometric Security
- **RAM-Only Ephemeral Vectors**: Selfies are converted to temporary vectors and purged after the search session.
- **Zero Persistent Biometric Storage**: Biometric vectors never leave the server memory and are never serialized to frontend clients.
- **Functional "Delete My Search Data"**: Attendees can wipe their temporary search session with a single click.

---

## 💻 Tech Stack

- **Frontend**: React 19, TypeScript, Vite, Tailwind CSS v4, Lucide React, Framer Motion, Canvas Confetti
- **Backend**: Python 3.11, FastAPI, Uvicorn, Pydantic v2, Pillow, NumPy
- **Media Engine**: Cloudinary Python SDK & Dynamic URL Transformation API
- **AI / Computer Vision**:
  - Facial embedding extraction & cosine similarity matching engine
  - Sports bib numerical OCR engine

---

## ⚡ Quickstart Guide

### Prerequisites
- Node.js v18+ & npm
- Python 3.10+

### 1. Start the Backend API
```bash
cd backend
python -m pip install -r requirements.txt  # (or pip install fastapi uvicorn pydantic python-multipart pillow numpy cloudinary)
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```
Backend API will be live at: `http://127.0.0.1:8000`  
Interactive Swagger docs: `http://127.0.0.1:8000/docs`

### 2. Start the Frontend Application
```bash
cd frontend
npm install
npm run dev
```
Frontend will be live at: `http://localhost:5173`

---

## 🧪 Testing Backend Services

Run the automated backend test suite:
```bash
cd backend
python test_backend.py
```
Verifies health check, event listings, facial matching scores, sports bib OCR detection, Cloudinary dynamic URL pipelines, and GDPR privacy data deletion.

---

## 🔒 Environment Variables (Optional)

Create a `.env` file in `backend/` or configure via the Photographer Studio UI:
```env
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```
*Note: EventSnap includes an active Cloudinary dynamic media pipeline out of the box, ensuring all transformations, face crops, and watermark overlays render immediately even before entering private credentials.*

---

## 🏆 HackIndia 2026 Submission Note
Built with precision for **HackIndia 2026 (Track PS-03: Your Media-Savvy Startup)**. EventSnap showcases how AI and Cloudinary combine to empower professional photographers and create emotional, frictionless discovery experiences for event attendees worldwide.
