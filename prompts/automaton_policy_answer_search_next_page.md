Context

- The search corpus consists of multiple documents.
- Each document is divided into ordered chunks.
- When provided, `background_context` contains background information needed to
  answer `question`.
- Before the first decision, `question` is used as the initial search `query`.
  This is recorded in `action_history` with `action` set to `initial_search`, and
  the returned chunks are included in `acquired_chunks`.
- `action_history` records the retrieval and exploration actions already performed.
  Each action contains `results` with the returned `chunk_id` and, when
  applicable, its `result_rank` for the search `query` in `parameters`.
- `acquired_chunks` contains chunks obtained through those actions.

Goal

- Based on `background_context` and `acquired_chunks`, select the next `action`
  to collect all evidence required to answer `question`.

Available actions

- `search`: Select this when `background_context` or `acquired_chunks` contains
  concrete information that identifies what to search for next, but evidence
  required to answer `question` is still missing. Specify a new `query` that uses
  that information to retrieve the missing evidence. It retrieves the top
  `page_size` results for the new `query`.
- `next_page`: Select this when none of the chunks in `acquired_chunks` contains
  evidence that contributes to answering `question`, and `background_context`
  and `acquired_chunks` provide no concrete clue for a new `query`. It reuses the
  most recent `query` in `action_history` and retrieves the next `page_size`
  ranked results.
- `answer`: Select this when `background_context` and `acquired_chunks` together
  contain all evidence required to answer `question`.
