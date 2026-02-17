---
name: business-context-flow-drawio-generator
description: ビジネスコンテキストフロー（業務像モデル）を作成
---

# ビジネスコンテキストフローの作成

**追加指示（引数）**: $ARGUMENTS

## 概要

ビジネスコンテキストフローは、匠Methodのモデルの一つで、企画における人・モノ・カネ・情報の循環を可視化するモデルです。

**目的**:
- 今回の企画の人、モノ、カネ、情報が循環する全体の業務像をモデル化する
- 企画が実現する生態系の業務が無理なく回るかを検証する

**前提条件**:
- Phase 1（ステークホルダーモデル）が完了している
- Phase 4（要求分析ツリー）が完了している
- `output/stakeholder.tsv` が存在する
- `output/requirement-tree.json` が存在する

---

## 実行手順

### 手順1: 前提条件の確認

以下のファイルが存在することを確認する：
- `output/stakeholder.tsv`
- `output/requirement-tree.json`

存在しない場合は、先に該当するPhaseを実行するようユーザーに通知する。

### 手順2: 既存ファイルの削除

`output/drawio/business-context-flow.drawio` が存在する場合は削除する。

### 手順3: エージェントの起動

`Task` ツールで `BusinessContextFlowDrawioGenerator` エージェントを起動する。

**エージェントへの追加指示**: 上記の「追加指示（引数）」が空でない場合、その内容をエージェント起動時のプロンプトに含めて渡すこと。

### 手順4: DrawIOファイルの出力

**【重要】エージェント完了後、Agentが設計したDrawIOモデルのデータを受け取り、必ず以下を実行**:

`Write` ツールで以下を作成：

- **ファイルパス**: `output/drawio/business-context-flow.drawio`
- **ファイル形式**: DrawIO XML形式

### 手順5: 出力確認

- `Glob` ツールで `output/drawio/business-context-flow.drawio` の存在を確認
- ファイルが存在しない場合は、手順4に戻りWriteツールでファイルを作成する

---

## 完了時の動作

- 出力したファイルを報告
- ビジネスコンテキストフローの内容（主要なステークホルダーと流れ）を簡潔に説明

/clear
