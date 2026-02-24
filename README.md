# 🎧 YouTube Mixtape Automation (FastAPI + Streamlit)

Convert a simple notebook workflow into a **modular, API‑driven, UI‑based application** that produces a complete YouTube‑ready mixtape: audio, timestamps, description, and MP4 video.

This system lets you:

* ✔ Upload multiple songs
* ✔ Auto‑generate smooth DJ‑style fade transitions
* ✔ Create YouTube descriptions with timestamps
* ✔ Combine audio + background image into MP4 (FFmpeg)
* ✔ Use an easy Streamlit web interface
* ✔ Run long tasks safely via FastAPI background jobs

---

## 🚀 Features

### 🎶 1) Mixtape Generator

* Concatenates multiple tracks
* Smooth fade‑in / fade‑out transitions
* Channel & frame‑rate normalization
* Outputs `mixtape.mp3`

### 📝 2) YouTube Description Generator

* Reads track durations
* Builds timestamped tracklist
* Adds hashtags & metadata

### 🎥 3) Video Renderer (FFmpeg)

* Combines static image + MP3 → MP4
* Optimized for long audio
* `libx264` video + `AAC` audio codec

### 🖥 4) Streamlit Frontend

A simple UI to:

* Upload audio files
* Create mixtape
* Generate description
* Render video
* Download results

### 🛠 5) FastAPI Backend

API endpoints for:

* File upload
* Background mixtape creation
* Description generation
* Video rendering
* Job status polling

---

## 🧩 How It Works (Pipeline)

1. **Upload Tracks**
   Streamlit uploads → FastAPI saves to `/uploaded/{job_prefix}/`

2. **Create Mixtape**
   FastAPI background job → `audio.py` applies fades → `output/mixtape.mp3`

3. **Generate Description**
   Reads each track → calculates timestamps → returns formatted description

4. **Create Video**
   `video.py` runs FFmpeg → image + MP3 → `output/mixtape_vid.mp4`

5. **Download**
   Streamlit provides download links for final files

**UI:** [http://localhost:8501](http://localhost:8501)

---

## 🛠 API Endpoints

| Endpoint                 | Method | Description                  |
| ------------------------ | ------ | ---------------------------- |
| `/upload-track/`         | POST   | Upload a single audio file   |
| `/create-mixtape/`       | POST   | Start background mixtape job |
| `/job/{job_id}`          | GET    | Check job status             |
| `/generate-description/` | POST   | Generate YouTube description |
| `/make-video/`           | POST   | Combine image + audio → MP4  |
| `/download/`             | GET    | Download output files        |

---

## 🧰 Tech Stack

* **Python** – core logic
* **FastAPI** – backend & background jobs
* **Streamlit** – frontend UI
* **Pydub** – audio processing
* **FFmpeg** – audio/video encoding

**Supported formats:** MP3, WAV, FLAC, OGG, AAC, M4A

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/sauravyadav7721/End-to-end-Youtube-mixtape-automation.git
cd End-to-end-Youtube-mixtape-automation
```

### 2. Install uv (fast Python package manager)

```bash
pip install uv
```

### 3. Create environment using uv

```bash
uv venv ytmitape
```

Activate:

**Windows**

```bash
ytmitape\Scripts\activate
```

**Linux / Mac**

```bash
source ytmitape/bin/activate
```

### 4. Install dependencies

```bash
uv pip install -r requirements.txt
```

```bash
pip install -r requirements.txt
```

---

## 🎬 Install FFmpeg (Required)

1. Download from: [https://ffmpeg.org/download.html](https://ffmpeg.org/download.html)
2. Extract the archive
3. Add the `bin` folder to system PATH

Verify:

```bash
ffmpeg -version
```

---

## ▶️ Running the Application

### Start FastAPI backend

```bash
uvicorn backend.main:app --reload
```

Backend runs at:

```
http://127.0.0.1:8000
```

### Start Streamlit frontend

```bash
streamlit run frontend/app.py
```

Open in browser:

```
http://localhost:8501
```

---

## 📦 Output Files

* `mixtape.mp3` → Final merged audio
* `mixtape_vid.mp4` → YouTube‑ready video
* `description.txt` → YouTube description
* `timestamps.txt` → Track timestamps

---

## 📝 Notes & Possible Improvements

* Current job store is **in‑memory** (resets on restart)
* Add Redis / SQLite for persistence
* Add LUFS loudness normalization
* Add authentication for local privacy
* Auto thumbnail generation
* Auto YouTube upload via API

---

## ❤️ Credits

Created as a modular end‑to‑end automation project using:

**Python • FastAPI • Streamlit • FFmpeg • Pydub**

---

## ⭐ Support

If this project helped you, please consider giving the repository a star!

