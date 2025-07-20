# label-syncer-config

このリポジトリは、GitHub リポジトリ間でラベルを同期するための **設定ファイル（YAML）管理 リポジトリ**です。  
GitHub Actions と [micnncim/action-label-syncer](https://github.com/micnncim/action-label-syncer) を組み合わせて、統一されたラベルを複数のリポジトリに展開できます。

## 使い方

ラベルを同期したい任意のリポジトリに、以下の GitHub Actions ワークフローを `.github/workflows/label-syncer.yml` として作成してください。

> 💡 `prune: true` を設定すると、**同期対象ファイルに存在しないラベルはリポジトリから削除されます**（上書きモード）

```yaml
# https://github.com/akidon0000/label-syncer-config を参照

name: Sync Labels

on:
  workflow_dispatch:

jobs:
  sync-labels:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout the label-syncer-config repository
        uses: actions/checkout@v4
        with:
          repository: akidon0000/label-syncer-config
          path: label-syncer-config

      - name: Sync labels
        uses: micnncim/action-label-syncer@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          manifest: label-syncer-config/base-labels.yml
          prune: false  # true にすると差分削除も行われます
```

## 管理対象ファイル
このリポジトリでは、同期対象となるラベル定義を `base-labels.yml` ファイルとして管理しています。

このファイルには以下のようなラベル情報が定義されています。

```
- ADR 🏯
- bugs 🐞
- chore 🏠
- design 🏯
- docs ✍️
- enhancement 🚀
- high priority 🔥
- low priority 🏕️
- question❓
- refactoring 🧰
- renovate 🤖
- testing ✅
```


## 謝辞
[micnncim/action-label-syncer](https://github.com/micnncim/action-label-syncer)


## ライセンス
このリポジトリは、MITライセンスの元で公開されています。詳細については、[LICENSE](./LICENSE)を参照してください。
