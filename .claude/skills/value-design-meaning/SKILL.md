---
name: value-design-meaning
description: 価値デザインモデルの意味の作成（Phase 2-4a）
---

# Phase 2-4a: 意味の作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 2-3が完了している
- `output/value-design.tsv` が存在する（ビジョン、コンセプト、言葉が含まれている）

**出力ファイル**:
- `output/value-design.tsv`（更新：意味列を追加）

---

## 実行手順

### 手順1: 入力ファイルの読み込み

`Read` ツールで以下のファイルを読み込む：
- `input/idea.md`
- `output/value-design.tsv`

### 手順2: 意味の作成

`Task` ツールで `ValueDesignMeaning` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順3: TSVファイルの更新（意味列を追加）

既存の `output/value-design.tsv` を読み込み、意味列を追加して更新する。

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-design.tsv`
- **ヘッダー**: `ビジョン	コンセプト1の名前	コンセプト1	コンセプト2の名前	コンセプト2	コンセプト3の名前	コンセプト3	言葉	意味`
- **データ行**: 1行（意味まで含む）

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、以下のファイルの存在を確認する：
- `output/value-design.tsv`

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。

次のステップとして `/value-design-story` の実行を案内する。