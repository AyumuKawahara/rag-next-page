# RAGにおける下位検索結果の追加取得

論文「Agentic RAGにおける下位検索結果の追加取得の有効性」の補足資料を公開するためのリポジトリです。

論文4.5節に対応するプロンプトとJSON Schema、および紙面に収録しなかった実験結果を掲載しています。

## プロンプト

- [従来構成の行動選択](prompts/automaton_policy_answer_search.md)
- [提案構成の行動選択](prompts/automaton_policy_answer_search_next_page.md)
- [反実仮想評価における検索クエリ生成](prompts/search_query_generation.md)
- [回答生成](prompts/answer_generation.md)

## JSON Schema

- [従来構成の行動選択](schemas/action-selection-baseline.schema.json)
- [提案構成の行動選択](schemas/action-selection-proposed.schema.json)
- [検索クエリ生成](schemas/search-query-generation.schema.json)
- [回答生成](schemas/answer-generation.schema.json)

## 実験結果

- [反実仮想評価における行動別の取得成否](results/counterfactual-action-effectiveness.md)
- [システム全体の評価結果](results/system-performance.md)
