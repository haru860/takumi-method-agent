---
name: planning-proposal-make
description: 匠Methodの成果物から企画書を生成（フォーマット選択可能）
---

# 企画書の生成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 1〜4が完了している
- 以下のファイルが存在する:
  - `output/stakeholder.tsv`
  - `output/value-design.tsv`
  - `output/value-analysis-value-description.tsv`
  - `output/value-analysis-objective.tsv`
  - `output/requirement-tree.json`


## 実行手順

### 手順1: 企画内容の確認

まず `input/idea.md` を読み込み、企画の概要をユーザーに表示して確認を求める。

1. `Read` ツールで `input/idea.md` を読み込む
2. 企画の概要（タイトル、背景、アイデア概要）を簡潔にまとめて表示

### 手順2: フォーマットの確認

追加指示（引数）に `format1` または `format2` が含まれているか確認：

- `format1` が含まれる → Why-What-How型を使用
- `format2` が含まれる → ストーリーテリング型を使用
- 指定なし → `format1` とする（デフォルト値）


### 手順3: 前提条件の確認

`Glob` ツールで以下のファイルが存在することを確認：
- `output/stakeholder.tsv`
- `output/value-design.tsv`
- `output/value-analysis-value-description.tsv`
- `output/value-analysis-objective.tsv`
- `output/requirement-tree.json`

### 手順4: 既存ファイルの削除

選択されたフォーマットに応じたファイル（`output/proposal-format1.md` または `output/proposal-format2.md`）が存在する場合は削除する。

**注意**: ユーザー確認は不要。存在すれば自動的に削除して続行する。

### 手順5: エージェントの起動

`Task` ツールで `ProposalGenerator` エージェントを起動する。

**エージェントへの指示に含めること**:
1. 選択されたフォーマット（`format=format1` または `format=format2`）
2. 追加指示（引数）がある場合はその内容

### 手順6: 企画書ファイルの出力

**【重要】エージェント完了後、Agentが生成した企画書のデータを受け取り、必ず以下を実行**:

`Write` ツールで以下を作成：

- **ファイルパス**: 選択されたフォーマットに応じて決定
  - format1 → `output/proposal-format1.md`
  - format2 → `output/proposal-format2.md`
- **ファイル形式**: Marp形式（Markdownベースのプレゼンテーション）
- エージェントから返却された企画書の内容を出力
- プレゼン資料としてプレビューした際に、ページ枠からはみ出していないレイアウトになっているかを確認する。（特に下枠）。はみ出している場合は修正する。


### 手順7: 出力確認

`Glob` ツールで `output/proposal-format1.md` または `output/proposal-format2.md` の存在を確認。
ファイルが存在しない場合は、手順6に戻りWriteツールでファイルを作成する。

---

## 完了時の動作

- 出力したファイル名を報告
- 使用したフォーマット（Why-What-How型 or ストーリーテリング型）を報告
- 企画書の構成を簡潔に報告
---

## 使用例

```bash
# フォーマット選択プロンプトが表示される（デフォルト）
/planning-proposal-make

# Why-What-How型を指定
/planning-proposal-make format1

# ストーリーテリング型を指定
/planning-proposal-make format2

# ストーリーテリング型 + 追加指示
/planning-proposal-make format2 受講者向けの価値を強調してください

# Why-What-How型 + 簡潔版
/planning-proposal-make format1 2ページ程度の簡潔な企画書にしてください

# 投資家向け（フォーマット選択プロンプトが表示される）
/planning-proposal-make 投資家向けのトーンで作成してください
```

## 企画書の生成

### 目的
匠Methodの成果物を基に、企画書を生成する

### フォーマット選択

以下の2つのフォーマットから選択できます：

| フォーマット | 名前 | 特徴 |
|-------------|------|------|
| `format1` | Why-What-How型（デフォルト） | ゴールデンサークル理論に基づく論理的構成。「なぜ」から始めることで共感を得やすい |
| `format2` | ストーリーテリング型 | 読み手を引き込む物語形式。感情に訴求し、記憶に残りやすい |
