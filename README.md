🎞️ Multimodal Media-to-Text Pipeline (ASR · OCR · Translation · Retrieval)

An end-to-end **multimodal AI pipeline** that converts short-form video clips into structured text outputs by combining:

- Speech transcription (ASR)
- On-screen text extraction (OCR)
- Optional machine translation
- LLM-assisted query generation and external source retrieval

The system is designed to transform short video content into readable, reusable text for
**summarization, indexing, translation, and basic verification workflows**.

---

## ✅ Features

### 1) Video Ingestion & Preprocessing
- Downloads short video segments using `yt-dlp` and `ffmpeg`
- Extracts lightweight subclips with `moviepy` for faster processing

### 2) Speech → Text (ASR)
- Transcribes audio using **OpenAI Whisper (base)**
- Produces a full spoken-text transcript from video audio

### 3) Frame → Text (OCR)
- Extracts frames using `opencv-python`
- Crops subtitle regions and applies preprocessing:
  - Grayscale conversion
  - Thresholding for contrast enhancement
- Performs OCR using **Tesseract (pytesseract)**

### 4) Translation (Optional)
- Translates extracted text into a target language (example: English → Korean)
- Notes:
  - Translation quality varies by backend
  - For production use, prefer stable APIs or well-evaluated open models

### 5) Retrieval & Verification Helpers (Optional)
- Generates search queries from transcript text using a lightweight LLM
  (`google/flan-t5-small`)
- Retrieves top external sources via **SerpAPI (Google Search)**
- Surfaces links and snippets for downstream human review

---

## 🧱 Tech Stack

**Video**
- yt-dlp, ffmpeg, moviepy

**Vision / OCR**
- opencv-python, pytesseract, tesseract-ocr

**Speech**
- openai-whisper

**NLP / LLMs**
- Hugging Face Transformers
- google/flan-t5-small

**Retrieval**
- serpapi, google-search-results

**Translation (optional)**
- googletrans (demo) or alternative translation backends

---
## 🔐 Environment Variables

If using SerpAPI for external search:

```bash
SERPAPI_API_KEY=your_api_key_here

```

## ⚠️ Notes / Limitations

- OCR quality depends heavily on subtitle size, contrast, and video compression.
- Whisper output may include transcription errors (especially names/numbers).
- Translation quality depends on the backend (demo translators may be inconsistent).
- Verification search retrieves sources but does not guarantee correctness—always review sources critically.

---

## ▶️ How to Run

1) Install dependencies (see notebook cells).  
2) Provide a video URL.  
3) Run the pipeline:
- download → clip → frames → OCR
- transcription
- optional translation
- optional search + source retrieval

---

## 🗂️ Suggested Outputs (Recommended)

Consider exporting results to JSON for clean reuse:

- `transcript`
- `ocr_text`
- `translations`
- `generated_search_query`
- `retrieved_sources` (title/snippet/url)
- `video_metadata` (url, timestamps, clip length)

---

## 🚀 Improvement Ideas

- Automatic subtitle-region detection (instead of fixed cropping)
- Better OCR preprocessing (adaptive thresholding, morphology, EasyOCR alternative)
- Claim extraction + evidence ranking for verification
- A clean CLI wrapper: `python main.py --url ... --translate ko --search`

---
