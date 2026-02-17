---
name: value-analysis-value-description
description: Phase 3-1: 価値記述の作成（Phase 3-1）
---

# Phase 3-1: 価値記述の作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 1, Phase 2が完了している
- `output/stakeholder.tsv` が存在する
- `output/value-design.tsv` が存在する

---

## 実行手順

### 手順1: 価値記述の作成

`Task` ツールで `ValueAnalysisValueDescription` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/value-analysis-value-description.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-analysis-value-description.tsv`
- **ヘッダー**: `ステークホルダー	価値記述名	価値記述`
- **データ行**:
  - ステークホルダー: ステークホルダー名
  - 価値記述名: 価値を端的に表す名前
  - 価値記述: 「シチュエーション」+「価値を実現する手段」+「〜で嬉しい」形式の文
- **並び順**: 重要度「高」→「中」の順、各ステークホルダー内は価値の高い順

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。