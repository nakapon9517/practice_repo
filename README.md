- A. ログの改変
- B. 最新develop取得(git pull --rebase origin develop)
- C. rebase時のプッシュ解決(git push --force-with-lease)

# 以下でGitのログを改変する

## A-1 コミットログの確認(1行ずつ)

```sh
git log --oneline

[コミットID, コミットメッセージ]
```
`cccccc c`<br>
`bbbbbb b`<br>
`aaaaaa a`


## A-2 リベース
```sh
git rebase -i (--interactive)

[コマンド, コミットID, コミットメッセージ]
```
`pick bbbbbb b`<br>
`pick cccccc c`<br>
`pick aaaaaa a`<br>

1. コミットIDを指定（aaaaaaに、bbbbbbとcccccc をにリベース）

```sh
git rebase -i aaaaaa
```
`pick bbbbbb b`<br>
`pick cccccc c`<br>

2. コミット履歴から指定（aaaaaaのコミットを残して、bbbbbbとccccccを統合）
```sh
git rebase -i HEAD~3
```
`pick aaaaaa a`<br>
`s bbbbbb b`<br>
`s cccccc c`<br>


| コマンド         | 説明 |
| --------------- | ------- |
| (p)pick	        |コミットをそのまま残す。 |
| (r)reword       |コミットメッセージを変更。 |
| (e)edit	        |コミット自体の内容を編集。 |
| (s)squash       |直前のpickを指定したコミットに統合。メッセージも統合。 |
| (f)fixup        |直前のpickを指定したコミットに統合。メッセージは破棄。 |

[vimはこちら](#主に使うvimコマンド)

## A-3 コミットメッセージの修正
一番上のコミットのみ残す場合、2行目以下を削除する

## A-4 リモートブランチのコミットを上書き

```sh
git push -f (--force)
```
---

## 最新developの取得(git pull --rebase origin develop)

# その他
## リベースを削除して戻す
```sh
git rebase --abort
```

## 主に使うvimコマンド

| コマンド         | 説明 |
| --------------- | ------- |
| ESC	            | コミットをそのまま残す。 |
| i               | 入力モード |
| ZZ	            | 保存して閉じる |
| :q!	            | 保存せずに終了 |

参考：[よく使う Vim のコマンドまとめ](https://qiita.com/hide/items/5bfe5b322872c61a6896)