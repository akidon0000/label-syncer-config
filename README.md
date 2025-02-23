# label-syncer-config
このリポジトリは、GitHubのラベルを同期するための設定ファイルを管理するためのリポジトリです。

## 使い方

詳細は [micnncim/action-label-syncer](https://github.com/micnncim/action-label-syncer) をご覧ください。

ラベルを同期したいリポジトリのルートディレクトリに `.github/workflows/label-syncer.yml` を作成し、以下の内容を記述してください。

※ ラベル上書き機能をオンにするには `prune: true`

```label-syncer.yaml
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
            prune: false
```

## 謝辞
[micnncim/action-label-syncer](https://github.com/micnncim/action-label-syncer)


## ライセンス
このリポジトリは、MITライセンスの元で公開されています。詳細については、[LICENSE](./LICENSE)を参照してください。
