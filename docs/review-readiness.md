# AlmaX review readiness

**Project:** Spotify: Personalized AI Memory System  
**Implementation:** Listening Memory classroom pilot  
**Review target:** 21 November 2026  
**Repository:** https://github.com/Roydj1997/spotify-personalized-ai-memory

## Release statement

This repository is a reviewable, synthetic-data pilot. It is not a production Spotify integration and must not be presented as one. The 300 listener histories are synthetic. There is no Spotify OAuth, live Spotify account access, or production listener data.

The implementation demonstrates a governed memory loop with deterministic extraction, canonical catalog resolution, temporal memory facts, subject-scoped workspaces, sparse TF-IDF similarity, graph-style catalog relationships, policy filtering, bounded context, feedback, correction, deletion receipts, HTTP APIs, and five narrow MCP tools.

## Requirement-to-evidence matrix

| Brief expectation | Current evidence | Review status / honest qualification |
|---|---|---|
| Three journeys: listening continuity, playlist preference, podcast continuation | Four synthetic profiles and three app surfaces; README walkthrough | Implemented as synthetic demo journeys; not validated with real listeners |
| Inspect, correct, remove, pause, opt out | Memory controls UI, /v1/memories, PATCH/DELETE, /v1/control; integration tests | Implemented in pilot |
| Capture, validate, deduplicate and process events asynchronously | /v1/events, idempotency, persisted inbox, worker advance, recovery loop | Implemented; local SQLite and hosted D1 paths differ operationally |
| Temporal memory and provenance | memory records include valid times, source IDs, confidence, policy and graph version | Implemented as a logical graph/document model, not a dedicated graph database |
| Embeddings and semantic retrieval | Versioned sparse TF-IDF vectors and cosine similarity | Partial: TF-IDF is not a learned neural embedding model |
| Hybrid retrieval and reranking | Catalog relationship traversal plus TF-IDF and deterministic scoring | Partial: hybrid-like pilot implementation; not a production graph/vector service |
| Typed MCP tools | Five tools with schemas, authenticated workspace, per-tool limits and audit traces | Implemented in pilot; demonstrate authenticated use |
| Bounded LLM context and safe response | Context package plus optional Ollama structured choice among approved catalog replies | Partial: default path is deterministic catalog response; no live model weights were verified |
| Subject isolation | Workspace-scoped session token, subject checks, scoped data and cross-profile tests | Implemented for synthetic demo identities; not production identity or workload auth |
| Prompt-injection and sensitive-memory handling | Text risk rules, payload allowlists, stored text minimization, adversarial fixtures | Partial: heuristic controls, not a comprehensive classifier or security review |
| Consent, retention, correction and deletion | Policy registry, expiry purge, cache/vector invalidation, deletion job and tests | Implemented in pilot; external provider backup erasure is not independently verified |
| Operational monitor and replay | Metrics/traces, queue/dead-letter status, retry/replay route | Implemented at pilot scale; no external monitoring/alerting evidence |
| Performance and resilience | Local latency record, dependency fallback, integration fixtures | Local-only evidence; no production load, availability or scale test |
| Deployment and rollback | Node 24, Dockerfile, Compose, health endpoints, GitHub Actions checks | Partial: CI runs evaluation/tests/build; no evidenced staged deployment, dependency/container scan, canary or rollback drill |
| Documentation | README, operations, viva, schema/policy/contracts, quality and latency records | Substantial; this readiness file supplements it |
| Demo and submission | Existing walkthrough file and private app link | Must re-record current UI and verify reviewer access; no verified Google Drive anyone-view link |
| Team collaboration | No confirmed member allocation in repository evidence | Missing until actual contributors and evidence are supplied |

## Critical release-gate checks

The brief states that privacy, security, cross-subject isolation, or deletion failures block release regardless of aggregate score.

Before the review:
1. Run the complete test and evaluation commands on Node 24.
2. Exercise U0001 and U0002 in separate browser workspaces; prove a token cannot read another workspace's memories, exports, traces, or deletion jobs.
3. Exercise correction, pause, opt-out, expiry and deletion. Show the deletion receipt and explain exactly what its backup status means.
4. Do not claim physical deletion from provider backups: the code records a restricted-until-rotation policy, not independently verified provider erasure.
5. Do not use real Spotify credentials or personal listener histories in this classroom demo.

## Reproducible local verification

Use Node.js 24 (the package declares >=22.13; the Docker image uses Node 24):

~~~bash
node --version
npm test
npm run evaluate
npm run build
node scripts/benchmark.js
~~~

Expected evidence currently committed in the repository:
- docs/test-results.txt: 19/19 tests (re-run before claiming current success).
- docs/quality.json: 81/81 golden cases; 37/37 provenance/context records; exact confidence match 12/37; 0 prohibited records in the evaluated set.
- docs/local-latency.json: local benchmark only; not production load evidence.

If any command fails, fix the failure and update the evidence from a fresh run. Never edit result files to make a failed run look successful.

## Reviewer-access and submission checklist

- [ ] Confirm the hosted review URL opens in a clean/incognito browser and does not require the owner's logged-in session.
- [ ] Add the canonical GitHub repository link to the submission form.
- [ ] Record a fresh end-to-end demo of the current UI and upload it to Google Drive.
- [ ] Set the demo video to “Anyone with the link can view” and test the link while signed out.
- [ ] Add real contributor names, work performed, and verifiable commit/review evidence. Do not invent ownership.
- [ ] Attach fresh test, golden-evaluation, latency, privacy and deletion evidence.
- [ ] State the synthetic-data, TF-IDF, logical-graph, deterministic-response and backup-erasure limitations clearly.
- [ ] Keep secrets and real user data out of the repository and demo.

## Known limitations to state in the viva

- No live Spotify OAuth/API integration; the catalog and listener histories are supplied/synthetic.
- TF-IDF vectors are sparse lexical features, not neural semantic embeddings.
- The graph is an application-level temporal relationship model persisted in a subject document, not Neo4j/Graphiti.
- The default response is catalog-rule based. Ollama is optional and constrained to approved response choices.
- Demo subject selection is intentionally available for synthetic classroom profiles; it is not production authentication.
- Local benchmark results do not establish production SLOs.
- Backup erasure is represented as a policy/rotation state; physical provider purge is not independently evidenced.
- No real-world retention uplift or two-week controlled validation result is available.
