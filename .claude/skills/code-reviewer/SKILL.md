---
name: code-reviewer
description: DADAプロセスのPhase 4（実装・総合テスト報告）の自己校正（Self-Correction）で使用するペルソナスキルです。ソースコードがコーディング規約と品質基準に準拠しているかをレビューし、欠陥をバグ管理表（BUG101）に記録します。総合テスト報告書のレビューは test-reviewer が担当します。
---

# code-reviewer（Claude Code 用の案内）

このファイルは Claude Code にスキルを自動発見させるための**案内**です。スキルの本文ではありません。

**今すぐ `.agents/skills/code-reviewer/SKILL.md` を読み、その手順に従ってください。** 本文・禁止事項・完了条件はすべてそちらが正です。

- 本文中の相対パス（`references/...` など）は `.agents/skills/code-reviewer/` を起点に解決してください。
- 共通ルールは `.agents/AGENTS.md` です（`CLAUDE.md` から読み込み済みのはずですが、未読なら先に読んでください）。
- 保守メモ: 上の `description` は `.agents/skills/code-reviewer/SKILL.md` の `description` と同一に保つこと（正は `.agents/` 側）。
