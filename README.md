# EBOscope

**EBOscope** goes beyond a decontextualized claim such as **“X is biased.”**

A visitor enters a named artefact, process, map/projection, dataset/model, document, or public work. EBOscope first searches for sources that **explicitly use or report bias language** about that target. It then reconstructs the documented reasoning behind each claim through an EBO-oriented structure.

> EBOscope is **not** a bias detector and does not output a global “biased / unbiased” verdict.

## Retrieval logic: bias-claim first

The prototype deliberately starts from explicit claims rather than from generic technical limitations.

1. Search for the named target together with **“biased”**.
2. If needed, broaden to the term **“bias”**.
3. Keep only retrieved source text that actually contains explicit bias language.
4. Read multiple portions of each source, especially the passages around the bias claim.
5. Reconstruct the qualification from different parts of **that same source** where the source supports it.

A technical limitation alone is not automatically converted into an epistemic-bias qualification.

## What is reconstructed

For each documented claim, EBOscope can expose:

- assessed **target** and its scope;
- reported **assessor**;
- relevant **purpose/context**;
- epistemic **criterion**;
- **indicator**;
- reported **evidence**;
- supporting **grounds**;
- resulting **qualification**;
- optional **bias category**.

If the source merely says “biased” without enough reasoning, the result remains a **bare claim** rather than being completed by the model.

## Architecture

- **Frontend:** HTML/CSS/JavaScript in `web/index.html`
- **Backend:** FastAPI in `app.py`
- **Web retrieval:** Tavily Search API
- **LLM reconstruction:** Groq API, default model `openai/gpt-oss-120b`
- **Ontology:** provisional EBO application profile
- **Hosting:** Render Blueprint via `render.yaml`

Visitors never enter API keys.

## Deployment

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/minhdavideragagni/EBOscope)

Configure these server-side secrets in Render:

- `GROQ_API_KEY`
- `TAVILY_API_KEY`

Do **not** commit real keys to GitHub.

After deployment:

- `/` — public EBOscope interface
- `/api/health` — provider configuration status

## Epistemic safeguards

EBOscope distinguishes:

- an observable/technical phenomenon from an epistemic-bias qualification;
- the reporting source from the assessor it reports;
- a bias category from an epistemic criterion;
- a claim about a particular version/use/subset from a global judgement;
- source-explicit information from an EBO-oriented interpretation.

Exact source quotations are returned only when they can be matched back to the retrieved source text.

## EBO status

The authoritative EBO OWL is **not yet connected**. `ontology/adapter.json` remains an explicit placeholder. Once the ontology is released, the provisional terms and JSON-LD export can be aligned to the real EBO IRIs and axioms.
