---
name: rdra-make-initial-needs
description: 匠Methodの成果物からRDRAの初期要望を生成
---

# RDRA初期要望の生成

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- Phase 1〜4が完了している
- 以下のファイルが存在する：
  - `input/idea.md`
  - `output/stakeholder.tsv`
  - `output/value-design.tsv`
  - `output/value-analysis-objective.tsv`
  - `output/requirement-tree-business.tsv`

**目的**: 匠Methodの成果物を元に、RDRAの入力となる初期要望ファイルを生成する

---

## 実行手順

### 手順1: 入力ファイルの読み込み

`Read` ツールで以下のファイルを読み込む：
- `input/idea.md`（企画案・背景情報）
- `output/stakeholder.tsv`（ステークホルダー情報）
- `output/value-design.tsv`（ビジョン・コンセプト）
- `output/value-analysis-objective.tsv`（目的）
- `output/requirement-tree-business.tsv`（業務要求）
- `output/requirement-tree-it.tsv`（IT要求）
- `output/requirement-tree-activity.tsv`（活動）

### 手順2: RDRA初期要望の生成

`Task` ツールで `RdraInitialNeedsGenerator` エージェントを起動する。

**エージェントへの指示（必須）**:
- **【重要】エージェントはファイルを作成しないこと。生成結果はテキストとして返すこと。**
- **【重要】`.claude/agents/RdraInitialNeedsGenerator.md` に定義された出力フォーマットを厳守すること**
- フォーマットは「背景」「要求」「ビジネスポリシー」「ビジネスパラメータ」「業務概要」の5セクション構成
- 「要望一覧」「制約条件」「非機能要件」「システム間連携」などの形式は使用しない
- ファイルへの出力は手順3で親エージェントが行う

**エージェントへの追加指示**: 上記の「追加指示（引数）」が空でない場合、その内容をエージェント起動時のプロンプトに含めて渡すこと。

### 手順3: 初期要望ファイルの出力

**【重要】エージェント完了後、生成結果を必ず以下のファイルに出力する**:

`Write` ツールで以下を作成：
- **ファイルパス**: `output/初期要望.txt`
- **ファイル形式**: テキスト形式
- **内容**: エージェントが生成したRDRA初期要望

---

## 完了時の動作

- 出力したファイル名を報告
