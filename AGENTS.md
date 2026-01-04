# Repository Guidelines

## Project Structure & Responsibilities
- `main.py`: Streamlit UI for PDF upload, DeepSeek API key entry, and chat history display.
- `utils.py`: QA pipeline built with LangChain `ConversationalRetrievalChain`, FAISS vector store, and HuggingFace BGE-M3 embeddings (local path currently hard-coded).
- `requirements.txt`: Pinned dependencies for the Streamlit + LLM stack; install inside a virtual environment.
- Runtime files: uploads are saved temporarily as `temp.pdf` during requests.

## Setup, Build & Run
- Python 3.10+ recommended. Create a virtualenv and install dependencies:
```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```
- Ensure the BGE-M3 model is available locally and update the `model_name` path in `utils.py` if needed.
- Start the app locally:
```bash
streamlit run main.py
```

## Coding Style & Naming Conventions
- Follow PEP 8; use 4-space indentation; order imports stdlib > third-party > local.
- Use `snake_case` for functions/variables, `PascalCase` for classes, and `UPPER_SNAKE_CASE` for constants.
- Keep UI labels consistent (current UI is in Chinese). Prefer short docstrings for public functions and clarify why non-default parameters are chosen.

## Testing Guidelines
- No automated tests yet; add `tests/test_*.py` with `pytest` when introducing new logic. Example run:
```bash
pytest
```
- Manually verify: `streamlit run main.py`, upload a sample PDF, ask a question, and confirm the answer plus chat history render correctly.
- Smoke-check that the local embedding model path resolves and that no API keys or sensitive text are logged.

## Commit & Pull Request Guidelines
- Use concise commit messages in present tense; history currently favors short summaries (e.g., "第一个版本，测试", "Initial commit").
- Include PR details: what changed, why, manual test steps/output, and screenshots or screen recordings for UI changes. Link to related issues/tasks.
- Note dependencies or configuration expectations (DeepSeek API key, local BGE model path) in the PR description.

## Security & Configuration
- Do not commit real API keys or local model paths; rely on environment variables or a git-ignored `.env`, and keep placeholders in code.
- Remove hard-coded secrets before pushing; if data is sensitive, scrub `temp.pdf` outputs and avoid storing uploads beyond request handling.
