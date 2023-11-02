## 概要

- [A. コミットログ整理（git rebase -i develop）](#a-ログ改変)
- [B. 最新 develop 取得(git pull --rebase origin develop)](#b-最新develop取得)
- [C. rebase プッシュ解決(git push --force-with-lease)](#c-rebaseプッシュ解決)
- [D. 強制的にリモートのブランチに合わせる(git reset --hard origin/develop)](#d-強制的にリモートブランチに合わせる)
- [E. 一つ前のコミットを取り消す(git reset --hard HEAD^](#e-一つ前のコミットを取り消す)
- [F. 実ファイルを残しつつ過去コミットを取り消す](#f-実ファイルを残しつつ過去コミットを取り消す)
- [G. GitCommitEmoji](https://gist.github.com/parmentf/035de27d6ed1dce0b36a)
- [H. 派生元ブランチを間違えた場合](#h-派生元ブランチを切り替える)
- [I. スタッシュ](#i-スタッシュ)
- [その他](#その他)
  - [リベースを戻す](#リベースを戻す)
  - [vim](#vim)

## A. ログ改変

コミットログ確認(1 行ずつ)

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

- コミットメッセージの修正 ※一番上のコミットのみ残す(p)場合、2 行目以下を削除(s)
- リモートブランチのコミットを上書き

```sh
git push -f (--force)
git push --force-with-lease
```

## B. 最新 develop 取得

最新リモートリポジトリ取得

```sh
git pull --rebase origin develop
```

## C. rebase プッシュ解決

※B-1 にてエラーが発生した場合
force 時にローカルが最新でない場合はエラーとなる

```sh
git push --force-with-lease
```

## D. 強制的にリモートブランチに合わせる

```sh
git fetch origin
git reset --hard origin/develop
```

## E. 一つ前のコミットを取り消す

ここ一旦見て soht と hard で異なる
https://qiita.com/maejimayuto/items/30bfab250186a00ae884

```sh
git reset --hard HEAD^
```

## F. 実ファイルを残しつつ過去コミットを取り消す

```sh
1. git rebase -i develop // 1件目以外を squash して一つのコミットに
2. git reset HEAD^       // 実ファイルはそのままに、1でまとめたコミットを取り消し
3. git add ...           // 意味のある、関連の高いファイル同士のみ選んでコミット
```

## H. 派生元ブランチを切り替える

```
branches
  L develop(正しい派生元)
    L branch-a(作業中)
    L branch-b(誤った派生元)
```

```sh
git rebase --onto origin/develop branch-b branch-a
```

## I. スタッシュ

変更ファイルの退避

```
git stash -u(--include-untracked 新規作成ファイルも退避)
```

退避リストの確認

```
$ git stash list
stash@{0}: WIP on aaaa: xxxx
stash@{1}: WIP on bbbb: xxxx
```

変更を戻す場合

```
git stash apply stash@{0}
```

## その他

### リベースを戻す

```sh
git rebase --abort
```

### コマンド

| コマンド  | 説明                                                     |
| --------- | -------------------------------------------------------- |
| (p)pick   | コミットをそのまま残す。                                 |
| (r)reword | コミットメッセージを変更。                               |
| (e)edit   | コミット自体の内容を編集。                               |
| (s)squash | 直前の pick を指定したコミットに統合。メッセージも統合。 |
| (f)fixup  | 直前の pick を指定したコミットに統合。メッセージは破棄。 |

### vim

| コマンド  | 説明                     |
| --------- | ------------------------ |
| ESC       | コミットをそのまま残す。 |
| i         | 入力モード               |
| ctrl + v  | 短形選択                 |
| shife + i | 短形選択 → 入力モード    |
| ZZ        | 保存して閉じる           |
| :q!       | 保存せずに終了           |

参考：[よく使う Vim のコマンドまとめ](https://qiita.com/hide/items/5bfe5b322872c61a6896)

a
