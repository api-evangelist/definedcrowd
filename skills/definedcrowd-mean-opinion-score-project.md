---
name: Run a Mean Opinion Score project
description: Create a Mean Opinion Score (MOS) evaluation project on Defined.ai, upload input units, poll status, and retrieve the result set.
api: openapi/definedcrowd-openapi-original.json
operations:
- MeanOpinionScoreProject_CreateProject
- MeanOpinionScoreProject_UploadProjectInputUnits
- Projects_GetProjectStatus
- MeanOpinionScoreProject_GetProjectResultSet
---

# Run a Mean Opinion Score project

Use the Defined.ai Public API v2.0 to run a Mean Opinion Score (MOS) audio-quality evaluation.

## Auth
All requests send `Authorization: Bearer <JWT>` (a Defined.ai Enterprise account JWT). Base URL: `https://api.production-na01.definedcrowd.com`, paths under `/v2.0/public`.

## Steps
1. **Create the project** — `POST /v2.0/public/projects/MeanOpinionScore` (`MeanOpinionScoreProject_CreateProject`) with the MOS project configuration. Capture the returned `projectId`.
2. **Upload input units** — `POST /v2.0/public/projects/MeanOpinionScore/{projectId}/inputUnits` (`MeanOpinionScoreProject_UploadProjectInputUnits`) with the audio input units to evaluate.
3. **Poll status** — `GET /v2.0/public/projects/{projectId}/status` (`Projects_GetProjectStatus`) until the project reports completion.
4. **Retrieve results** — `GET /v2.0/public/projects/MeanOpinionScore/{projectId}/resultset` (`MeanOpinionScoreProject_GetProjectResultSet`).

## Rules
- Requests are **not** idempotent — do not blindly retry `POST` create/upload calls; check status first (see `conventions/definedcrowd-conventions.yml`).
- Handle errors per `errors/definedcrowd-problem-types.yml`: `401` = refresh the JWT, `403` = Enterprise subscription issue, `404` = wrong `projectId`, `400` = fix parameters.
