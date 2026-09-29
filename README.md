# EBOscope

**EBOscope** explores how claims that an identifiable artefact or process is epistemically biased are documented online, and reconstructs the reasoning behind those claims using an EBO-oriented semantic profile.

This repository hosts the public web prototype.

## Core idea

EBOscope does **not** answer “is X biased?” with a global verdict. It searches for documented assessments and reconstructs, where the sources support it:

- the assessed target;
- the responsible assessor or attributed agent;
- the assessment purpose/context;
- the epistemic criterion;
- relevant indicators and evidence;
- the resulting epistemic-bias qualification;
- optional bias category and perspective;
- what remains undocumented or interpretive.

The current EBO mapping is provisional until the authoritative OWL version is available.

## Deployment

The project is configured for Render via `render.yaml`. Server-side environment variables are required:

- `MISTRAL_API_KEY`
- `TAVILY_API_KEY`

Visitors never enter API keys.

