---
name: desc-takumi-method-agent
description: 匠Method Agentの使い方を説明する
---

# 匠Method Agentの使い方説明

**追加指示（引数）**: $ARGUMENTS

---

## 実行手順

### 手順1: 知識の読み込み

以下のファイルを読み込み、匠Method Agentの使い方を説明する：

- `CLAUDE.md`
- `README.md`

**エージェントへの追加指示**: 上記の「追加指示（引数）」が空でない場合、その内容を考慮して説明すること。

---

## 説明すべき内容

### 1. 匠Method Agentとは
- 匠Methodを生成AIで自動化・支援するツール
- Claude Codeのスラッシュコマンドでモデルを生成
- AIが生成するモデルは「たたき台」であり、人間が魂を込めることが重要

### 2. セットアップと準備
- リポジトリのクローンとClaude Codeの起動
- 企画案（`input/idea.md`）の3つの準備方法
  - `/idea-create`（対話型）
  - `/idea-create-by-product-research <url>`（既存製品分析）
  - 手動作成

### 3. 基本的な使い方（2パターン）

#### パターンA: 一括実行（クイックスタート）
- `/takumi-method-all` : 全成果物（テキスト + DrawIO）を一括作成
- `/takumi-method-all-only-text-data` : テキストデータのみ一括作成
- `/takumi-method-core-all-only-text-data` : コアモデルのみ一括作成

#### パターンB: ステップバイステップ
- Phase 1 → Phase 2 → Phase 3 → Phase 4 の順に個別実行
- 各フェーズで成果物を確認・修正しながら進める

### 4. コマンド体系の全体像

| カテゴリ | プレフィックス | 説明 | 例 |
|---------|---------------|------|-----|
| 作成 | （なし） | モデル・成果物を作成 | `/value-design-vision` |
| 検証 | `verify-` | 良い点5つ・改善点5つ・問い5つを生成 | `/verify-vision` |
| 洗練 | `refine-` | 検証結果に基づき再作成 | `/refine-vision` |
| 説明 | `desc-` | 作成観点や知識を説明 | `/desc-vision` |
| 一括 | `*-all*` | 複数の成果物をまとめて作成 | `/takumi-method-all` |

### 5. 検証→洗練サイクル
- `verify-*` で検証 → `refine-*` で洗練 → 再度 `verify-*` のサイクル
- 検証結果は `output/verify-*-result.md` に保存される
- 洗練コマンドは検証結果ファイルを読み込んで改善指示を作成する

### 6. フェーズ別コマンドの流れ

#### Phase 1: ステークホルダーモデル
- `/stakeholder-extractor` → `/stakeholder-drawio-generator`

#### Phase 2: 価値デザインモデル
- `/value-design-vision` → `/value-design-concept` → `/value-design-catch-copy` → `/value-design-meaning` → `/value-design-story` → `/value-design-design` → `/value-design-drawio-generator`

#### Phase 3: 価値分析モデル
- `/value-analysis-value-description` → `/value-analysis-objective` → `/value-analysis-drawio-generator`

#### Phase 4: 要求分析ツリー
- `/requirement-tree-business-requirement` → `/requirement-tree-it-requirement` → `/requirement-tree-activity` → `/requirement-tree-drawio-generator`

### 7. オプション機能

#### Value Metrics（VM）
- `/vm-value-concept-score` → `/vm-it-activity-impact-score` → `/vm-compare-score`
- 価値概念とIT要求・活動のスコアを定量評価し、乖離を検証

#### 計画・企画書
- `/planning-causal-loop-diagram` : 因果関係ループ図
- `/planning-msp-plan` : MSP計画
- `/goal-description` : ゴール記述モデル
- `/planning-proposal-make` : 企画書生成

#### その他
- `/business-context-flow-drawio-generator` : ビジネスコンテキストフロー
- `/rdra-make-initial-needs` : RDRAの初期要望生成
- `/requirement-tree-priority` : MSP計画に基づく優先要素の色分け

### 8. 成果物の確認方法
- TSVファイル: テキストエディタまたはTSV Tweaker（VS Code拡張）
- DrawIOファイル: DrawIOアプリまたはDrawIO Integration（VS Code拡張）
- Markdownファイル: MarkDown Preview Mermaid Support（VS Code拡張）
- 企画書（Marp形式）: Marp for VS Code
- JSONファイル: JSON Crack（VS Code拡張）

### 9. 推奨ワークフロー
1. `/idea-create` で企画案を作成
2. `/takumi-method-all-only-text-data` で全テキストデータを一括作成
3. 各フェーズの成果物を確認し、`verify-*` → `refine-*` で品質向上
4. `/takumi-method-drawio-all` でDrawIOモデルを生成
5. `/vm-all` でValue Metricsを実施
6. `/planning-all` で計画・企画書を作成

---

## 完了時の動作

- 匠Method Agentの使い方をコンソールに出力
- ファイル出力は行わない（参考情報として提供）
