# Strelingo — Stremio Dual Language Subtitles Addon

A self-hosted [Stremio](https://www.stremio.com/) addon that fetches subtitles for movies and series from **OpenSubtitles** and merges two language tracks into a single SRT file — designed for language learners who want native and target language subtitles displayed simultaneously.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/import/project?template=https://github.com/nil3190/strelingo_Demov1)

**Live Demo:** [strelingo-demov1.vercel.app](https://strelingo-demov1.vercel.app)

---

## Screenshot

![Strelingo dual subtitle preview](https://github.com/user-attachments/assets/d2441e6c-82b7-4115-876d-1af0e419f6df)

---

## Features

- Fetches subtitles from **OpenSubtitles** and [Buta no Subs](https://github.com/Pigamer37/buta-no-subs-stremio-addon) (better Japanese coverage)
- **Merges two subtitle tracks** into a single `.srt` stream
- Secondary (translation) subtitles rendered in *italic* style
- Handles **Gzip-compressed** subtitle files automatically
- **Multi-encoding support** via `chardet` + `iconv-lite` (great for non-Latin scripts)
- Configurable directly from the Stremio addon settings UI:
  - Primary Language (audio language)
  - Translation Language (your native language)
- Subtitle files hosted via **Vercel Blob** or **Supabase Storage**
- One-click deploy to Vercel

---

## Tech Stack

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-43853D?style=flat-square&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)

**Key Dependencies:** `stremio-addon-sdk` · `axios` · `srt-parser-2` · `pako` · `chardet` · `iconv-lite` · `@vercel/blob` · `@supabase/supabase-js`

---

## Local Setup

### Prerequisites

- [Node.js](https://nodejs.org/) v14+
- An [OpenSubtitles](https://www.opensubtitles.com/) account and API key
- Either a **Vercel Blob** token or **Supabase** project credentials (for hosting merged SRT files)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/nil3190/strelingo_Demov1.git
   cd strelingo_Demov1
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the project root and add your credentials:

   **Option A — Vercel Blob:**
   ```env
   BLOB_READ_WRITE_TOKEN=your_vercel_blob_token
   ```

   **Option B — Supabase Storage:**
   ```env
   SUPABASE_URL=your_supabase_url
   SUPABASE_SERVICE_KEY=your_supabase_service_key
   SUPABASE_ANON_KEY=your_supabase_anon_key
   ```

4. Start the addon server:
   ```bash
   npm start
   ```

### Installing into Stremio

1. Open [http://localhost:7000](http://localhost:7000) in your browser.
2. Select your **Primary Language** (audio language) and **Translation Language**.
3. Click **Install Addon** — Stremio will open and ask you to confirm.
4. Play any movie or series in Stremio and select the merged subtitle track.

---

## Deployment (Vercel)

Click the **Deploy with Vercel** button above, or run:

```bash
npm install -g vercel
vercel --prod
```

Set your environment variables in the Vercel dashboard under **Settings → Environment Variables**.

---

## How It Works

1. When Stremio requests subtitles, the addon queries OpenSubtitles for both configured languages.
2. Both SRT files are downloaded, decompressed (if gzipped), and decoded to UTF-8.
3. The subtitle lines are merged: the primary language on top, the translation underneath in *italics*.
4. The merged SRT is uploaded to Vercel Blob or Supabase and the URL is returned to Stremio.

---

## License

MIT
