# DADA Process（Claude Code 用の案内）

このプロジェクトのルール本文は `.agents/AGENTS.md` です。次の行で会話の最初に読み込まれます。未読のときは、作業を始める前に必ずそのファイルを読み、以降はそれに従ってください。

@.agents/AGENTS.md

## スキルの場所

- スキルの本文は `.agents/skills/` にあります（**正**）。
- `.claude/skills/` には、Claude Code がスキルを自動発見するための**案内ファイル**だけを置いています。案内ファイルは、対応する `.agents/skills/<name>/SKILL.md` を読むよう指示するだけで、本文を持ちません。
- ソフトウェアの新規開発・機能追加・修正・バグ対応では、必ず `.agents/skills/dada-process/SKILL.md` を読んでから進めてください。各工程では、そこに書かれたペルソナスキル（同じ `.agents/skills/` 配下）を読んでください。

## Claude Code での読み替え

`.agents/` の本文は Antigravity を前提に書かれています。Claude Code では次のとおり読み替えてください。本文そのものは書き換えないでください。

| `.agents/` の記述 | Claude Code での読み替え |
| :--- | :--- |
| サブエージェント起動ツール（`invoke_subagent` 等） | **Agent ツール**（サブエージェント起動。旧称 Task ツール）。これがあれば動作モードは **ツールが自動的にサブエージェントを作る**、`context-reset` は **方式A** |
| エージェント開発/実行ツール（Antigravity 2.0 / CLI） | Claude Code（CLI / IDE 拡張 / デスクトップ） |
| 全プロジェクト共通の設定（`~/.gemini/...`） | `~/.claude/`（ただし DADA の設定はこのリポジトリ内に閉じる） |
| MCP 設定（`~/.gemini/config/mcp_config.json`） | リポジトリ直下の `.mcp.json`（context7 を登録済み。API キーは環境変数 `CONTEXT7_API_KEY`） |
| Antigravity 2.0 専用の `/goal`、`/grill-me` | 使わない。同じ意図は通常のチャット指示で伝える |
| 自動実行ポリシー（P開発自律型 / A開発自律型） | 作業ブランチを切ってから、権限モードを `acceptEdits` にする（`Shift+Tab` で切替）。必要な Bash の許可は `.claude/settings.json` |
| 起動コマンド `python` | 環境により `python3` または `py -3` |

## 新しいスキルを作ったとき（A開発）

エージェント定義の開発で `.agents/skills/<name>/SKILL.md` を新規作成したら、同じ作業単位の中で `.claude/skills/<name>/SKILL.md` に案内ファイルを追加してください（既存の案内ファイルと同じ形式。`name` と `description` は `.agents/` 側と一字一句同じにする）。これは `.agents/AGENTS.md` 第9節「単一情報源」「変更時の同時修正」の適用です。

## 触らないもの

- `docs/` の工程・ひな形・ガイドライン（ASDoQ 文書品質モデルを含む）
- `tools/` の点検ツール
- `.agents/` の本文を、Claude Code 向けに別内容へ書き換えること
