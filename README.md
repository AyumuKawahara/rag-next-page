# RAGにおける下位検索結果の追加取得

論文「Agentic RAGにおける下位検索結果の追加取得の有効性」の補足資料を公開するためのリポジトリです。

論文3.2節および4.1節に対応するプロンプトとJSON Schema、ならびに紙面に収録しなかった実験結果を掲載しています。

## プロンプト

- [3.2.1 従来構成の行動選択](prompts/automaton_policy_answer_search.md)
- [3.2.1 提案構成の行動選択](prompts/automaton_policy_answer_search_next_page.md)
- [3.2.2 回答生成](prompts/answer_generation.md)
- [4.1 反実仮想評価における検索クエリ生成](prompts/search_query_generation.md)

## JSON Schema

- [3.2.2 従来構成の行動選択](schemas/action-selection-baseline.schema.json)
- [3.2.2 提案構成の行動選択](schemas/action-selection-proposed.schema.json)
- [3.2.2 回答生成](schemas/answer-generation.schema.json)
- [4.1 検索クエリ生成](schemas/search-query-generation.schema.json)

## 実験結果

- [4.2 反実仮想評価における行動別の取得成否](results/counterfactual-action-effectiveness.md)
- [4.3 システム全体の評価結果](results/system-performance.md)
- [4.4 システム実行時の行動選択分析](results/visited-action-selection.md)
