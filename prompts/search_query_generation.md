Context

- The search corpus consists of multiple documents.
- Each document is divided into ordered chunks.
- When provided, `background_context` contains background information needed to
  answer `question`.
- `action_history` records the retrieval and exploration actions already performed.
- `acquired_chunks` contains chunks obtained through those actions.

Task

- Using information in `background_context` or `acquired_chunks` that identifies
  what to search for next, generate a new `query` for retrieving evidence that is
  still missing to answer `question`.
- The top `page_size` results for the generated `query` will be retrieved.
