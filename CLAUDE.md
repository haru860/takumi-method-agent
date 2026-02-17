# 匠Method Agentプロジェクト

## プロジェクト概要

このプロジェクトは、ビジネス企画立案のための体系的メソッド「匠Method」を、生成AIを活用して自動化・支援するものです。

## 匠Methodとは

ビジネス企画を4つのフェーズで体系的に進めるメソッドです：

1. **Phase 1: ステークホルダーモデル** - 関係するステークホルダーを洗い出し、モデル化する
2. **Phase 2: 価値デザインモデル** - シーズ、深層的価値をモデル化する
3. **Phase 3: 価値分析モデル** - ニーズ、表層的価値をモデル化する
4. **Phase 4: 要求分析ツリー** - 要求を階層化し、モデル化する

## 準備: 企画案の作成

モデリングを開始する前に、`input/idea.md` に企画案を準備します。

### 新規企画の場合（対話型）

`/idea-create` コマンドで対話形式で企画案を作成できます。

### 新規企画の場合（手動作成）

`input/idea.md` を手動で作成することもできます。以下の形式で記載してください：

```markdown
# 企画案

## 企画の背景、問題意識、企画者の思い
[解決したい課題や問題意識を記載]

## 企画の背景、問題意識を解決するためのアイデア（概要）
[アイデアの概要を記載]
```

### 既存製品・サービスを分析する場合

`/idea-create-by-product-research <url1> [url2] ...` コマンドでURLから企画案を自動生成します。

## Claude Codeの役割

あなた（Claude Code）は、以下の役割を担います：

1. ビジネスの情報をファイルから読み込む（`input/`ディレクトリから読み込む）
2. 各フェーズに対応したSubAgentを起動
3. 匠Methodに従ってモデリングプロセスを実行
4. 各フェーズの成果物（TSV、DrawIO XML、JSON等）を`output/`ディレクトリに生成
5. 品質チェックとフィードバックの提供

## スラッシュコマンド一覧

すべてのコマンドは `.claude/skills/` 配下にSkillとして定義されています。

### 一括実行コマンド

| コマンド | 説明 |
|---------|------|
| `/takumi-method-all` | 全成果物（テキストデータ + DrawIOモデル）を一括作成 |
| `/takumi-method-all-only-text-data` | 全成果物のテキストデータ（TSV）を一括作成 |
| `/takumi-method-core-all-only-text-data` | コアモデルのテキストデータを一括作成 |
| `/takumi-method-drawio-all` | DrawIOモデル（コアモデル + ビジネスコンテキストフロー）をすべて作成 |
| `/takumi-method-drawio-core-all` | コアモデルのDrawIOモデルを作成 |

### 企画案作成

| コマンド | 説明 |
|---------|------|
| `/idea-create` | 対話型で企画案を作成 |
| `/idea-create-by-product-research` | 既存製品・サービス分析から企画案を生成 |

### Phase 1: ステークホルダーモデル

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/stakeholder-all-only-text-data` | Phase 1 TSV一括作成 | `output/stakeholder.tsv` |
| `/stakeholder-extractor` | ステークホルダー抽出 | `output/stakeholder.tsv` |
| `/stakeholder-drawio-generator` | DrawIO生成 | `output/drawio/stakeholder.drawio` |

### Phase 2: 価値デザインモデル

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/value-design-all-only-text-data` | Phase 2 TSV一括作成 | `output/value-design.tsv` |
| `/value-design-vision` | ビジョンの作成 | `output/value-design.tsv` |
| `/value-design-concept` | コンセプトの作成 | `output/value-design.tsv` |
| `/value-design-catch-copy` | 言葉（キャッチコピー）の作成 | `output/value-design.tsv` |
| `/value-design-meaning` | 意味の作成 | `output/value-design.tsv` |
| `/value-design-story` | ストーリーの作成 | `output/value-design.tsv` |
| `/value-design-design` | デザインの作成 | `output/value-design.tsv` |
| `/value-design-drawio-generator` | DrawIO生成 | `output/drawio/value-design.drawio` |

### Phase 3: 価値分析モデル

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/value-analysis-all-only-text-data` | Phase 3 TSV一括作成 | `output/value-analysis-*.tsv` |
| `/value-analysis-value-description` | 価値記述の作成 | `output/value-analysis-value-description.tsv` |
| `/value-analysis-objective` | 目的の作成 | `output/value-analysis-objective.tsv` |
| `/value-analysis-drawio-generator` | DrawIO生成 | `output/drawio/value-analysis.drawio` |

### Phase 4: 要求分析ツリー

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/requirement-tree-all-only-text-data` | Phase 4 TSV一括作成 | `output/requirement-tree-*.tsv` |
| `/requirement-tree-business-requirement` | 業務要求の作成 | `output/requirement-tree-business.tsv` |
| `/requirement-tree-it-requirement` | IT要求の作成 | `output/requirement-tree-it.tsv` |
| `/requirement-tree-activity` | 活動の作成 | `output/requirement-tree-activity.tsv` |
| `/requirement-tree-drawio-generator` | DrawIO生成 | `output/drawio/requirement-tree.drawio` |
| `/requirement-tree-make-json` | JSON出力と構造検証 | `output/requirement-tree.json` |
| `/requirement-tree-priority` | MSP計画に基づく優先要素の色分け表示 | |
| `/requirement-tree-it-activity-add` | 下位要素が存在しない業務要求にIT要求/活動を追加 | |

### ビジネスコンテキストフロー

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/business-context-flow-drawio-generator` | ビジネスコンテキストフロー作成 | `output/drawio/business-context-flow.drawio` |

### 匠Method Value Metrics（VM）

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/vm-all` | VM全評価を一括実行 | |
| `/vm-value-concept-score` | 価値概念のリストアップとインパクト評価 | `output/vm-value-concept.tsv` |
| `/vm-it-activity-impact-score` | IT要求・活動のインパクトスコア算出 | `output/vm-*.tsv` |
| `/vm-compare-score` | 価値概念との乖離検証 | `output/vm-compare-score.md` |

### 計画・企画書作成

| コマンド | 説明 | 成果物 |
|---------|------|--------|
| `/planning-all` | 企画立案の全成果物を一括作成 | |
| `/planning-causal-loop-diagram` | 因果関係ループ図の作成 | `output/causal-loop-diagram.md` |
| `/planning-msp-plan` | MSP計画の作成 | `output/msp-plan.md` |
| `/goal-description` | ゴール記述モデルの作成 | `output/goal-description-model.tsv` |
| `/planning-proposal-make` | 企画書の生成 | `output/proposal-format1.md` |

### 検証コマンド

| コマンド | 説明 |
|---------|------|
| `/verify-stakeholder` | ステークホルダーモデルの検証 |
| `/verify-vision` | ビジョンの検証 |
| `/verify-concept` | コンセプトの検証 |
| `/verify-catch-copy` | キャッチコピーの検証 |
| `/verify-meaning` | 意味の検証 |
| `/verify-story` | ストーリーの検証 |
| `/verify-design` | デザインの検証 |
| `/verify-value-description` | 価値記述の検証 |
| `/verify-objective` | 目的の検証 |
| `/verify-business-requirement` | 業務要求の検証 |
| `/verify-it-requirement` | IT要求の検証 |
| `/verify-activity` | 活動の検証 |
| `/verify-value-description-sales-profit` | 価値記述の売上・利益観点での検証 |
| `/verify-goal-description` | ゴール記述モデルの検証 |
| `/verify-vm-value-concept-score` | 価値概念スコアの検証 |
| `/verify-vm-it-activity-impact-score` | IT要求・活動インパクトスコアの検証 |
| `/verify-vm-compare-score` | スコア乖離検証結果の検証 |
| `/verify-planning-causal-loop-diagram` | 因果関係ループ図の検証 |
| `/verify-planning-msp-plan` | MSP計画の検証 |
| `/verify-planning-proposal-make` | 企画書の検証 |

### 洗練コマンド（検証結果に基づく修正）

対応する `verify-*` を先に実行してから使用します。`/refine-{要素名}` の形式です。

| コマンド | 説明 |
|---------|------|
| `/refine-stakeholder` | ステークホルダーモデルの洗練 |
| `/refine-vision` | ビジョンの洗練 |
| `/refine-concept` | コンセプトの洗練 |
| `/refine-catch-copy` | キャッチコピーの洗練 |
| `/refine-meaning` | 意味の洗練 |
| `/refine-story` | ストーリーの洗練 |
| `/refine-design` | デザインの洗練 |
| `/refine-value-description` | 価値記述の洗練 |
| `/refine-objective` | 目的の洗練 |
| `/refine-business-requirement` | 業務要求の洗練 |
| `/refine-it-requirement` | IT要求の洗練 |
| `/refine-activity` | 活動の洗練 |
| `/refine-value-description-sales-profit` | 価値記述の洗練（売上・利益観点） |
| `/refine-goal-description` | ゴール記述モデルの洗練 |
| `/refine-vm-value-concept-score` | 価値概念スコアの洗練 |
| `/refine-vm-it-activity-impact-score` | IT要求・活動インパクトスコアの洗練 |
| `/refine-vm-compare-score` | スコア乖離検証結果の洗練 |
| `/refine-planning-causal-loop-diagram` | 因果関係ループ図の洗練 |
| `/refine-planning-msp-plan` | MSP計画の洗練 |
| `/refine-planning-proposal-make` | 企画書の洗練 |

### 説明コマンド

`/desc-{要素名}` の形式で、各要素の作成観点を説明します。

| コマンド | 説明 |
|---------|------|
| `/desc-takumi-method` | 匠Method全体の概要と各フェーズの関係を説明 |
| `/desc-takumi-method-agent` | 匠Method Agentの使い方を説明 |
| `/desc-stakeholder` | ステークホルダーモデルの観点を説明 |
| `/desc-value-design` | 価値デザインモデルの観点を説明 |
| `/desc-vision` | ビジョンの観点を説明 |
| `/desc-concept` | コンセプトの観点を説明 |
| `/desc-catch-copy` | キャッチコピーの観点を説明 |
| `/desc-meaning` | 意味の観点を説明 |
| `/desc-story` | ストーリーの観点を説明 |
| `/desc-design` | デザインの観点を説明 |
| `/desc-value-analysis` | 価値分析モデルの観点を説明 |
| `/desc-value-description` | 価値記述の観点を説明 |
| `/desc-objective` | 目的の観点を説明 |
| `/desc-requirement-tree` | 要求分析ツリーの観点を説明 |
| `/desc-business-requirement` | 業務要求の観点を説明 |
| `/desc-it-requirement` | IT要求の観点を説明 |
| `/desc-activity` | 活動の観点を説明 |
| `/desc-business-context` | ビジネスコンテキストフローの観点を説明 |
| `/desc-goal-description` | ゴール記述モデルの観点を説明 |
| `/desc-value-metrics` | Value Metrics（価値概念・インパクト評価・スコア乖離検証）の観点を説明 |
| `/desc-verify-vm-value-concept-score` | 価値概念スコア検証の観点を説明 |
| `/desc-verify-vm-it-activity-impact-score` | IT要求・活動インパクトスコア検証の観点を説明 |
| `/desc-verify-vm-compare-score` | スコア乖離検証結果の検証の観点を説明 |
| `/desc-planning-causal-loop-diagram` | 因果関係ループ図の観点を説明 |
| `/desc-planning-msp-plan` | MSP計画の観点を説明 |
| `/desc-planning-proposal-make` | 企画書の観点を説明 |

### その他

| コマンド | 説明 |
|---------|------|
| `/rdra-make-initial-needs` | 匠Methodの成果物からRDRAの初期要望を生成 |
| `/takumi-method` | 匠Methodの知識ベースを参照 |

## ディレクトリ構造

```
<project-root>/
├── CLAUDE.md                    # このファイル（プロジェクト全体のガイド）
├── .claude/
│   ├── settings.local.json      # ローカル設定
│   ├── agents/                  # 各フェーズ専門のSubAgent（実作業担当）
│   │   ├── StakeholderExtractor.md, StakeholderDrawioGenerator.md  # Phase 1
│   │   ├── ValueDesign*.md      # Phase 2（Vision, Concept, CatchCopy, Meaning, Story, Design, DrawioGenerator）
│   │   ├── ValueAnalysis*.md    # Phase 3（ValueDescription, Objective, DrawioGenerator）
│   │   ├── RequirementTree*.md  # Phase 4（Business, It, Activity, DrawioGenerator）
│   │   ├── Desc*.md, Verify*.md # 説明・検証エージェント
│   │   └── その他               # IdeaGenerator, CausalLoopDiagramGenerator, ProposalGenerator 等
│   └── skills/                  # スキル定義（スラッシュコマンド）
│       ├── common-procedures/   # 共通手順（TSV/DrawIO出力ルール等）
│       ├── takumi-method/       # 匠Methodの知識ベース（examples/ にDrawIOサンプル）
│       └── <コマンド名>/SKILL.md
├── docs/
│   └── process-flow.drawio      # プロセスフロー図
├── input/
│   └── idea.md                  # 企画案（ユーザーが準備）
├── output/                      # 生成された成果物（TSV, JSON, MD, DrawIO）
│   └── drawio/                  # DrawIOモデル
└── samples/                     # サンプル企画（入出力の参考例）
    └── furoya-takumi/           # サンプル：風呂屋の匠
        ├── input/               # 企画案（idea.md）
        └── output/              # 全成果物（TSV, JSON, MD, DrawIO）
```

## トラブルシューティング

- **情報が不足している場合**: ユーザーに質問し、仮定を明確にして進め、仮定は成果物に明記する
- **成果物が基準を満たさない場合**: 不足項目を指摘し、改善案を提示して再作成を提案する
- **ファイル形式が正しくない場合**: エラー箇所を特定して修正し、再生成する

## 参考情報

- 匠Methodの知識: `.claude/skills/takumi-method/`
- 共通手順（TSV/DrawIO出力ルール等）: `.claude/skills/common-procedures/SKILL.md`
- DrawIOサンプル: `.claude/skills/takumi-method/examples/`（XML構造の参考のみ）
- 入力ファイル: `input/idea.md`
