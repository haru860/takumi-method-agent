---
name: stakeholder-extractor
description: Phase 1-1（ステークホルダー抽出とTSV生成）を実行
---

# Phase1-1: ステークホルダーの抽出

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `input/idea.md` が存在する

**出力ファイル**: `output/stakeholder.tsv`

---

## 実行手順

### 手順1: ステークホルダーの抽出

`Task` ツールで `StakeholderExtractor` エージェントを起動し、以下を抽出する：

- ステークホルダー名（役割名）
- 重要度（高/中/低）
- 重要度の理由
- 課題（複数ある場合はカンマ区切り）

最低5つ以上のステークホルダーを洗い出す。

※ @common-procedures の「エージェント起動時の追加指示」を参照。

### 手順2: 既存ファイルの削除

`output/stakeholder.tsv` が存在する場合は削除する。

### 手順3: TSVファイルの出力

`Write` ツールで以下を作成（@common-procedures の「TSV出力形式の共通ルール」に従う）：

- **パス**: `output/stakeholder.tsv`
- **ヘッダー**: `ステークホルダー	重要度	重要度の理由	課題`
- **データ行**:
  - ステークホルダー: 役割名
  - 重要度: 高/中/低
  - 重要度の理由
  - 課題: 複数は「,」区切り
- **並び順**: 重要度 高→中→低

### 手順4: 出力確認

@common-procedures の「出力確認手順」に従い、ファイルの存在を確認する。

### 手順5: 完了報告

@common-procedures の「完了報告」に従う。
