# university-ai-knowledge-base

A template for building a personalized AI-powered knowledge base tailored to your university degree. Fork it, point it at your course PDFs, and let the included AI agents bootstrap a structured, indexed, searchable study companion — slides, exercises, past exams, and a per-subject tutor agent ready to answer questions in Greek or English.

This template is **IDE-agnostic**: agent definitions are plain Markdown files with YAML frontmatter. They work in Cursor, Claude Code, GitHub Copilot Chat, ChatGPT custom GPTs, and any other AI coding assistant that lets you load a system prompt or custom instructions.

---

## What you get

- A standardised folder layout for any number of subjects.
- A pipeline that takes raw PDFs and produces:
  - Markdown copies of every PDF with faithful text extraction.
  - Extracted images saved per-PDF and referenced from the Markdown.
  - A curated `assets/` folder where decorative images (logos, portraits, banners) are stripped out.
  - A per-subject **tutor agent** that knows the material, the file structure, and when to open which image. When you ask it to save a study document, it writes the file to that subject's `out/` folder.
- A small set of cross-platform Python scripts (`tools/`) that do the mechanical work.
- A set of agents (`agents/`) that do the intelligent work (curation, formatting review, tutor authoring).

---

## Quick start

1. **Clone or fork** this repository.
2. **Install Python dependencies** (Python 3.10+ recommended):

   ```bash
   python -m venv .venv
   source .venv/bin/activate           # on Windows: .venv\Scripts\activate
   pip install -r requirements.txt
   ```

3. **Wire the agents into your AI assistant.** See [`docs/ide-integration.md`](docs/ide-integration.md) for Cursor, Claude Code, Copilot, and generic instructions.
4. **Invoke the initializer agent** in your assistant and tell it:
   - the subject name (e.g. *Algorithms*),
   - the list of PDFs you want to ingest,
   - which category each PDF belongs to (`slides`, `exams`, or `general`).

   The initializer will create `subjects/<your-subject>/`, place raw PDFs, convert them to Markdown with images, curate the assets, format the output, and finally generate a tutor agent in `subjects/<your-subject>/agents/`.

5. **Talk to the tutor agent** for that subject. Ask in Greek or English — it answers in whichever language you used last. Ask it to save a study document and the file lands in `subjects/<your-subject>/out/`.

---

## Folder layout

```
.
├── agents/                    # root-level agents: the pipeline
│   ├── kb-initializer.md
│   ├── image-curator.md
│   ├── md-formatter.md
│   └── tutor-generator.md
├── tools/                     # cross-platform Python scripts
│   ├── pdf_to_md.py
│   ├── format_md.py
│   ├── filter_images.py
│   ├── init_subject.py
│   └── regenerate.py
├── templates/                 # skeletons used when creating a new subject
│   ├── subject/               # folder layout copied for each new subject
│   └── tutor-agent.md         # template for the per-subject tutor agent
├── subjects/                  # one folder per subject (populated by the initializer)
│   └── <subject>/
│       ├── agents/            # subject-specific agents (tutor lives here)
│       ├── assets/            # one subfolder per PDF, holds extracted images
│       ├── kb/                # markdown knowledge base, mirrors raw/ layout
│       │   ├── general/
│       │   ├── slides/
│       │   └── exams/
│       ├── out/               # study artifacts the tutor writes on request
│       └── raw/               # original PDFs, same category layout as kb/
│           ├── general/
│           ├── slides/
│           └── exams/
└── docs/                      # how the pipeline works, IDE wiring, workflow
```

---

## Documentation

- [`docs/architecture.md`](docs/architecture.md) — pipeline, agent responsibilities, data flow.
- [`docs/ide-integration.md`](docs/ide-integration.md) — how to load the agents in Cursor / Claude Code / Copilot / generic chat.
- [`docs/workflow.md`](docs/workflow.md) — end-to-end walkthrough of adding a new subject.

---

## Language

Source material can be in Greek, English, or any mix. The tutor agent detects the user's language and replies in kind, while keeping Greek terminology in quotes when relevant.

---

## License

See [`LICENSE`](LICENSE).
