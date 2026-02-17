---
name: refine-value-description-sales-profit
description: 売上・利益観点での検証結果に基づいて自社の価値記述を洗練・修正する
---

# 価値記述の洗練（売上・利益観点）

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-value-description-sales-profit` が完了している
- `output/verify-value-description-sales-profit-result.md` が存在する

**出力ファイル**: `output/value-analysis-value-description.tsv`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-value-description-sales-profit-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-value-description-sales-profit-result.md

先に `/verify-value-description-sales-profit` を実行して、価値記述の売上・利益観点での検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-value-description-sales-profit-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在の自社の価値記述における売上・利益面の問題点
- **改善のための問い**: 売上・利益を向上させるための価値記述改善のヒント

### 手順3: 価値記述の再作成

`Skill` ツールで `value-analysis-all-only-text-data` スキルを呼び出す。

**引数として以下を渡す**:

```
【売上・利益観点の検証結果に基づく修正指示】

以下の改善点を踏まえて、自社の価値記述を再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]

※自社の価値記述（value-analysis-value-description.tsv の自社行）を売上・利益の観点で改善してください。他のステークホルダーの価値記述は変更しないでください。
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-value-description-sales-profit` の実行を案内する。
