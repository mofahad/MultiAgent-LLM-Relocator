# Local repair status

The checked-in backend is a notebook with LLM-based routing and two retrieval paths: housing and crime records. It is a forked hackathon prototype, not evidence of five independently implemented agents or measured workflow improvements.

The supported lightweight backend loads the supplied 1,000-row housing CSV and returns retrieved records on CPU. Real-data loading and chat smoke checks pass. Seven backend tests, three frontend behavior tests, and the frontend production build pass. These are functionality checks, not retrieval-quality benchmarks. Optional local-model generation is tested with stubs; an actual model has not been executed.

## Repairs prepared

- Separated housing and crime text stores, embedders, and FAISS indices; the original shared globals overwrote housing retrieval state.
- Fixed the chat endpoint's reference to `answer` before assignment.
- Added request validation and request-local conversation state.
- Replaced the expired frontend tunnel with a configurable localhost URL.
- Guarded invalid FAISS result indices and avoided moving an already quantized model.
- Disabled Flask debug mode and cleared saved notebook outputs.

## Reproduction blockers

The housing dataset is now available outside the repository. The supplied crime ZIP remains unreadable through the linked-phone filesystem and must be copied to a local folder. The original notebook requires the processed crime CSV, whose schema and provenance still need inspection. No fabricated replacement data is presented as the original dataset.

The original quantized Zephyr-7B path requires compatible hardware and downloaded weights. Original model routing, GPU execution, and response correctness remain unvalidated. The model's regex-based routing is fragile and needs a structured-output test suite. Claims about a city's safety require appropriate denominators and evidence; current prompt-generated examples are not validated statistics.

## Frontend

In `React`, run `npm ci` and `npm start`. The default API URL is `http://127.0.0.1:5004`; `.env.example` documents the override. Start `backend.py` using the root README's environment configuration. Requests currently use single-turn state.

The existing dependency lockfile's npm audit reported 103 findings (6 low, 15 moderate, 78 high, 4 critical). Dependency upgrades need separate validation before public deployment; no force upgrade was applied.

Preserve the fork relationship and upstream contributor credit when presenting this project. Separate original hackathon contributions from these later repairs.
