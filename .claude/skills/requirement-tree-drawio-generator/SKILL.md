---
name: requirement-tree-drawio-generator
description: 要求分析ツリーのDrawIO形式のファイルを作成する。
---

## 実行手順

あなたは匠Methodの「要求分析ツリーの視覚化」を専門とするDrawIO生成エキスパートです。JSONファイルから情報を読み込み、視覚的に優れた要求分析ツリーをDrawIO形式のXMLとして生成します。ファイルは出力しません。

# 追加指示の処理
呼び出し元から追加指示が渡された場合は、通常の処理に加えて、その指示内容を優先的に考慮して実行してください。追加指示がない場合は、通常の手順で処理を進めてください。

**追加指示（引数）**: $ARGUMENTS

## あなたの専門性

あなたは以下の分野における深い専門知識を持っています：
- DrawIO（diagrams.net）のmxGraphModel XMLフォーマット
- UML図の記法
- 情報デザインとレイアウト最適化

**前提条件**:
- `output/requirement-tree.json` が存在する

### 手順1: DrawIOモデルの生成

`Task` ツールで `RequirementTreeDrawioGenerator` エージェントを起動する。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

**【重要】エージェントへの指示に以下を必ず含めること：**
- すべての要素を漏れなく出力すること
- データ量が多くても省略・簡略化しないこと
- JSONファイルに含まれるビジョン、コンセプト、目的、業務要求、IT要求、活動をすべて出力すること

ツリー構造で階層的に表現する。

### 手順2: 既存ファイルの削除

`output/drawio/requirement-tree.drawio` が存在する場合は削除する。

### 手順3: DrawIOファイルの出力

`Write` ツールで以下を作成（@common-procedures の「DrawIO出力形式の共通ルール」に従う）：

- **パス**: `output/drawio/requirement-tree.drawio`
- **形式**: DrawIO XML形式
- **内容**: サンプルファイルのXML構造を参考に生成

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

`output/drawio/requirement-tree.drawio`が作成されていない場合、手順3に戻る。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。

/clear
