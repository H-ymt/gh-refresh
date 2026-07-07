# gh-refresh

デフォルトブランチへ切り替えて最新化し、マージ済みのローカルブランチを掃除する [GitHub CLI](https://cli.github.com/) 拡張です。

dotfiles の fish 関数 `gbase` を gh extension 化したもので、シェルに依存せずどの環境でも `gh refresh` で同じ操作を実行できます。

## インストール

```sh
gh extension install H-ymt/gh-refresh
```

## 使い方

Git リポジトリ内で実行します。

```sh
gh refresh
```

以下を順に行います。

1. `origin/HEAD` からデフォルトブランチを特定（ネットワーク不要で高速。未設定なら `git remote set-head` で一度セット）
2. デフォルトブランチへ `git switch`
3. `git fetch -p`（リモートで消えた追跡ブランチを prune）
4. `git pull origin <default>`
5. [`gh poi`](https://github.com/seachicken/gh-poi) がインストールされていれば実行し、マージ済みのローカルブランチを掃除

## 任意依存

- [`gh poi`](https://github.com/seachicken/gh-poi): マージ済みブランチの掃除に使用します。未インストールでも `gh refresh` は成功します。

  ```sh
  gh extension install seachicken/gh-poi
  ```

## ライセンス

[MIT](./LICENSE)
