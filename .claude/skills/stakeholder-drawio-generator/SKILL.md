---
name: stakeholder-drawio-generator
description: ステークホルダーモデルのDrawIO形式のファイルを作成する。
---

## 実行手順

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `output/stakeholder.tsv` が存在する

### 手順1: エージェントの起動

`Task` ツールで `StakeholderDrawioGenerator` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/drawio/stakeholder.drawio` が存在する場合は削除する。

### 手順3: DrawIOファイルの出力

**【重要】エージェント完了後、Agentが設計したDrawIOモデルのデータを受け取り、必ず以下を実行**:

`Write` ツールで以下を作成（@common-procedures の「DrawIO出力形式の共通ルール」に従う）：

- **ファイルパス**: `output/drawio/stakeholder.drawio`
- **ファイル形式**: DrawIO XML形式
- サンプルファイルのXML構造を参考にする

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

`output/drawio/stakeholder.drawio`が作成されていない場合、手順3に戻る。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。

/clear
