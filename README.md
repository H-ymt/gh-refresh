# gh-refresh

ブランチ作業のあと、`gh refresh` 一発でデフォルトブランチに戻って最新化し、マージ済みのローカルブランチを掃除する [GitHub CLI](https://cli.github.com/) 拡張です。

```sh
# before
git switch main && git fetch -p && git pull && gh poi

# after
gh refresh
```

シェルに依存しないので、fish / zsh / bash どの環境でも同じ操作を実行できます。

## インストール

```sh
gh extension install H-ymt/gh-refresh
```

## 使い方

Git リポジトリ内で実行するだけです。

```sh
gh refresh
```

実行すると、デフォルトブランチへ切り替えてリモートの最新を取り込み、マージ済みのローカルブランチを掃除します。

## 任意依存

- [`gh poi`](https://github.com/seachicken/gh-poi): マージ済みブランチの掃除に使います。未インストールでも `gh refresh` は成功します（掃除だけスキップ）。

  ```sh
  gh extension install seachicken/gh-poi
  ```

## 動作の詳細

`gh refresh` は次を順に行います。

1. `origin/HEAD` からデフォルトブランチを特定（ネットワーク不要。未設定なら `git remote set-head` で一度だけセット）
2. デフォルトブランチへ `git switch`
3. `git fetch -p`（リモートで消えた追跡ブランチを prune）
4. `git pull origin <default>`
5. `gh poi` があれば実行し、マージ済みのローカルブランチを掃除

> dotfiles の fish 関数 `gbase` を gh extension 化したものです。

## ライセンス

[MIT](./LICENSE)
