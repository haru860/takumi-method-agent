---
name: value-analysis-relation
description: 価値記述に「関連する目的」列を追加（Phase 3-3）
---

# Phase 3-3: 価値記述と目的の関連付け

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 3-1、Phase 3-2が完了している
- `output/value-analysis-value-description.tsv` が存在する
- `output/value-analysis-objective.tsv` が存在する

**出力ファイル**: `output/value-analysis-value-description.tsv`（更新：「関連する目的」列を追加）

---

## 実行手順

### 手順1: 入力ファイルの読み込み

`Read` ツールで以下のファイルを読み込む：
- `output/value-analysis-value-description.tsv`
- `output/value-analysis-objective.tsv`

いずれかが存在しない場合は、ユーザーに先行フェーズの完了を求める。

### 手順2: 関連付けの実行

`Task` ツールで `ValueAnalysisRelation` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順3: TSVファイルの更新（「関連する目的」列を追加）

既存の `output/value-analysis-value-description.tsv` を読み込み、「関連する目的」列を追加して更新する。

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-analysis-value-description.tsv`
- **ヘッダー**: `ステークホルダー	価値記述名	価値記述	関連する目的`
- **データ行**: エージェントが返却した関連付け結果に基づき、各行に「関連する目的」を追記

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。

次のステップとして `/value-analysis-drawio-generator` の実行を案内する。
