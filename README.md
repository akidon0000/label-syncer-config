# label-syncer-config
このリポジトリは、GitHubのラベルを同期するための設定ファイルを管理するためのリポジトリです。

## 使い方
ラベルを同期したいリポジトリのルートディレクトリに `.github/workflows/label-syncer.yml` を作成し、以下の内容を記述してください。

```label-syncer.yaml
# ラベルを毎週月曜日の午前9時に自動で同期するためのワークフロー
# https://github.com/akidon0000/label-syncer-config を参照してください

name: Sync Labels
on:
    workflow_dispatch:
    schedule:
        - cron: "0 9 * * 1"
        
jobs:
  sync-labels:
    permissions:
      issues: write
    runs-on: ubuntu-latest
    steps:
        - name: Checkout the current repository
          uses: actions/checkout@v4

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

```

## ライセンス
このリポジトリは、MITライセンスの元で公開されています。詳細については、[LICENSE](./LICENSE)を参照してください。
