# 4.4 システム実行時の行動選択分析

論文4.4節に対応する集計結果です。論文では紙面の都合から `k=3` の結果のみを示し、ここでは補足として `k=2, 5` の結果を掲載します。

提案構成を実行した際に実際に訪れた探索状態を対象としています。各状態から残りの探索予算内で到達できるSupport Recallを行動ごとに計算し、最大値を達成する行動を最良行動としました。同率の場合は回答生成までの追加探索回数が少ない行動を優先し、それでも同率の行動は最良行動集合として扱っています。

- データセット: IIRC 559問、MuSiQue-Ans 2,417問
- 追加探索行動の上限: 2回
- 再検索クエリ生成モデル: Qwen3.5-4B
- 9Bおよび27Bの分析も、Qwen3.5-4Bが生成した再検索クエリを仮定した根拠取得上の評価
- `next_page` のPrecision、RecallおよびF1は、同行動が根拠取得上の最良行動集合に含まれるかを正解ラベルとして算出
- 形式不正は状態数に含め、反実仮想最良行動との一致率では不一致として集計

## 行動選択性能

| データセット | k | 行動選択モデル | 状態数 | 反実仮想最良行動との一致率 | `next_page` Precision | `next_page` Recall | `next_page` F1 |
|---|---:|---:|---:|---:|---:|---:|---:|
| IIRC | 2 | 4B | 854 | 47.89% | 15.34% | 22.52% | 18.25% |
|  |  | 9B | 808 | 55.45% | 0.00% | 0.00% | 0.00% |
|  |  | 27B | 939 | 54.53% | 0.00% | 0.00% | 0.00% |
|  | 3 | 4B | 846 | 52.84% | 15.91% | 18.75% | 17.21% |
|  |  | 9B | 791 | 56.13% | 0.00% | 0.00% | 0.00% |
|  |  | 27B | 904 | 59.73% | 0.00% | 0.00% | 0.00% |
|  | 5 | 4B | 837 | 56.99% | 11.11% | 7.50% | 8.96% |
|  |  | 9B | 788 | 57.36% | 0.00% | 0.00% | 0.00% |
|  |  | 27B | 856 | 64.02% | 0.00% | 0.00% | 0.00% |
| MuSiQue-Ans | 2 | 4B | 3,937 | 47.90% | 46.94% | 26.26% | 33.68% |
|  |  | 9B | 3,852 | 49.74% | 0.00% | 0.00% | 0.00% |
|  |  | 27B | 4,344 | 52.51% | 50.00% | 0.13% | 0.27% |
|  | 3 | 4B | 4,017 | 51.38% | 45.52% | 25.05% | 32.32% |
|  |  | 9B | 3,700 | 51.41% | 0.00% | 0.00% | 0.00% |
|  |  | 27B | 4,211 | 56.02% | 50.00% | 0.28% | 0.57% |
|  | 5 | 4B | 4,013 | 51.96% | 44.03% | 15.81% | 23.27% |
|  |  | 9B | 3,499 | 53.93% | 0.00% | 0.00% | 0.00% |
|  |  | 27B | 4,110 | 57.47% | 66.67% | 0.14% | 0.29% |

## 根拠取得上の最良行動集合とLLMの選択

各表では、上段の列見出しが反実仮想評価で求めた「根拠取得上の最良行動集合」、左側の行見出しが「LLMの選択」を表します。LLMの選択が最良行動集合に含まれるセルを太字で示します。`再検索・追加取得`列では、再検索と下位検索結果の追加取得が同率で最良です。
`k=3`の詳細表は論文本文に掲載しているため、ここでは紙面に収録しなかった`k=2,5`を示します。

### k=2

#### IIRC

<table>
  <thead>
    <tr>
      <th rowspan="2">選択モデル</th>
      <th rowspan="2">LLMの選択</th>
      <th colspan="4">根拠取得上の最良行動集合</th>
    </tr>
    <tr>
      <th>回答</th>
      <th>再検索</th>
      <th>追加取得</th>
      <th>再検索・追加取得</th>
    </tr>
  </thead>
  <tbody>
    <tr><td rowspan="3">4B</td><td>回答</td><td><strong>277</strong></td><td>125</td><td>37</td><td>18</td></tr>
    <tr><td>再検索</td><td>107</td><td><strong>96</strong></td><td>20</td><td><strong>11</strong></td></tr>
    <tr><td>追加取得</td><td>73</td><td>65</td><td><strong>10</strong></td><td><strong>15</strong></td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="4">9B</td><td>回答</td><td><strong>290</strong></td><td>114</td><td>40</td><td>27</td></tr>
    <tr><td>再検索</td><td>148</td><td><strong>133</strong></td><td>29</td><td><strong>25</strong></td></tr>
    <tr><td>追加取得</td><td>0</td><td>0</td><td><strong>0</strong></td><td><strong>0</strong></td></tr>
    <tr><td>形式不正</td><td>1</td><td>0</td><td>1</td><td>0</td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="3">27B</td><td>回答</td><td><strong>264</strong></td><td>63</td><td>20</td><td>10</td></tr>
    <tr><td>再検索</td><td>262</td><td><strong>197</strong></td><td>70</td><td><strong>51</strong></td></tr>
    <tr><td>追加取得</td><td>1</td><td>1</td><td><strong>0</strong></td><td><strong>0</strong></td></tr>
  </tbody>
</table>

#### MuSiQue-Ans

<table>
  <thead>
    <tr>
      <th rowspan="2">選択モデル</th>
      <th rowspan="2">LLMの選択</th>
      <th colspan="4">根拠取得上の最良行動集合</th>
    </tr>
    <tr>
      <th>回答</th>
      <th>再検索</th>
      <th>追加取得</th>
      <th>再検索・追加取得</th>
    </tr>
  </thead>
  <tbody>
    <tr><td rowspan="3">4B</td><td>回答</td><td><strong>722</strong></td><td>333</td><td>262</td><td>208</td></tr>
    <tr><td>再検索</td><td>454</td><td><strong>497</strong></td><td>352</td><td><strong>276</strong></td></tr>
    <tr><td>追加取得</td><td>171</td><td>271</td><td><strong>256</strong></td><td><strong>135</strong></td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="4">9B</td><td>回答</td><td><strong>835</strong></td><td>369</td><td>305</td><td>218</td></tr>
    <tr><td>再検索</td><td>493</td><td><strong>705</strong></td><td>549</td><td><strong>376</strong></td></tr>
    <tr><td>追加取得</td><td>0</td><td>0</td><td><strong>0</strong></td><td><strong>0</strong></td></tr>
    <tr><td>形式不正</td><td>2</td><td>0</td><td>0</td><td>0</td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="3">27B</td><td>回答</td><td><strong>765</strong></td><td>128</td><td>125</td><td>99</td></tr>
    <tr><td>再検索</td><td>952</td><td><strong>1,015</strong></td><td>757</td><td><strong>499</strong></td></tr>
    <tr><td>追加取得</td><td>2</td><td>0</td><td><strong>1</strong></td><td><strong>1</strong></td></tr>
  </tbody>
</table>

### k=5

#### IIRC

<table>
  <thead>
    <tr>
      <th rowspan="2">選択モデル</th>
      <th rowspan="2">LLMの選択</th>
      <th colspan="4">根拠取得上の最良行動集合</th>
    </tr>
    <tr>
      <th>回答</th>
      <th>再検索</th>
      <th>追加取得</th>
      <th>再検索・追加取得</th>
    </tr>
  </thead>
  <tbody>
    <tr><td rowspan="4">4B</td><td>回答</td><td><strong>304</strong></td><td>129</td><td>20</td><td>21</td></tr>
    <tr><td>再検索</td><td>115</td><td><strong>152</strong></td><td>18</td><td><strong>15</strong></td></tr>
    <tr><td>追加取得</td><td>20</td><td>28</td><td><strong>3</strong></td><td><strong>3</strong></td></tr>
    <tr><td>形式不正</td><td>6</td><td>3</td><td>0</td><td>0</td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="4">9B</td><td>回答</td><td><strong>278</strong></td><td>143</td><td>21</td><td>20</td></tr>
    <tr><td>再検索</td><td>125</td><td><strong>155</strong></td><td>20</td><td><strong>19</strong></td></tr>
    <tr><td>追加取得</td><td>0</td><td>0</td><td><strong>0</strong></td><td><strong>0</strong></td></tr>
    <tr><td>形式不正</td><td>7</td><td>0</td><td>0</td><td>0</td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="4">27B</td><td>回答</td><td><strong>340</strong></td><td>107</td><td>32</td><td>19</td></tr>
    <tr><td>再検索</td><td>121</td><td><strong>184</strong></td><td>22</td><td><strong>24</strong></td></tr>
    <tr><td>追加取得</td><td>1</td><td>1</td><td><strong>0</strong></td><td><strong>0</strong></td></tr>
    <tr><td>形式不正</td><td>4</td><td>0</td><td>1</td><td>0</td></tr>
  </tbody>
</table>

#### MuSiQue-Ans

<table>
  <thead>
    <tr>
      <th rowspan="2">選択モデル</th>
      <th rowspan="2">LLMの選択</th>
      <th colspan="4">根拠取得上の最良行動集合</th>
    </tr>
    <tr>
      <th>回答</th>
      <th>再検索</th>
      <th>追加取得</th>
      <th>再検索・追加取得</th>
    </tr>
  </thead>
  <tbody>
    <tr><td rowspan="3">4B</td><td>回答</td><td><strong>920</strong></td><td>151</td><td>157</td><td>157</td></tr>
    <tr><td>再検索</td><td>753</td><td><strong>480</strong></td><td>424</td><td><strong>460</strong></td></tr>
    <tr><td>追加取得</td><td>139</td><td>147</td><td><strong>87</strong></td><td><strong>138</strong></td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="4">9B</td><td>回答</td><td><strong>1,041</strong></td><td>303</td><td>238</td><td>313</td></tr>
    <tr><td>再検索</td><td>417</td><td><strong>452</strong></td><td>340</td><td><strong>394</strong></td></tr>
    <tr><td>追加取得</td><td>0</td><td>0</td><td><strong>0</strong></td><td><strong>0</strong></td></tr>
    <tr><td>形式不正</td><td>0</td><td>0</td><td>1</td><td>0</td></tr>
  </tbody>
  <tbody>
    <tr><td rowspan="3">27B</td><td>回答</td><td><strong>1,050</strong></td><td>100</td><td>115</td><td>109</td></tr>
    <tr><td>再検索</td><td>888</td><td><strong>687</strong></td><td>535</td><td><strong>623</strong></td></tr>
    <tr><td>追加取得</td><td>1</td><td>0</td><td><strong>1</strong></td><td><strong>1</strong></td></tr>
  </tbody>
</table>
