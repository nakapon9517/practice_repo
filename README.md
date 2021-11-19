## 概要
- [A. コミットログ整理（git rebase -i develop）](#a-ログ改変)
- [B. 最新develop取得(git pull --rebase origin develop)](#b-最新develop取得)
- [C. rebaseプッシュ解決(git push --force-with-lease)](#c-rebaseプッシュ解決)
- [D. 強制的にリモートのブランチに合わせる(git reset --hard origin/develop)](#d-強制的にリモートブランチに合わせる)
- [E. 一つ前のコミットを取り消す(git reset --hard HEAD^](#e-一つ前のコミットを取り消す)
- 
- [その他](#その他)
    - [リベースを戻す](#リベースを戻す)
    - [vim](#vim)

## A. ログ改変
コミットログ確認(1行ずつ)
```sh
git log --oneline
```

リベース
```sh
git rebase -i develop // ブランチ指定
git rebase -i aaaaaa  // コミットIDを指定（aaaaaaに、bbbbbbとcccccc をにリベース）
git rebase -i HEAD~3  // コミット履歴から指定（aaaaaaのコミットを残して、bbbbbbとccccccを統合）
```

[コマンド](#コマンド) / [vim](#vim)

- コミットメッセージの修正 ※一番上のコミットのみ残す(p)場合、2行目以下を削除(s)
- リモートブランチのコミットを上書き

```sh
git push -f (--force)
git push --force-with-lease
```
## B. 最新develop取得
最新リモートリポジトリ取得
```sh
git pull --rebase origin develop
```
## C. rebaseプッシュ解決
※[ B-1 ](#B-1)にてエラーが発生した場合
force時にローカルが最新でない場合はエラーとなる
```sh
git push --force-with-lease
```

## D. 強制的にリモートブランチに合わせる
```sh
git fetch origin
git reset --hard origin/develop
```

## E. 一つ前のコミットを取り消す
ここ一旦見てsohtとhardで異なる
https://qiita.com/maejimayuto/items/30bfab250186a00ae884
```sh
git reset --hard HEAD^
```

## その他
### リベースを戻す
```sh
git rebase --abort
```

### コマンド
| コマンド         | 説明 |
| --------------- | ------- |
| (p)pick	        |コミットをそのまま残す。 |
| (r)reword       |コミットメッセージを変更。 |
| (e)edit	        |コミット自体の内容を編集。 |
| (s)squash       |直前のpickを指定したコミットに統合。メッセージも統合。 |
| (f)fixup        |直前のpickを指定したコミットに統合。メッセージは破棄。 |

### vim

| コマンド         | 説明 |
| --------------- | ------- |
| ESC	            | コミットをそのまま残す。 |
| i               | 入力モード |
| ctrl + v               | 短形選択 |
| shife + i               | 短形選択→入力モード |
| ZZ	            | 保存して閉じる |
| :q!	            | 保存せずに終了 |

参考：[よく使う Vim のコマンドまとめ](https://qiita.com/hide/items/5bfe5b322872c61a6896)
