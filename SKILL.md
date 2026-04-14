---
name: screenshot-review
description: スクリーンショットを GitHub Copilot CLI (GPT-5.4) に送ってUIレビューを受ける。
  「UIレビュー」「デザインチェック」「見た目レビュー」「スクショレビュー」
  「GPTレビュー」「Copilotに見せて」「画面レビュー」といった依頼で使用。
  スクリーンショット撮影後や、UI実装後に自動的にこのスキルを提案すること。
---

# スクリーンショットレビュー（GitHub Copilot CLI + GPT-5.4）

GitHub Copilot CLI 経由で GPT-5.4 にスクリーンショットを送り、UIのフィードバックを得る。

## 前提条件

- GitHub Copilot CLI がインストール済み（`gh extension install github/gh-copilot`）
- `gh auth login` で GitHub アカウント認証済み

未インストールの場合はユーザーにセットアップ手順を案内して中断する。

## 実行手順

### Step 1: スクリーンショットの確認

ユーザーからパスが指定されていればそれを使う。指定がなければプロジェクト内の画像を探す。画像が見つからない場合はユーザーにパスを確認する。

### Step 2: プロンプトの組み立て

ユーザーの依頼内容に応じてレビュープロンプトを組み立てる。

- **画面の種類や文脈**を特定し、プロンプトに含める
- **確認したい観点**がユーザーから指定されていればそれを優先する
- 指定がなければ以下のデフォルト観点を使う:
  - レイアウトバランス（余白、配置、情報の重心）
  - 色のコントラスト・可読性
  - 視覚的な階層（見出し > コンテンツ > 操作）
  - 改善すべき点の優先度付け（高/中/低）

プロンプトは英語で書き、回答言語はユーザーの言語に合わせて指定する。

### Step 3: Copilot CLI 実行

```bash
gh copilot -p "@<画像パス> <組み立てたプロンプト>" \
  --allow-all --model gpt-5.4 -s
```

**複数画像（Before/After 比較など）:**

```bash
gh copilot -p "@<画像パス1> @<画像パス2> <組み立てたプロンプト>" \
  --allow-all --model gpt-5.4 -s
```

**注意点:**
- 画像パスは `@` を先頭に付ける（例: `@./screenshots/screen-0.png`）
- 画像は2-4枚が目安。多すぎると応答が遅くなる
- `--allow-all` は権限許可、`-s` は統計情報の省略

### Step 4: 結果の報告

Copilot CLI の出力を整理してユーザーに報告する:

1. 指摘事項を優先度付きで箇条書きにする
2. 優先度が高い改善点を強調する
3. 「これらの改善に取り組みますか？」と次のアクションを提案する

## プロンプト例

### 汎用レビュー

```
Review the attached screenshot of the UI.
Give feedback in Japanese on: layout balance, color contrast, text readability,
visual hierarchy, and usability. Prioritize improvements as high/medium/low.
```

### Before/After 比較

```
Two screenshots are attached: the first is BEFORE, the second is AFTER.
Compare both versions and give feedback in Japanese on:
- Whether each change improved the UI (and why/why not)
- Any remaining issues or regressions
- Overall assessment of the improvement
```

### 特定観点あり

```
Review the attached screenshot. Focus specifically on: {ユーザー指定の観点}.
Give feedback in Japanese with specific improvement suggestions.
```
