---
name: refine-stakeholder
description: 検証結果に基づいてステークホルダーモデルを洗練・修正する
---

# ステークホルダーモデルの洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-stakeholder` が完了している
- `output/verify-stakeholder-result.md` が存在する

**出力ファイル**: `output/stakeholder.tsv`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-stakeholder-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-stakeholder-result.md

先に `/verify-stakeholder` を実行して、ステークホルダーモデルの検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-stakeholder-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在のステークホルダーモデルの問題点
- **改善のための問い**: ステークホルダーモデルを改善するためのヒント

### 手順3: ステークホルダーモデルの再作成

`Skill` ツールで `stakeholder-extractor` スキルを呼び出す。

**引数として以下を渡す**:

```
【検証結果に基づく修正指示】

以下の改善点を踏まえて、ステークホルダーモデルを再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-stakeholder` の実行を案内する。
