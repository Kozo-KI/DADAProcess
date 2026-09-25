# Claude Code で DADA Process を使う

このリポジトリを Claude Code（CLI / VS Code・JetBrains 拡張 / デスクトップアプリ）で使うための追加ファイルの説明です。追加したのは「Claude Code が最初に見に行く場所への案内」だけで、DADA の本体（`.agents/`・`docs/`・`tools/`）は変えていません。

## 追加したファイル

| ファイル | 役割 |
| :--- | :--- |
| `CLAUDE.md`（リポジトリ直下） | ルールの入口。インポート記法（`@` + パス）で `.agents/AGENTS.md` の本体ルールを会話の最初に読み込み、Antigravity 向けの記述の読み替え表を持つ |
| `.claude/skills/<name>/SKILL.md`（14件） | スキルの自動発見用の案内。本文は持たず、`.agents/skills/<name>/SKILL.md` を読むよう指示する |
| `.claude/settings.json` | 点検ツール（`tools/dada_check.py`・`tools/agent_def_check.py`）と参照系 git コマンドの実行許可。`.env` の読み取りと `git push` は拒否 |
| `.mcp.json`（リポジトリ直下） | context7 MCP サーバーの登録（任意） |
| `.claude/README.md` | この説明 |

## はじめ方

1. Python 3.8 以降が使えることを確認します（`python --version` / `python3 --version`）。
2. 作業ブランチを切ります（README の Step 4 と同じ）。
3. リポジトリのフォルダで Claude Code を起動します（CLI なら `claude`）。
4. `/skills` と入力し、`dada-process` などが一覧に出ることを確認します。
5. 次の指示文を貼って起動します。

起動に成功すると、AI が「開発対象・実行モード・変更スケール・動作モード」を宣言し、応答の末尾に `[DADA | Phase …]` を付けます。Claude Code にはサブエージェント起動ツール（Agent ツール）があるため、動作モードは **ツールが自動的にサブエージェントを作る**（`context-reset` の方式A）になります。

## ASDoQ 文書品質モデルを使うレビューエージェントを作る（A開発承認ゲート型）

ASDoQ の品質モデルは `docs/guidelines/` にあります。新しく作るエージェントも、この3ファイルを**単一の情報源として参照**させ、スキル配下へ複製しないでください（`.agents/AGENTS.md` 第7節）。

| ファイル | 用途 |
| :--- | :--- |
| `docs/guidelines/asdoq_checklist.md` | 軽量チェックリスト（6大品質特性 × 副特性 × 測定項目、文書別の重点特性ガイド） |
| `docs/guidelines/asdoq_model_markdown.md` | フル版（例文・違反例付き）。厳密レビュー時のみ |
| `docs/guidelines/asdoq_writing_rules.md` | 執筆ルール12箇条（書き手向け） |

### コピー用の指示文

`[ ]` の中を自分の要件に書き換えてください。

```text
DADAプロセス承認ゲート型を開始します。
・開発対象：エージェント定義（Claude Code 向け ASDoQ 文書品質レビューエージェント一式）
・要求概要：任意の開発文書（例: [要求仕様書・設計書・取扱説明書などの対象文書]）を入力として受け取り、
  docs/guidelines/ の ASDoQ 文書品質モデル（軽量チェックリスト／フル版）の6大品質特性・副特性・測定項目に照らしてレビューし、
  指摘を [指摘ID・品質特性・該当箇所（ファイルパス:行番号）・重大度・修正案] の形式でレビュー記録表に出力する。
  [文書の種類ごとの重点特性、重大度の基準、日本語/英語の対応など、追加の要求]
・構成留意点：エージェント定義は『自然言語レイヤー（SKILL.md, AGENTS.md, 参照docs）』と『プログラム言語レイヤー（Pythonツール）』の二重構造として責務を切り分けること。
  曖昧語・表の空欄など機械的に判定できる項目は Python ツールへ委譲し、図表と本文の齟齬・用語のゆれ・目的適合性など判断が必要な項目をスキルに担当させること。
  レビューする役割と、レビュー結果を評価する役割は別スキルにすること。
  新しく作るスキルは .agents/skills/ に置き、同じ作業単位で .claude/skills/ に案内ファイルを追加すること。
各Phaseごとにエージェント要求仕様書、二重評価仕様書（Eval Dataset＋単体テスト）、アーキテクチャ設計書、総合テスト報告書を作成し、人間の承認ゲートを挟んで進めてください。
```

一気に完成まで任せる場合は、1行目を `DADAプロセス自律型を開始します。` にします。そのときは作業ブランチ上で、権限モードを `acceptEdits`（`Shift+Tab` で切替）にしておくと、ファイル更新のたびに確認で止まりません。

## context7（任意）

最新のライブラリ情報を調べる `context7-mcp` スキルを使う場合だけ設定します。

1. [https://context7.com/](https://context7.com/) で API キーを取得します。
2. Claude Code を起動する前に、環境変数 `CONTEXT7_API_KEY` にキーを設定します（キーはファイルに書かず、Git に入れないでください）。
   - Windows（PowerShell）: `$env:CONTEXT7_API_KEY = "取得したキー"`
   - macOS / Linux: `export CONTEXT7_API_KEY="取得したキー"`
3. 起動時に `.mcp.json` のサーバーを承認するか聞かれたら承認します。`/mcp` で `context7` が接続済みか確認できます。

## 保守のルール

- 本文を直すときは `.agents/` 側だけを直します。`.claude/skills/` の案内ファイルは本文を持たないため、直す必要があるのは `description` を変えたときだけです（`name` と `description` は `.agents/` 側と一字一句同じにする）。
- スキルを追加・削除したら、`.claude/skills/` の案内ファイルも同じ作業単位で追加・削除します。
- `.claude/` に `.py` などのソースファイルを置かないでください。`tools/dada_check.py` の `code` チェックが `.claude/` を走査対象にするため、未追跡のソースとして検出される可能性があります。
- ここに書いた置き場所・設定名は、Claude Code のバージョンによって変わる場合があります。公式の [メモリ（CLAUDE.md）](https://code.claude.com/docs/en/memory)・[Skills](https://code.claude.com/docs/en/skills)・[Settings](https://code.claude.com/docs/en/settings)・[MCP](https://code.claude.com/docs/en/mcp) が正です。
