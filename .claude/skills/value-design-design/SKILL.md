---
name: value-design-design
description: 価値デザインモデルのデザインの作成（Phase 2-4c）
---

# Phase 2-4c: デザインの作成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 2-4bが完了している
- `output/value-design.tsv` が存在する（ビジョン、コンセプト、言葉、意味、ストーリーが含まれている）

**出力ファイル**:
- `output/value-design.tsv`（更新：デザイン列を追加）
- `output/value-design-logo.svg`

---

## 実行手順

### 手順1: 入力ファイルの読み込み

`Read` ツールで以下のファイルを読み込む：
- `input/idea.md`
- `output/value-design.tsv`

`Glob` で `input/*.svg` および `input/*.png` を検索し、ロゴファイルの存在をチェックする。
- ロゴファイルが存在する場合: そのファイルパスを記録する（手順4で使用）

### 手順2: デザインの作成

`Task` ツールで `ValueDesignDesign` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順3: TSVファイルの更新（デザイン列を追加）

既存の `output/value-design.tsv` を読み込み、デザイン列を追加して更新する。

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/value-design.tsv`
- **ヘッダー**: `ビジョン	コンセプト1の名前	コンセプト1	コンセプト2の名前	コンセプト2	コンセプト3の名前	コンセプト3	言葉	意味	ストーリー	デザイン`
- **データ行**: 1行（全要素を含む）

### 手順4: SVGロゴファイルの出力

**手順1で`input/`ディレクトリにロゴファイルが見つかった場合:**

`Read` ツールでロゴファイルの内容を読み込み、`Write` ツールで `output/value-design-logo.svg` として出力する。
※ PNGファイルの場合もそのまま`.svg`としてコピー（拡張子は統一）

**ロゴファイルが見つからなかった場合:**

`Write` ツールで以下を作成：
- **パス**: `output/value-design-logo.svg`
- **形式**: SVG画像
- **内容**: デザインコンセプトを視覚的に表現したロゴ

### 手順5: 出力確認

@common-procedures の「出力確認手順」に従い、以下のファイルの存在を確認する：
- `output/value-design.tsv`
- `output/value-design-logo.svg`

### 手順6: 完了報告

@common-procedures の「完了報告」に従う。

次のステップとして `/value-design-drawio-generator` の実行を案内する。