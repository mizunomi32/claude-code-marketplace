# Claude Code プラグイン マーケットプレイス

このリポジトリは、Claude Code のプラグインを自社内で配布するためのマーケットプレイスです。

## 概要

Claude Code のプラグイン、スラッシュコマンド、サブエージェント、MCPサーバー、フックなどを一元管理し、組織内で共有するためのリポジトリです。

## ディレクトリ構造

```
.
├── .claude-plugin/
│   └── marketplace.json          # マーケットプレイス定義
├── plugins/                       # 各メンバーのプラグインディレクトリ
│   ├── sample/                    # メンバー別ディレクトリ
│   │   ├── .claude-plugin/
│   │   │   └── plugin.json        # プラグインマニフェスト
│   │   ├── commands/              # スラッシュコマンド
│   │   ├── agents/                # サブエージェント
│   │   ├── skills/                # Agent Skills（オプション）
│   │   └── hooks/                 # フック（オプション）
│   └── {member_name}/
└── README.md
```

## プラグインの作成

### 新規プラグインの追加手順

1. `plugins/{member_name}/` ディレクトリを作成
2. `plugins/{member_name}/.claude-plugin/plugin.json` を作成
3. 必要に応じて以下のディレクトリを作成し、ファイルを追加
   - `commands/` - スラッシュコマンド（.mdファイル）
   - `agents/` - サブエージェント（.mdファイル）
   - `skills/` - Agent Skills（.mdファイル）
   - `hooks/` - フック（.jsonファイル）

### plugin.json の例

```json
{
  "name": "sample",
  "version": "1.0.0",
  "description": "Sample plugin",
  "author": "Your Name",
  "commands": [
    {
      "name": "hello",
      "description": "Hello world command"
    }
  ],
  "agents": [
    {
      "name": "code-reviewer",
      "description": "Code review agent"
    }
  ]
}
```

### スラッシュコマンドの例 (`commands/hello.md`)

```markdown
---
name: hello
description: Hello world command
---

Hello, World!
```

### サブエージェントの例 (`agents/code-reviewer.md`)

```markdown
---
name: code-reviewer
description: Code review agent
---

You are a code reviewer. Review the code for potential issues.
```

## マーケットプレイスへの登録

`.claude-plugin/marketplace.json` に新しいプラグインを追加します。

```json
{
  "name": "company-plugins",
  "owner": {
    "name": "Dev Team",
    "email": "dev@example.com"
  },
  "plugins": [
    {
      "name": "sample",
      "source": "./plugins/sample",
      "description": "Sample plugin",
      "version": "1.0.0"
    },
    {
      "name": "{plugin-name}",
      "source": "./plugins/{member_name}",
      "description": "{description}",
      "version": "{version}"
    }
  ]
}
```

## インストール方法

### マーケットプレイスの追加

```bash
/plugin marketplace add {owner}/{repo}
```

### プラグインのインストール

```bash
/plugin install {plugin-name}@company-plugins
```

## メンテナンス

### プラグインの更新

1. プラグインの内容を変更
2. `plugin.json` のバージョンを更新
3. `marketplace.json` のバージョン情報を更新
4. ユーザーは `/plugin update {plugin-name}` で更新可能

### プラグインの削除

1. プラグインディレクトリを削除
2. `marketplace.json` から該当のエントリを削除

## 参考資料

- [Plugins](https://docs.claude.com/en/docs/claude-code/plugins)
- [Plugins Reference](https://docs.claude.com/en/docs/claude-code/plugins-reference)
- [Plugin Marketplaces](https://docs.claude.com/en/docs/claude-code/plugin-marketplaces)
- [スラッシュコマンド](https://docs.claude.com/ja/docs/claude-code/slash-commands)
- [サブエージェント](https://docs.claude.com/ja/docs/claude-code/sub-agents)
- [MCP](https://docs.claude.com/ja/docs/claude-code/mcp)
- [フックガイド](https://docs.claude.com/ja/docs/claude-code/hooks-guide)
