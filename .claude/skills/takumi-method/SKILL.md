---
name: takumi-method
description: 匠Methodでビジネス企画をモデリングする際に使用。ステークホルダーモデル、価値デザインモデル、価値分析モデル、要求分析ツリーの知識を提供。
allowed-tools: Read, Glob, Grep
user-invocable: false
---

# 匠Method スキル

このスキルは匠Methodの知識を提供します。

---

## 匠Methodとは

「価値」を起点にビジネスやサービスを創造・デザインする体系的な企画手法。

### 特徴
- 「知・情・意」の統合
  - 「情（おもてなしの心など、他者を引き寄せるもの）」や「意（社会に対する思いなど、自分たちの強い意志）」という2種類の価値をデザインし、それらを基に「知（戦略）」を策定する。
- 「情」は、「顧客が感じる「価値（ニーズ）」、「意」は、提供する側が持つ「価値（シーズ）」である。これら二つの側面から価値をデザインする。
- 「価値創造サイクル」
  - 価値のデザインから始まり、要求の創出、業務の改善、具体的な活動計画までを「価値創造サイクル」として一貫して描く

### 匠Methodのモデル

| Phase | 名前 | 目的 | 視点 |
|-------|------|------|------|
| 1 | ステークホルダーモデル | 関係者を洗い出す | Who |
| 2 | 価値デザインモデル | シーズ、深層的価値をモデル化。「意」のモデル。 | Why（本質） |
| 3 | 価値分析モデル | ニーズ、表層的価値をモデル化。「情」のモデル。 | Why（顕在） |
| 4 | 要求分析ツリー | 要求を階層化。「知」のモデル。 | What/How |

---

## フェーズの流れ

```
Phase 1          Phase 2           Phase 3          Phase 4
ステークホルダー → 価値デザイン → 価値分析 → 要求分析
  (Who)           (深層Why)        (表層Why)      (What/How)
```

**重要**: 各フェーズは順番に進める。Phase3とPhase3は入れ替えることが出来る。

---

## 各フェーズの詳細

詳細は以下の資料を参照：

- @stakeholder.md - ステークホルダーモデルの詳細
- @value-design.md - 価値デザインモデルの詳細
- @value-analysis.md - 価値分析モデルの詳細
- @requirement-tree.md - 要求分析ツリーの詳細
- @business-context-flow.md - ビジネスコンテキストフローの詳細
- @goal-description.md - ゴール記述モデルの詳細
- @value-metrics.md - Value Metrics（価値概念・インパクト評価・スコア乖離検証）の詳細

---

## 品質基準（共通）

### 全フェーズ共通
- [ ] 前フェーズとの整合性がある
- [ ] 成果物ファイルが正しく生成されている

### Phase 1: ステークホルダーモデル
- [ ] ステークホルダーが5個以上
- [ ] 各ステークホルダーの課題が明確
- [ ] TSVとDrawIOが正しい形式

### Phase 2: 価値デザインモデル
- [ ] ビジョンが明確に定義されている
- [ ] コンセプトがビジョンを実現する手段として定義
- [ ] シーズ（技術・強み）が具体的
- [ ] 深層的価値が本質的

### Phase 3: 価値分析モデル
- [ ] ニーズ（顧客要求）が具体的
- [ ] 表層的価値（見える価値）が明確
- [ ] Phase 2との整合性がある

### Phase 4: 要求分析ツリー
- [ ] 要求が階層的に整理
- [ ] 上位・下位要求の関係が論理的
- [ ] 全Phaseとの整合性がある

---

## 成果物一覧

| Phase | TSVファイル | DrawIOファイル |
|-------|------------|---------------|
| 1 | output/stakeholder.tsv | output/drawio/stakeholder-model.drawio |
| 2 | output/value-design-*.tsv | output/drawio/value-design-model.drawio |
| 3 | output/value-analysis-*.tsv | output/drawio/value-analysis-model.drawio |
| 4 | output/requirement-tree-*.tsv | output/drawio/requirement-tree.drawio |
