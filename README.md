# EBOscope

**EBOscope** goes beyond a decontextualized claim such as **“X is biased.”**

A visitor enters a named artefact, process, map/projection, dataset/model, document, or public work. The application searches the web for readable sources, uses **Mistral** to reconstruct source-documented epistemic-bias assessments, and exposes the reasoning through an **EBO-oriented** structure.

> EBOscope is **not** a bias detector and does not output a global “biased / unbiased” verdict.

## Public workflow

1. **Search** — retrieve readable web sources about documented criticisms, limitations, uses and responses.
2. **Reconstruct** — identify candidate target, assessor, purpose, criterion, indicator, evidence, grounds and qualification.
3. **Inspect** — explore each candidate as a human-readable record and an interactive EBO graph.
4. **Reuse** — export a provisional JSON-LD representation.

The web interface never asks visitors for API keys.

## Architecture

- **Frontend:** plain HTML/CSS/JavaScript in `web/index.html`
- **Backend:** FastAPI in `app.py`
- **Search:** Tavily Search API
- **LLM:** Mistral API, default model `mistral-small-latest`
- **Ontology:** provisional EBO application profile; `ontology/adapter.json` is an explicit placeholder until the authoritative EBO OWL is available
- **Hosting:** Render Blueprint via `render.yaml`

## Deploy

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/minhdavideragagni/EBOscope)

During deployment, configure these **server-side secrets**:

- `MISTRAL_API_KEY`
- `TAVILY_API_KEY`

Do **not** commit either key to GitHub.

Mistral Studio currently supports Free mode with usage/rate limits. Tavily also provides a free developer allowance; provider quotas can change, so check the current provider dashboards before public testing.

After deployment, visit:

- `/` — public EBOscope interface
- `/api/health` — confirms whether the two server-side providers are configured

## Epistemic safeguards

EBOscope deliberately distinguishes:

- a technical phenomenon from an epistemic-bias qualification;
- the webpage author from the assessor reported by the source;
- a bias category from an epistemic criterion;
- a finding about a particular version/use/subset from a global judgement about the searched entity;
- source-explicit information from an EBO-oriented interpretive mapping.

If a source does not support a field, the application should leave it absent rather than invent it.

## EBO status

The authoritative OWL version of EBO is **not yet connected**. The current prototype uses provisional role labels based on the documented conceptual model. This is declared in `ontology/adapter.json`.

When the authoritative ontology is released, the adapter can be replaced and the exported graph validated against the real EBO IRIs and axioms.

## Repository

Research prototype for investigating explainable, source-grounded and machine-readable epistemic-bias qualifications.
