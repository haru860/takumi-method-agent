---
name: value-design-vision
description: 価値デザインモデルのビジョンを作成（Phase 2-1）
---

# Phase 2-1: ビジョンの作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 1が完了している
- `output/stakeholder.tsv` が存在する

**出力ファイル**: `output/value-design.tsv`

---

## 実行手順

### 手順1: ビジョンの作成

`Task` ツールで `ValueDesignVision` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/value-design.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-design.tsv`
- **ヘッダー**: `ビジョン`
- **データ行**: 1行（ビジョンのみ）

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。

次のステップとして `/value-design-concept` の実行を案内する。