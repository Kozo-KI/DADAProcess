---
name: dada-check
description: 開発文書（SW105/SWP6/SW205）とソースコードの機械的な検証を、決定論的なスクリプトへ委譲する手順です。ID対応（REQ↔TC↔UNIT）の照合、曖昧語・表の空欄の走査、未実装ユニットの検出を、AIの推論ではなくコマンド実行で行います。
---

# dada-check（Claude Code 用の案内）

このファイルは Claude Code にスキルを自動発見させるための**案内**です。スキルの本文ではありません。

**今すぐ `.agents/skills/dada-check/SKILL.md` を読み、その手順に従ってください。** 本文・禁止事項・完了条件はすべてそちらが正です。

- 本文中の相対パス（`references/...` など）は `.agents/skills/dada-check/` を起点に解決してください。
- 共通ルールは `.agents/AGENTS.md` です（`CLAUDE.md` から読み込み済みのはずですが、未読なら先に読んでください）。
- 保守メモ: 上の `description` は `.agents/skills/dada-check/SKILL.md` の `description` と同一に保つこと（正は `.agents/` 側）。
