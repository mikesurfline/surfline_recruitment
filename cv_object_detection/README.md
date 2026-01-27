# Object Detection on Busy Beaches

## Overview

This take-home test assesses your ability to analyze computer vision model outputs, identify performance issues, and extract meaningful insights from real-world detection data. You'll work with detection outputs from production computer vision models.

---

## What You'll Receive

You will receive two datasets - one from **Oceanside, CA, USA** and one from **Burleigh Heads, Australia**. Each dataset contains:

1. **Video files** (two per dataset):
   - Raw 10-minute video footage from a Surfline surf camera
   - Annotated video with detection bounding boxes overlaid (sampled at ~1Hz)

2. **JSON file** (one per dataset):
   - Detection outputs containing bounding boxes, confidence scores, class IDs, and timestamps

---

## Data Format

### JSON Structure

Each JSON file has the following structure:

```json
{
  "frame_width": 1280,
  "frame_height": 720,
  "dets": {
    "0": [
      {
        "y_min": 0.485596,
        "x_min": 0.623047,
        "y_max": 0.507812,
        "x_max": 0.628418,
        "score": 0.72,
        "class": 12,
        "timestamp": 1768438454.18
      }
    ],
    "23": [...],
    "46": [...]
  }
}
```

### Field Descriptions

| Field | Description |
|-------|-------------|
| `frame_width`, `frame_height` | Video resolution in pixels (typically 1280×720) |
| `dets` | Dictionary of detections keyed by frame index (as strings) |
| Frame keys (`"0"`, `"23"`, `"46"`, ...) | Frame indices from the source video. The model processes ~1 frame per second and source videos are ~20-30fps. |
| `y_min`, `x_min`, `y_max`, `x_max` | Normalized bounding box coordinates (0.0–1.0). Multiply by frame dimensions to get pixel coordinates. |
| `score` | Detection confidence (0.0–1.0) |
| `class` | Class ID (see Appendix for mapping) |
| `timestamp` | Unix timestamp for the frame |

---

## Your Task

### Part 1: Model Performance Analysis (Oceanside, CA)

**Use ONLY the Oceanside, CA dataset for this part.** The detection model provided seems to struggle in this footage.
- Where does the model appear to have problems?
  - Specific object classes
  - Spatial regions of the frame
  - Anything else that you notice?
- How would you go about improving the performance in these cases?

### Part 2: Deriving Insights from Detection Data (Burleigh Heads, Australia)

**Use ONLY the Burleigh Heads, Australia dataset for this part.** This dataset contains rich detection data from pumping surf.
Beyond raw detections, what can this data tell us about the surf spot and the conditions?
- What visualizations or derived metrics would be useful for Surfline?
- How can you process, transform, or analyze the data to extract additional value for Surfline from these detections?

---

## Deliverables

### Required: Report (PDF or PPTX)
- Executive summary (1 paragraph)
- Detailed findings for Parts 1 and 2
- Visualizations (embedded or referenced)
- Conclusions and actionable recommendations
- **Maximum 10 pages** including visualizations

### Optional: Code (Jupyter Notebook or Python scripts)
Sharing your code is encouraged but not required - we value seeing your creativity and analytical process.
- All analysis and visualization code
- Code should run end-to-end
- Brief README with setup instructions (we like `uv`, but any package manager is fine)

---

## Evaluation Criteria

We're looking for:
- Are conclusions well-supported by evidence?
- Do you demonstrate understanding of CV model behavior?
- Are your recommendations actionable and valuable?
- Is your report clear, concise, and well-organized?

---

## Tips

1. Skim the raw footage first to understand the scene, then watch the annotated version to see where detections fail or struggle.
2. Don't just describe observations - explain why they matter and what should be done about them.
3. Think about what would actually help surfers, safety organizations (like RNLI), or Surfline as a business.
4. A few deep insights beat many shallow ones.
5. For Part 1, don't hesitate to suggest improvements that you can't implement here (like retraining a model or collecting new training data). We value your understanding of how to improve model performance - the strategic thinking matters more than executable code.

---

# Appendix: Detection Class Labels and Colors


## Class Label Mapping

The detection model outputs class IDs in the `class` field of each detection. The mapping from class ID to class name is as follows:

| Class ID | Class Name | Description |
|----------|------------|-------------|
| 1 | `BeachPerson` | Person on the beach |
| 2 | `SUP` | Stand-up paddleboard |
| 3 | `SurferPaddling` | Surfer paddling |
| 4 | `SurferSitting` | Surfer sitting on board |
| 5 | `SurferSurfing` | Surfer actively surfing |
| 6 | `Jetski` | Jet ski |
| 7 | `Kayaks` | Kayak |
| 8 | `Motorboat` | Motorboat |
| 9 | `Sailboat` | Sailboat |
| 10 | `BeachPersonLaying` | Person lying on beach |
| 11 | `BeachPersonSitting` | Person sitting on beach |
| 12 | `BeachPersonWading` | Person wading in water |
| 13 | `Tent` | Tent |
| 14 | `Umbrella` | Umbrella |
| 15 | `RedFlag` | Red flag |
| 16 | `YellowFlag` | Yellow flag |
| 17 | `RedYellowFlag` | Red-yellow flag |
| 18 | `BlackWhiteFlag` | Black-white flag |

## Bounding Box Colors

Each class has an associated color for drawing bounding boxes. Colors are specified in hexadecimal format (RGB).

| Class ID | Class Name | Hex Color | RGB Color | Color Name |
|----------|------------|-----------|-----------|------------|
| 1 | `BeachPerson` | `#408FFF` | (64, 143, 255) | Dodger Blue |
| 2 | `SUP` | `#ffe51e` | (255, 229, 30) | Yellow |
| 3 | `SurferPaddling` | `#00ff7f` | (0, 255, 127) | Spring Green |
| 4 | `SurferSitting` | `#F68F46` | (246, 143, 70) | Orange |
| 5 | `SurferSurfing` | `#D54530` | (213, 69, 48) | Red |
| 6 | `Jetski` | `#DE7065` | (222, 112, 101) | Light Coral |
| 7 | `Kayaks` | `#EB8055` | (235, 128, 85) | Salmon |
| 8 | `Motorboat` | `#af38c7` | (175, 56, 199) | Medium Orchid |
| 9 | `Sailboat` | `#9B641B` | (155, 100, 27) | Dark Goldenrod |
| 10 | `BeachPersonLaying` | `#00ffff` | (0, 255, 255) | Aqua/Cyan |
| 11 | `BeachPersonSitting` | `#00bfff` | (0, 191, 255) | Deep Sky Blue |
| 12 | `BeachPersonWading` | `#ee82ee` | (238, 130, 238) | Violet/Pink |
| 13 | `Tent` | `#000000` | (0, 0, 0) | Black |
| 14 | `Umbrella` | `#000000` | (0, 0, 0) | Black |
| 15 | `RedFlag` | `#FFFF00` | (255, 255, 0) | Yellow |
| 16 | `YellowFlag` | `#FF0000` | (255, 0, 0) | Red |
| 17 | `RedYellowFlag` | `#FFA500` | (255, 165, 0) | Orange |
| 18 | `BlackWhiteFlag` | `#000000` | (0, 0, 0) | Black |


