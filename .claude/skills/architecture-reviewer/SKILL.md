---
name: architecture-reviewer
description: DADAプロセスのPhase 3（アーキテクチャ設計）の自己校正（Self-Correction）で使用するペルソナスキルです。設計書（SW205）の要求網羅性・テスト実行可能性・保守性をレビューし、指摘をレビュー記録表（REV101_Design）に記録します。
---

# architecture-reviewer（Claude Code 用の案内）

このファイルは Claude Code にスキルを自動発見させるための**案内**です。スキルの本文ではありません。

**今すぐ `.agents/skills/architecture-reviewer/SKILL.md` を読み、その手順に従ってください。** 本文・禁止事項・完了条件はすべてそちらが正です。

- 本文中の相対パス（`references/...` など）は `.agents/skills/architecture-reviewer/` を起点に解決してください。
- 共通ルールは `.agents/AGENTS.md` です（`CLAUDE.md` から読み込み済みのはずですが、未読なら先に読んでください）。
- 保守メモ: 上の `description` は `.agents/skills/architecture-reviewer/SKILL.md` の `description` と同一に保つこと（正は `.agents/` 側）。
