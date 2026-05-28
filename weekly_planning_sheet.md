# Savitribai Phule Pune University
## RMD SINHGAD SCHOOL OF ENGINEERING
### Department of Information Technology
#### Academic Year: 2025-26 | Semester – II
#### Weekly Planning Sheet

**Project Title:** HirePrepAI — AI-Powered Resume Skill Gap Analyzer & Learning Roadmap Generator

---

*Continuation from Semester I: In Sem I, we built and tested TF-IDF, Random Forest, and a BERT NER pipeline. While the final Sem I system could extract skills, it lacked semantic matching accuracy and had no roadmap generation. Semester II focuses on rebuilding the core with transformer embeddings, a JD skill predictor, and an LLM-powered roadmap generator.*

---

| Week No. | Activity Planned | Activity Completed Status | Student Signature | Guide Signature |
|----------|-----------------|--------------------------|-------------------|-----------------|
| **Week 1** | **System redesign & literature review.** Reviewed Sem I limitations (BERT NER was noisy, no roadmap feature). Decided to rebuild skill extraction using MiniLM sentence transformers. Researched FastAPI for backend, Ollama for local LLM. Finalized new architecture: PDF → MiniLM → DistilBERT → BAAI/bge → Ollama. Frontend in plain HTML/CSS/JS. | Architecture finalized. Tech stack confirmed. | | |
| **Week 2** | **FastAPI backend setup & PDF parsing.** Created new project. Set up FastAPI with CORS. Integrated PyMuPDF for PDF text extraction. Wrote `skill_extractor.py` using MiniLM to extract skills from resume text. Parallel: Frontend HTML skeleton started — upload form and layout. | FastAPI server running. PDF skill extraction working. Frontend form structure ready. | | |
| **Week 3** | **JD skill prediction model.** Trained DistilBERT multi-label classifier (`predict_skill.py`) to predict required skills from job title. Saved `mlb.pkl`. Challenge: model ran very slow on CPU. Fixed by forcing CUDA GPU in all model loaders. Parallel: Frontend — styled upload area, tabbed input (Job Title / Paste JD). | DistilBERT JD predictor working on GPU. Frontend input tabs styled. | | |
| **Week 4** | **Semantic gap scoring.** Built `gap_scorer.py` using BAAI/bge embeddings to semantically match resume skills vs JD skills. Computed match score (0–100%). Handled fuzzy matches (e.g. "aws ec2" → "aws", "html5" → "html"). Parallel: Frontend — results panel layout, skill badge components, match score gauge. | Semantic gap scoring working. Frontend results panel skeleton ready. | | |
| **Week 5** | **Ollama + Mistral integration for roadmap.** Installed Ollama locally. Pulled Mistral model. Wrote `ollama_roadmap.py` with prompt builder and non-streaming generator. Tested 4-week roadmap output. Challenge: Mistral model was ~4 GB, very heavy on storage and slow on first load. Flagged for replacement. | Roadmap generation working but Mistral too heavy. Replacement planned. | | |
| **Week 6** | **LLM migration: Mistral → Llama 3.2.** Pulled `llama3.2` via Ollama. Updated `MODEL_NAME` constant in `ollama_roadmap.py`. Llama 3.2 was significantly lighter and faster. Validated roadmap quality — output was comparable or better. Added streaming generator function. Parallel: Frontend — integrated match score color coding (red/yellow/green), missing skills badges. | LLM migrated to llama3.2. Frontend results panel complete. | | |
| **Week 7** | **Full pipeline integration.** Combined all modules into `pipeline.py`. Built `run_pipeline()` for batch mode and `run_pipeline_stream()` for SSE streaming. Tested end-to-end with real resumes and multiple job titles. Fixed edge cases: empty skills list, name extraction from resume header. | Full pipeline integrated and tested. | | |
| **Week 8** | **FastAPI endpoint & SSE streaming.** Exposed `POST /analyze` and `GET /health` endpoints in `main.py`. Implemented Server-Sent Events (SSE) for token-by-token roadmap streaming. Structured two event types: `type: result` (skills/scores) and `type: roadmap_token`. Parallel: Frontend — connected `fetch` SSE handler to stream roadmap with typing effect. | `/analyze` and `/health` live. SSE streaming working in browser. | | |
| **Week 9** | **Frontend integration & UX polish.** Added health check on page load with AI server status badge. Built animated loading steps ("Parsing Resume → Extracting Skills → Analyzing Gap → Generating Roadmap"). Rendered streamed roadmap markdown in browser. Added copy-to-clipboard button. | Full frontend-backend integration complete. Loading states and streaming UI working. | | |
| **Week 10** | **Testing & bug fixing.** Tested with multiple resumes and job titles. Fixed: non-PDF file rejection (HTTP 415), missing job_title and jd_text validation (HTTP 422), frontend file-type check. Verified GPU startup report printed correctly. Verified semantic matching accuracy (e.g. "mysql" → "sql" at 0.826 score). | All validation and edge cases fixed. Accuracy verified. | | |
| **Week 11** | **Documentation.** Wrote complete API integration guide (`hireprep_frontend_guide.md`) covering health check, form fields, SSE event format, error codes, UI/UX recommendations, and a real live output sample. Drafted project report: introduction, system design, implementation, results chapters. | Documentation complete. Project report drafted. | | |
| **Week 12** | **Final testing, demo preparation & submission.** Ran full end-to-end demo with real resume (Ashutosh Waghire) against "Full Stack Developer" job — got 45% match score with 9/20 skills matched and streamed roadmap. Cleaned codebase. Prepared presentation. Submitted report and source code. | Demo successful. Project submitted. | | |

---

*Project Coordinator Signature: ___________________*  
*Internal Guide Signature: ___________________*
