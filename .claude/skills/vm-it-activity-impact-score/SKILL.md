---
name: vm-it-activity-impact-score
description: IT要求・活動のインパクトスコアを算出
---

# IT要求・活動インパクトスコア算出

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 4（要求分析ツリー）が完了している
- `/vm-value-concept-evaluator` が完了している（`output/vm-value-concept.tsv` が存在）
- `output/requirement-tree-it.tsv` が存在する
- `output/requirement-tree-activity.tsv` が存在する
- `output/requirement-tree-business.tsv` が存在する

**成果物**:
- `output/vm-it-requirement-impact-score.tsv`
- `output/vm-activity-impact-score.tsv`
- `output/vm-it-requirement-activity-impact-score.tsv`

---

## 実行手順

### 手順1: 入力ファイルの確認

`Glob` ツールで以下のファイルの存在を確認：
- `output/requirement-tree-it.tsv`
- `output/requirement-tree-activity.tsv`
- `output/requirement-tree-business.tsv`
- `output/vm-value-concept.tsv`

ファイルが存在しない場合は、ユーザーに以下を案内：
- `requirement-tree-it.tsv` がない場合 → `/requirement-tree-it-requirement` を実行
- `requirement-tree-activity.tsv` がない場合 → `/requirement-tree-activity` を実行
- `requirement-tree-business.tsv` がない場合 → `/requirement-tree-business-requirement` を実行
- `vm-value-concept.tsv` がない場合 → `/vm-value-concept-evaluator` を実行

### 手順2: 既存ファイルの削除

以下のファイルが存在する場合は削除する：

- `output/vm-it-requirement-impact-score.tsv`
- `output/vm-activity-impact-score.tsv`
- `output/vm-it-requirement-activity-impact-score.tsv`

---

## Part 1: IT要求インパクトスコア算出

### 手順3: IT要求インパクトスコアの算出

`Task` ツールで `ITRequirementImpactEvaluator` エージェントを起動する。

**エージェントへの追加指示**: 上記の「追加指示（引数）」が空でない場合、その内容をエージェント起動時のプロンプトに含めて渡すこと。

### 手順4: IT要求スコアTSVファイルの出力

`Write` ツールで以下を作成：

- **パス**: `output/vm-it-requirement-impact-score.tsv`
- **形式**: TSV（タブ区切り）
- **ヘッダー**: `IT要求 | スコア | スコアの理由 | 関連する業務要求 | 関連する目的`
- **データ行**:
  - IT要求の名前
  - スコア（1, 3, 8, 13, 21, 34, 89のいずれか）
  - スコアの理由
  - 関連する業務要求
  - 関連する目的（業務要求経由で紐づく目的）
- **行の並び順**: スコアが大きい順

---

## Part 2: 活動インパクトスコア算出

### 手順5: 活動インパクトスコアの算出

`Task` ツールで `ActivityImpactEvaluator` エージェントを起動する。

**エージェントへの追加指示**: 上記の「追加指示（引数）」が空でない場合、その内容をエージェント起動時のプロンプトに含めて渡すこと。

### 手順6: 活動スコアTSVファイルの出力

`Write` ツールで以下を作成：

- **パス**: `output/vm-activity-impact-score.tsv`
- **形式**: TSV（タブ区切り）
- **ヘッダー**: `活動 | スコア | スコアの理由 | 関連する業務要求 | 関連する目的`
- **データ行**:
  - 活動の名前
  - スコア（1, 3, 8, 13, 21, 34, 89のいずれか）
  - スコアの理由
  - 関連する業務要求
  - 関連する目的（業務要求経由で紐づく目的）
- **行の並び順**: スコアが大きい順

---

## Part 3: TSVファイルのマージ

### 手順7: TSVファイルのマージ

2つのTSVファイル（IT要求スコア、活動スコア）をマージする。

#### マージ後のTSV形式

- **パス**: `output/vm-it-requirement-activity-impact-score.tsv`
- **形式**: TSV（タブ区切り）
- **ヘッダー**: `名前 | 種別 | スコア | スコアの理由 | 関連する業務要求 | 関連する目的`
- **データ行**:
  - 名前: IT要求名または活動名
  - 種別: 「IT要求」または「活動」
  - スコア: インパクトスコア
  - スコアの理由: スコアの根拠
  - 関連する業務要求: 紐づく業務要求名
  - 関連する目的: 業務要求経由で紐づく目的名
- **並び順**: スコアが大きい順（降順）

#### マージ手順

1. `output/vm-it-requirement-impact-score.tsv` の各行に種別「IT要求」を付与
2. `output/vm-activity-impact-score.tsv` の各行に種別「活動」を付与
3. 両方のデータを統合
4. スコアの降順でソート
5. `output/vm-it-requirement-activity-impact-score.tsv` に出力

---

## 完了時の動作

- IT要求スコアファイルを出力（`output/vm-it-requirement-impact-score.tsv`）
- 活動スコアファイルを出力（`output/vm-activity-impact-score.tsv`）
- マージファイルを出力（`output/vm-it-requirement-activity-impact-score.tsv`）
- スコア別の件数サマリーを表示
- 89点（ダントツ）がない場合は、34点の項目を89点に昇格させる施策案を提示---

## 次のステップ

スコアの比較・検証を行う場合は `/vm-compare-score` を実行してください。
