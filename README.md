# 🎞️ Multimodal Media-to-Text Pipeline (ASR + OCR + Translation + Optional Fact-Check)

A Python notebook that converts short video clips into **structured text outputs** by combining:
- **Speech transcription (ASR)** with Whisper
- **On-screen text extraction (OCR)** with Tesseract
- **Translation** of extracted text (optional)
- **Search query generation + source retrieval** for verification (optional)

This is useful for turning short-form content into readable text for: summarization, indexing, translation, and basic verification workflows.

---

## ✅ Features

### 1) Download a short video clip
- Uses `yt-dlp` + `ffmpeg` to download a lightweight segment
- Uses `moviepy` to cut a smaller subclip for faster processing

### 2) Speech → Text (ASR)
- Runs OpenAI Whisper (`base`) to generate a transcript from audio

### 3) Frame → Text (OCR)
- Extracts frames using `opencv-python`
- Crops subtitle regions and preprocesses:
  - grayscale
  - thresholding for higher contrast
- Runs OCR via `pytesseract`

### 4) Translation (Optional)
- Translates extracted text into a target language (example: English → Korean)
- Note: different translation methods vary in quality; for production use, prefer stable APIs or well-evaluated open models.

### 5) Verification Helpers (Optional)
- Generates a search query from transcript text (`transformers` with `google/flan-t5-small`)
- Retrieves top source links via SerpAPI (Google results)

---

## 🧱 Tech Stack

- Video: `yt-dlp`, `ffmpeg`, `moviepy`
- Frames/OCR: `opencv-python`, `pytesseract`, `tesseract-ocr`
- Transcription: `openai-whisper`
- Query generation: `transformers` + `google/flan-t5-small`
- Search (optional): `serpapi` / `google-search-results`
- Translation (optional): `googletrans` (demo) or other translation backends

---

## 🔐 Environment Variables

If using SerpAPI for search:
- `SERPAPI_API_KEY`

Do not hardcode keys inside notebooks.

---

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
- A clean CLI wrapper: `python main.py --url ... --translate ko --factcheck`

---

## 📜 License

MIT License
