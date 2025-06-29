# From Photo to Pattern: Building an AI-Powered Diamond Art Design Platform

<img src="https://cdn-icons-png.flaticon.com/512/2920/2920054.png" alt="Diamond Art Icon" style="float:left; width:130px; height:130px; margin-right:20px;">

## Introduction

Imagine turning any photo into a beautiful, custom diamond art pattern—ready for crafting, sharing, or printing. Our project makes this possible, blending advanced AI-driven image processing with a seamless user experience. Designed for hobbyists, crafters, and creative businesses, this platform automates the complex process of converting images into bead-based or shape-based SVG patterns, complete with color mapping and edge enhancements.

What sets this project apart is its smart use of AI and automation, transforming a traditionally manual, time-consuming task into a fast, accessible, and highly customizable digital service.

---

## General Overview

At its core, the platform allows users to upload any image and receive a ready-to-use SVG pattern for diamond art. Key features include:

- **Edge Detection:** Enhance image outlines for clearer, more defined patterns.
- **Color Quantization & Mapping:** Reduce image colors and map them to real-world DMC thread/bead colors.
- **SVG Pattern Generation:** Create scalable, printable SVG files with color-coded rectangles or overlaid bead/shape images.
- **Cloud Storage Integration:** Save and share results via secure cloud links.
- **Flexible Output:** Download files locally or access them from anywhere.

**Use Cases:**  
- DIY crafters designing custom diamond art  
- Small businesses offering personalized kits  
- Artists digitizing their work for new mediums

---

## Tech Stack

**Backend:**  
- **Python 3.11+** — Core language  
- **FastAPI** — High-performance API framework  
- **Uvicorn** — ASGI server for running FastAPI  
- **Poetry** — Dependency management

**AI/ML & Image Processing:**  
- **OpenCV** — Edge detection and image manipulation  
- **scikit-learn** — Color quantization (KMeans clustering)  
- **Pillow (PIL)** — Image loading and processing  
- **NumPy** — Efficient numerical operations

**Cloud & Storage:**  
- **AWS S3 (via boto3)** — File storage and presigned URL generation

**Other:**  
- **Pydantic** — Data validation and response schemas  
- **Custom Logging** — For robust monitoring and debugging

---

## How AI Powers the System

### The Role of AI

AI is at the heart of the platform’s image transformation pipeline. Here’s how:

- **Color Quantization:**  
  Using KMeans clustering (scikit-learn), the system reduces the number of colors in an image to a user-specified palette. This is crucial for translating complex images into manageable, craft-friendly patterns.

- **Color Mapping:**  
  Each quantized color is mapped to the nearest DMC thread/bead color using Euclidean distance in RGB space. This ensures the output pattern uses real, available colors.

- **Edge Detection:**  
  OpenCV’s Canny edge detection algorithm highlights important outlines, making the final pattern clearer and easier to follow.

### Integration

- All AI/ML operations are performed server-side, triggered by API endpoints.
- The pipeline is modular, allowing for easy extension (e.g., adding new pattern styles or color sets).

### Challenges & Solutions

- **Color Accuracy:**  
  Mapping arbitrary image colors to a limited set of DMC colors required careful tuning of the quantization and mapping algorithms.
- **Performance:**  
  Processing large images efficiently was solved by optimizing image loading and using NumPy for fast computations.
- **User Flexibility:**  
  Parameters like number of colors and bead size are user-configurable, balancing automation with creative control.

---

## Technical Breakdown

### Database & Storage

- No traditional database; files are stored in AWS S3.
- Temporary files are managed locally during processing, then uploaded or deleted as needed.

### Backend Architecture

- **FastAPI** serves as the main API layer.
- Modular service structure:  
  - image_processing.py — API endpoints  
  - `service/` — Core logic for color quantization, edge detection, SVG generation, and overlays  
  - `job/` — Background jobs for saving to S3  
  - `utils/` — Logging and helper functions

### Key API Endpoints

- `/image/apply-edges/` — Apply edge detection to an uploaded image.
- `/image/generate-rect-svg/` — Generate a rectangle-based SVG pattern from an image.
- `/image/overlay-beads-on-svg/` — Overlay bead images onto an SVG pattern.
- `/image/overlay-shapes-on-svg/` — Overlay shape images onto an SVG pattern.

### Engineering Decisions

- **Stateless API:** Each request is independent, making scaling and deployment easier.
- **Cloud-first Storage:** Using S3 for output files enables easy sharing and remote access.
- **Extensible Design:** New pattern types or color sets can be added with minimal changes.

---

## User Journey Walkthrough

1. **Upload Image:**  
   The user uploads a photo via the web interface (or API client).

2. **Choose Options:**  
   The user selects parameters like bead size, number of colors, and output type (rectangles, beads, shapes).

3. **Processing Begins:**  
   - The backend receives the image.
   - Edge detection is applied (if selected).
   - The image is quantized to the chosen number of colors.
   - Each color is mapped to the nearest DMC color.
   - An SVG pattern is generated, with rectangles colored and labeled accordingly.

4. **(Optional) Overlay:**  
   - The user can request overlays of bead or shape images onto the SVG for a more realistic preview.

5. **Save & Share:**  
   - The result is saved locally or uploaded to AWS S3.
   - The user receives a download link or S3 URL.

6. **Download & Craft:**  
   - The user downloads the SVG and uses it to create their diamond art masterpiece.

---

## System Flowchart (Text-Based)

```
User
  ↓
[Frontend Uploads Image & Options]
  ↓
FastAPI Backend
  ↓
[API Endpoint Receives Request]
  ↓
[Image Processing Pipeline]
    → Edge Detection (OpenCV)
    → Color Quantization (KMeans)
    → Color Mapping to DMC (NumPy)
    → SVG Generation (Pillow, XML)
    → (Optional) Overlay Bead/Shape Images
  ↓
[Temporary File Storage]
  ↓
[Save to AWS S3 or Local]
  ↓
[Return Download Link or S3 URL]
  ↓
User Downloads SVG Pattern
```

---

## Conclusion

This project demonstrates how AI and modern Python frameworks can revolutionize creative workflows. By automating the transformation of images into craft-ready patterns, we’ve empowered users to bring their ideas to life with unprecedented ease and precision.

**Technical highlights:**  
- Advanced AI-driven image processing  
- Robust, cloud-integrated backend  
- Extensible, modular architecture

**Creative impact:**  
- Makes custom diamond art accessible to everyone  
- Opens new possibilities for artists, crafters, and businesses

**What’s next?**  
- Adding more pattern styles (e.g., circular, mosaic)  
- Integrating a frontend for real-time previews  
- Expanding to other crafts (cross-stitch, pixel art)

---
