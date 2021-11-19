## Practice git
- [A. コミットログの整理（git rebase -i develop）](#a-ログの改変)
- [B. 最新developの取得(git pull --rebase origin develop)](#b-最新developの取得)
- [C. rebase時のプッシュ解決(git push --force-with-lease)](#c-rebase時のプッシュ解決)
- [D. 強制的にリモートのブランチに合わせる(git reset --hard origin/develop)](#d-強制的にリモートブランチに合わせる)
- [その他](#その他)
    - [リベースを戻す](#リベースを戻す)
    - [vim](#vim)

## A. ログの改変

A-1 コミットログの確認(1行ずつ)

```sh
git log --oneline
```

A-2 リベース
```sh
git rebase -i (--interactive)
```

```sh
git rebase -i develop // ブランチ指定
git rebase -i aaaaaa  // コミットIDを指定（aaaaaaに、bbbbbbとcccccc をにリベース）
git rebase -i HEAD~3  // コミット履歴から指定（aaaaaaのコミットを残して、bbbbbbとccccccを統合）
```
[コマンド](#コマンド)
[vim](#主に使うvimコマンド)

A-3 コミットメッセージの修正
一番上のコミットのみ残す場合、2行目以下を削除する

A-4 リモートブランチのコミットを上書き

```sh
git push -f (--force)
```
<br>

## B. 最新developの取得

B-1 最新のリモートリポジトリ取得
```sh
git pull --rebase origin develop
```

<br>

## C. rebase時のプッシュ解決

※[ B-1 ](#B-1)にてエラーが発生した場合

C-1 force時にローカルが最新でない場合はエラーとなる
```sh
git push --force-with-lease
```

<br>

## D. 強制的にリモートブランチに合わせる

```sh
git fetch origin
git reset --hard origin/master
```

<br>

# その他
### リベースを戻す
```sh
git rebase --abort
```

<br>

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
| ZZ	            | 保存して閉じる |
| :q!	            | 保存せずに終了 |

参考：[よく使う Vim のコマンドまとめ](https://qiita.com/hide/items/5bfe5b322872c61a6896)
