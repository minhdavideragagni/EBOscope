# EBOscope

**EBOscope** is an application based on the **Epistemic Bias Ontology (EBO)**.

It turns documented bias claims into **contextualised, source-grounded EBO qualifications** by reconstructing who assessed what, according to which criterion, using what evidence, and for what purpose.

> EBOscope is **not** a bias detector. It does not output a global “biased / unbiased” verdict.

## EBOscope v2

The v2 prototype introduces:

- recall-enhanced retrieval restricted to explicit **bias / biased** language;
- support for sources available only as search-result snippets;
- three result statuses:
  - **EBO qualification**
  - **Bias claim**
  - **Bias-related context**
- field-level grounding for target, assessor, purpose, method, criterion, indicator, evidence, grounds, qualification and category;
- explicit **Source-explicit / EBOscope interpretation / Not documented** provenance;
- source metadata including year, source type and retrieval level;
- explicit source ↔ assessment correspondence;
- an interactive EBO graph with:
  - draft model view,
  - qualification-instance view,
  - combined TBox/ABox view;
- an **EBO Passport**, a portable application-level record of one reconstructed qualification;
- in-browser JSON-LD preview, copy and download;
- a draft EBO conceptual model in `ontology/draft.json`.

## Retrieval policy

EBOscope currently searches only for explicit bias terminology. To improve coverage without broadening the semantics to unrelated criticism, it tries multiple formulations:

- `"entity" "biased"`
- `"entity" bias`
- `entity biased`
- `entity bias`

The system does **not** expand retrieval to terms such as *misrepresents*, *distorts*, *skewed*, or *underrepresents*.

A retrieved source can yield zero qualifications. This may happen when:

- the page discusses bias but does not formulate an identifiable assessment;
- the retrieved portion does not document enough of the assessment;
- only a snippet is available;
- the reconstruction cannot be grounded in verified source excerpts.

A missing qualification is never treated as evidence that the target is unbiased.

## Architecture

- **Frontend:** HTML/CSS/JavaScript in `web/index.html`
- **Backend:** FastAPI in `app.py`
- **Web retrieval:** Tavily Search API
- **LLM reconstruction:** Groq API, default model `openai/gpt-oss-120b`
- **Draft ontology model:** `ontology/draft.json`
- **Hosting:** Render Blueprint via `render.yaml`

Visitors never enter API keys.

## Server-side secrets

- `GROQ_API_KEY`
- `TAVILY_API_KEY`

Do **not** commit real keys to GitHub.

## EBO Passport

The **EBO Passport** is an EBOscope application artefact, **not an EBO ontology class**.

It packages one reconstructed assessment with:

- EBO-oriented entities and relations;
- source metadata;
- reconstruction status;
- per-field provenance;
- Web Annotation-style text-quote grounding;
- draft JSON-LD.

Once the authoritative EBO OWL is available, the draft namespace can be replaced with the real EBO IRIs and the export can be validated against the final ontology.

## EBO status

The authoritative EBO OWL is not yet released.

The v2 application therefore uses the supplied **draft conceptual model**, including:

- `ebo:BiasAssessmentActivity`
- `ebo:EpistemicBiasQualification`
- `ebo:EpistemicCriterion`
- `ebo:BiasIndicator`
- `ebo:EpistemicBiasCategory`
- `ebo:BiasAcknowledgement`
- `ebo:BiasMitigationActivity`
- `ebo:BiasPropagation`
- Cognitive Perspectivisation integration;
- Web Annotation grounding;
- provenance, acknowledgement, impact and propagation relations.

See `ontology/draft.json` for the current conceptual representation.

## Validation

A GitHub Actions workflow checks:

- Python syntax;
- frontend JavaScript syntax;
- draft EBO JSON validity.
