---
name: refine-planning-msp-plan
description: 検証結果に基づいてMSP計画を洗練・修正する
---

# MSP計画の洗練

**追加指示（引数）**: $ARGUMENTS

**前提条件**:
- `/verify-planning-msp-plan` が完了している
- `output/verify-planning-msp-plan-result.md` が存在する

**出力ファイル**: `output/msp-plan.md`（更新）

---

## 実行手順

### 手順1: 検証結果ファイルの存在確認

`Glob` ツールで `output/verify-planning-msp-plan-result.md` の存在を確認する。

**ファイルが存在しない場合**:
以下のメッセージを出力して処理を終了する。

```
検証結果ファイルが見つかりません: output/verify-planning-msp-plan-result.md

先に `/verify-planning-msp-plan` を実行して、MSP計画の検証を行ってください。
```

### 手順2: 検証結果の読み込み

`Read` ツールで `output/verify-planning-msp-plan-result.md` を読み込み、以下の情報を抽出する：

- **悪い点・改善点**: 現在のMSP計画の問題点
- **改善のための問い**: MSP計画を改善するためのヒント

### 手順3: MSP計画の再作成

`Skill` ツールで `planning-msp-plan` スキルを呼び出す。

**引数として以下を渡す**:

```
【検証結果に基づく修正指示】

以下の改善点を踏まえて、MSP計画を再作成してください：

[悪い点・改善点の内容をここに記載]

以下の問いを参考にしてください：

[改善のための問いの内容をここに記載]
```

### 手順4: 完了報告

@common-procedures の「完了報告」に従う。

検証と修正のサイクルを続ける場合は、再度 `/verify-planning-msp-plan` の実行を案内する。
