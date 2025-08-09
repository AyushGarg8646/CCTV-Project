                                      # Person Tracking & Re-Identification in CCTV Footage

## Overview
This project integrates **ByteTrack** (multi-object tracking) with **FastReID** (person re-identification) to track and re-identify individuals across CCTV footage in real time.  
It assigns unique IDs to people, even if they temporarily leave and re-enter the frame, using deep visual feature matching.
 tching and reappearance detection.  

---

## Features
- **YOLOv8 + ByteTrack** for fast & accurate person detection & tracking.  
- **FastReID** for matching appearances across frames.  
- **Appearance/Reappearance Tracking** with timestamps.  
- **Real-time CSV logging** of events.  
- **Customizable similarity thresholds** and frame confirmation counts.  

---

## Project Structure
```
.
├── model/                 # Pre-trained FastReID model
├── bytetrack.yaml          # Tracker configuration
├── person_appearance_log.csv # CSV logs of appearances & reappearances
├── main.py                 # Main tracking + re-id script
├── README.md               # Project documentation
```

---

##  Requirements
Install dependencies with:
```bash
pip install ultralytics torch torchvision opencv-python
```
You also need to install FastReID dependencies (for feature extraction):  
```bash
pip install fastreid
```

---

## How It Works
1. **YOLOv8** detects persons in each CCTV frame.  
2. **ByteTrack** assigns short-term tracking IDs.  
3. **FastReID** extracts visual embeddings for each detected person.  
4. Embeddings are matched against stored identities using **cosine similarity**.  
5. IDs are maintained across occlusions and exits/re-entries.  
6. All appearance & reappearance events are logged to a CSV file.  

---

##  Usage
Run the tracking script:
```bash
model.ipynb
```

While running:  
- Press **Q** to quit.  
- CSV log will be saved as `person_appearance_log.csv` in the project directory.  

---

## Example Log Output
| PersonID | EventType     | Time_HHMMSS | UnixTimestamp   |
|----------|--------------|-------------|-----------------|
| 0        | appearance   | 12:04:32    | 1691650472.45   |
| 0        | reappearance | 12:04:45    | 1691650485.28   |
| 1        | appearance   | 12:05:01    | 1691650501.83   |

---

##  Configuration
You can tweak the following parameters in `main.py`:  
- `SIMILARITY_THRESHOLD` → Cosine similarity for ID matching.  
- `CONFIRM_FRAMES` → Frames required before assigning a new ID.  
- `REAPPEAR_THRESHOLD` → Seconds before an ID is counted as reappearing.  
- `MIN_BOX_AREA` → Minimum area of a detection to consider.  
- `FEATURE HISTORY` → No. of vector embeddings to store,default=30.  
---

## License
This project uses **AGPL-3.0** due to YOLOv8 licensing.
