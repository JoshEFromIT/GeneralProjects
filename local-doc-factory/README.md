# Local Doc Factory

Local Doc Factory is a starter project for generating enterprise-style Word documentation from local evidence without sending source files, screenshots, or documents to cloud AI services.

The intended pattern is:

```text
Extract -> Structure -> Analyze locally -> Validate -> Render DOCX
```

This project is intentionally small and boring on purpose. The document output should be predictable, while the local model is used as an analyst rather than as a layout engine.

## What this starter includes

- Local-only project layout
- Sample document-plan JSON schema
- Prompt templates for business procedure, code explanation, and screenshot/UI analysis
- A simple Python CLI
- A shell script to bootstrap and run the sample
- A placeholder DOCX renderer that can generate a basic enterprise-style `.docx`
- An Ollama client stub for local model calls

## Model roles

| Role | Suggested local model |
|---|---|
| Business/document writing | Mistral Nemo 12B Instruct or another already-approved local instruct model |
| Code explanation | Mistral Nemo 12B Instruct with method-sized chunks |
| Screenshot/UI explanation | Llama 3.2 Vision 11B |
| UI/browser exploration | Microsoft Fara-7B, optional later |

## Quick start

From the repository root:

```bash
cd local-doc-factory
chmod +x scripts/run_sample.sh
./scripts/run_sample.sh
```

The script creates a virtual environment, installs Python dependencies, and renders a sample document to:

```text
output/docx/sample-enterprise-guide.docx
```

## Local-only operating rule

This starter assumes:

- `http://localhost:11434` for Ollama, if enabled
- local files only
- no hosted LLM APIs
- no external document upload
- deterministic document rendering from structured JSON

## Next steps

1. Replace `input/document_plan.sample.json` with generated content.
2. Add real `.vb`, `.cs`, `.sql`, `.xml`, or `.config` files under `input/code`.
3. Add screenshots under `input/screenshots`.
4. Extend `src/extractors/code_extractor.py` for your legacy VB.NET patterns.
5. Use the prompt files in `prompts/` to generate JSON with your local model.
6. Render the final document with `src/renderers/docx_renderer.py`.
