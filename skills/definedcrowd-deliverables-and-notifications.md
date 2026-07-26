---
name: Retrieve deliverables and manage notifications
description: List Defined.ai projects, check status, download deliverables, and subscribe to project notifications.
api: openapi/definedcrowd-openapi-original.json
operations:
- Projects_GetProjects
- Projects_GetProjectStatus
- ProjectsDeliverables_GetDeliverables
- ProjectsDeliverables_GetDeliverablesDownload
- Subscriptions_SubmitSubscriptions
---

# Retrieve deliverables and manage notifications

Track a Defined.ai project to completion, download its outputs, and subscribe to email notifications.

## Auth
Send `Authorization: Bearer <JWT>`. Base URL `https://api.production-na01.definedcrowd.com`, paths under `/v2.0/public`.

## Steps
1. **List projects** — `GET /v2.0/public/projects` (`Projects_GetProjects`). Paginate with `pageNumber` + `itemsPerPage`; sort with `sortBy` + `sortDirection`.
2. **Check status** — `GET /v2.0/public/projects/{projectId}/status` (`Projects_GetProjectStatus`).
3. **Subscribe to notifications** — `PUT /v2.0/public/projects/{projectId}/subscriptions` (`Subscriptions_SubmitSubscriptions`) to be emailed on `DeliverablePublished` / `DataUploadCompleted`. You must set `emailListConsent: true` and confirm recipient consent.
4. **List deliverables** — `GET /v2.0/public/projects/{projectId}/deliverables` (`ProjectsDeliverables_GetDeliverables`); capture each `deliverableId`.
5. **Download** — `GET /v2.0/public/projects/{projectId}/deliverables/{deliverableId}/download` (`ProjectsDeliverables_GetDeliverablesDownload`).

## Rules
- Pagination is page-number based (see `conventions/definedcrowd-conventions.yml`).
- Handle errors per `errors/definedcrowd-problem-types.yml` (`401`/`403`/`404`/`400`).
