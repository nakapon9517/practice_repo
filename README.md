## Practice git
- [A. ログの改変（git rebase -i develop）](#a-ログの改変)
    - [A-1 コミットログの確認(1行ずつ)](#a-1-コミットログの確認1行ずつ)
    - [A-2 リベース](#a-2-リベース)
    - [A-3 コミットメッセージの修正](#a-3-コミットメッセージの修正)
    - [A-4 リモートブランチのコミットを上書き](#a-4-リモートブランチのコミットを上書き)
- [B. 最新developの取得(git pull --rebase origin develop)](#b-最新developの取得git-pull---rebase-origin-develop)
    - [B-1 最新のリモートリポジトリ取得](#b-1-最新のリモートリポジトリ取得)
- [C. rebase時のプッシュ解決(git push --force-with-lease)](#c-rebase時のプッシュ解決git-push---force-with-lease)
    - [C-1 force時にローカルが最新でない場合はエラーとなる](#c-1-force時にローカルが最新でない場合はエラーとなる)
- [その他](#その他)
    - [リベースを戻す](#リベースを戻す)
    - [vim](#vim)

# A. ログの改変

### A-1 コミットログの確認(1行ずつ)

```sh
git log --oneline

[コミットID, コミットメッセージ]
```


### A-2 リベース
```sh
git rebase -i (--interactive)

[コマンド, コミットID, コミットメッセージ]
```

```sh
git rebase -i aaaaaa // コミットIDを指定（aaaaaaに、bbbbbbとcccccc をにリベース）
git rebase -i HEAD~3 // コミット履歴から指定（aaaaaaのコミットを残して、bbbbbbとccccccを統合）
```

| コマンド         | 説明 |
| --------------- | ------- |
| (p)pick	        |コミットをそのまま残す。 |
| (r)reword       |コミットメッセージを変更。 |
| (e)edit	        |コミット自体の内容を編集。 |
| (s)squash       |直前のpickを指定したコミットに統合。メッセージも統合。 |
| (f)fixup        |直前のpickを指定したコミットに統合。メッセージは破棄。 |

[vimはこちら](#主に使うvimコマンド)

### A-3 コミットメッセージの修正
一番上のコミットのみ残す場合、2行目以下を削除する

### A-4 リモートブランチのコミットを上書き

```sh
git push -f (--force)
```
<br>

# B. 最新developの取得(git pull --rebase origin develop)

### B-1 最新のリモートリポジトリ取得
```sh
git pull --rebase origin develop
```

<br>

# C. rebase時のプッシュ解決(git push --force-with-lease)

※[ B-1 ](#B-1)にてエラーが発生した場合

### C-1 force時にローカルが最新でない場合はエラーとなる
```sh
git push --force-with-lease
```

<br>

# その他
### リベースを戻す
```sh
git rebase --abort
```

<br>

### vim

| コマンド         | 説明 |
| --------------- | ------- |
| ESC	            | コミットをそのまま残す。 |
| i               | 入力モード |
| ZZ	            | 保存して閉じる |
| :q!	            | 保存せずに終了 |

参考：[よく使う Vim のコマンドまとめ](https://qiita.com/hide/items/5bfe5b322872c61a6896)
