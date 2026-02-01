# InsightCV — AI Resume Analyzer ✨

**A small, local web app that analyzes resumes and gives ATS-friendly scores and practical improvement tips using AI.**

---

## 🚀 Overview

InsightCV helps job seekers get actionable feedback on resumes. Drop a PDF and the app:

- converts the PDF to an image for preview ✅
- uploads files to a file store ✅
- calls an AI service to analyze the resume against a job description ✅
- returns a structured JSON feedback object with an overall score and category-specific tips ✅

This repository is a Vite + React + TypeScript app using Tailwind for styles and Putter.js for file/AI/kv integrations.

---

## ✨ Key Features

- ATS suitability scoring and category breakdown (ATS, Tone & Style, Content, Structure, Skills)
- Visual preview of the uploaded resume (PDF -> PNG conversion)
- Persistent per-resume storage via a key-value store
- Simple, responsive UI with reusable components (Score badges, Resume cards, etc.)

---

## 🧭 How it works

1. User uploads a PDF via the `/upload` page.
2. The app converts the first PDF page to an image (see `app/lib/pdf2img.ts`).
3. Files are uploaded using `puter.fs.upload`.
4. The app calls `puter.ai.chat` (via `usePuterStore().ai.feedback`) with the resume path and a prepared prompt (`prepareInstructions` in `constants/index.ts`).
5. The AI returns a JSON object with scores and tips which is saved in `puter.kv` and rendered on the `/resume/:id` page.

---

## 🧩 Tech Stack

- React 19 + TypeScript
- Vite (dev server & build)
- Tailwind CSS
- React Router (routes built via `react-router` dev tools)
- Zustand (client store)
- pdfjs-dist (PDF → image conversion)
- Putter.js (hosted file storage, AI & KV service integration)

---

## 📁 Important Files

- `app/routes/upload.tsx` — upload form & analysis flow
- `app/lib/pdf2img.ts` — converts the first page of a PDF to PNG
- `app/lib/puter.ts` — wrapper around `window.puter` with helper methods
- `constants/index.ts` — sample data and AI instruction templates
- `app/components/*` — UI components (ResumeCard, ScoreCircle, FileUploader, etc.)

---

## 🧰 Scripts

```bash
npm install            # install dependencies
npm run dev            # start dev server (react-router dev)
npm run build          # build production bundle
npm run start          # serve production build
npm run typecheck      # generate route types and run TypeScript checks
```

> Note: the project uses `react-router`'s build/dev/serve scripts (see `package.json`).

---

## 🛠️ Local Development & Tips

1. Clone the repo and install:

   ```bash
   npm install
   npm run dev
   ```

2. The app expects Putter.js to be available globally. The script is injected in `app/root.tsx`:
   ```html
   <script src="https://js.puter.com/v2/"></script>
   ```
   If Putter isn't loaded, features like upload, AI, and KV will fail.

3. PDF conversion uses `pdfjs-dist` and expects `public/pdf.worker.min.mjs` to exist.

4. Common debug steps:
   - Open the browser console for Putter / AI errors ⚠️
   - Ensure `pdf.worker.min.mjs` loads (network tab)
   - Check the `ai.feedback` responses and ensure they return a JSON string matching the expected format defined in `constants/index.ts`

---

## 🐞 Troubleshooting

- Putter not available: check network / script inclusion and confirm the script is reachable.
- PDF conversion fails: ensure `pdfjs-dist` worker is accessible and the uploaded file is a valid PDF.
- AI returns non-JSON: check `prepareInstructions` and the AI response format in `constants/index.ts`.

---

## 🤝 Contributing

Contributions are welcome! Please open issues or PRs for bug fixes, improvements, and doc updates. Keep changes focused and include tests or manual verification steps where applicable.

---

## 📄 License

MIT — see LICENSE file (or add one if missing).

---

## 💡 Contact

If you have questions, open an issue or contact the maintainers through the repository.

---

Thanks for using InsightCV — built to make resumes smarter and job-ready! 💼✅

