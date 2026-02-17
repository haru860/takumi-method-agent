---
name: value-design-catch-copy
description: 価値デザインモデルの言葉を作成する（Phase 2-3）
---

# Phase 2-3: 言葉（キャッチコピー）の作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 2-2が完了している
- `output/value-design.tsv` が存在する（ビジョンとコンセプトが含まれている）

**出力ファイル**: `output/value-design.tsv`（更新）

---

## 実行手順

### 手順1: 言葉（キャッチコピー）の作成

`Task` ツールで `ValueDesignCatchCopy` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: TSVファイルの更新（追記）

既存の `output/value-design.tsv` を読み込み、言葉列を追加して更新する。

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-design.tsv`
- **ヘッダー**: `ビジョン	コンセプト1の名前	コンセプト1	コンセプト2の名前	コンセプト2	コンセプト3の名前	コンセプト3	言葉`
- **データ行**: 1行（既存のビジョン・コンセプトと言葉を結合）

### 手順3: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

- ビジョン、コンセプト3つ、言葉が正しく記載されていることを確認

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

次のステップとして `/value-design-meaning` の実行を案内する。