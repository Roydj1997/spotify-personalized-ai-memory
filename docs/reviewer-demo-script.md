# Reviewer demo script (8–10 minutes)

Use only the synthetic demo profiles. Start the app and confirm the current deployed review link before recording.

## 0. Opening (30 seconds)
“This is a Spotify-themed Personalized AI Memory System pilot. It demonstrates how a governed memory layer can preserve a small number of useful preferences across listening, playlist and podcast journeys. All listener data is synthetic; this is not connected to Spotify accounts.”

## 1. Product experience and continuity (2 minutes)
1. Open the Listening Desk as U0001.
2. Submit the example listening request.
3. Open View request and View source.
4. Explain that the response is grounded in retrieved memory IDs with provenance, confidence, policy and relevance metadata.
5. Show the memory timeline and distinguish explicit preference from a recent episode.

## 2. Capture and extraction (1 minute)
1. Record the supported play/save/follow interaction from the UI.
2. Open the event/operations view and show the intake receipt.
3. Explain idempotency and why raw event text is minimized before queued processing.
4. State that extraction is deterministic/constrained in this pilot, not an unrestricted agent.

## 3. Correction and retrieval (1.5 minutes)
1. Correct the Arijit Singh preference to Shreya Ghoshal.
2. Re-run the same request.
3. Show that the old fact is superseded and the corrected fact is preferred.
4. Explain graph-version checking and cache invalidation.

## 4. Playlist and podcast journeys (1 minute)
1. Switch to the playlist profile and show its relevant request.
2. Switch to U0003 and demonstrate podcast resume at the saved position.
3. Explain that these are separate synthetic subject workspaces.

## 5. User control and privacy (1.5 minutes)
1. Pause memory and submit a request; show the no-memory fallback.
2. Resume, then demonstrate opt-out if the demo state permits.
3. Delete a memory and open its deletion receipt.
4. Explain accurately: graph/vector/cache and operational references are handled by the pilot; backup policy is marked restricted until rotation, but external physical purge is not independently verified.

## 6. Retrieval quality and operations (1 minute)
1. Show the golden evaluation summary and policy panel.
2. Show retrieval trace, latency/fallback and queue/dead-letter view.
3. State that 81/81 golden cases and 19/19 tests are the committed evidence; rerun them before recording and show fresh results.
4. Clarify that the latency benchmark is local and no production load was simulated.

## 7. Architecture and honest limitations (1 minute)
Explain the flow:
event → validation/idempotency → extraction/entity resolution → temporal memory → TF-IDF + catalog-relationship retrieval → policy/reranking → bounded context → response → feedback/correction/deletion.

Be explicit:
- Synthetic data, no Spotify OAuth/API.
- TF-IDF rather than learned neural embeddings.
- Logical graph model rather than dedicated graph DB.
- Deterministic default response; optional constrained Ollama.
- Pilot-level deployment and monitoring, not production SLO proof.

## Recording checklist
- [ ] Use a clean browser profile and test the whole flow before recording.
- [ ] Hide personal tabs, notifications, account details and secrets.
- [ ] Do not show .env, tokens, API keys, or private user data.
- [ ] Record the current UI, not the older walkthrough.
- [ ] Upload to Google Drive, set anyone-with-link viewer access, and test signed out.
