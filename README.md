# practice_repo

#### リモートからリポジトリを取得
```sh
git clone
```

#### ローカルでリポジトリ作成
```sh
git init
```


# 以下でGitのログを改変する

## A-1 コミットログの確認(1行ずつ)

```sh
git log --oneline
```
>`cccccc c [comme-id, commit-message]`<br>
`bbbbbb b`<br>
`aaaaaa a`


## A-2 cとbを a にリベースする場合
```sh
git rebase -i aaaaaa
```

## A-3 指示コマンドを指定
```sh
git rebase -i (--interactive)
```

>`pick bbbbbb b [command, comme-id, commit-message]`<br>
`pick cccccc c`<br>


| コマンド         | 説明 |
| --------------- | ------- |
| (p)pick	        |コミットをそのまま残す。 |
| (r)reword       |コミットメッセージを変更。 |
| (e)edit	        |コミット自体の内容を編集。 |
| (s)squash       |直前のpickを指定したコミットに統合。メッセージも統合。 |
| (f)fixup        |直前のpickを指定したコミットに統合。メッセージは破棄。 |
[vimコマンドはこちら](#主に使うvimコマンド)

## A-4 リモートブランチのコミットを上書き

```sh
git push -f (--force)
```

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