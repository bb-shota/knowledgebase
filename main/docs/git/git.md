# gitの基本的使い方

## ユースケース

### 更新するファイル追加(git add)

```git
git add filename
```

### コミット実行(git commit)

```git
git commit -m "comment"
```

### リモートリポジトリの変更内容を取り込む(git pull)

``` git
git pull origin main
```

### 更新ファイル確認(git status)

``` git
git status
```

### リモートリポジトリの変更(git push)

``` git
git push -u origin main
```

### gitの管理対象から外す(git rm)

#### git command

``` git
git rm --cached file.txt

git rm -r --cached folder/
```

#### .gitignore

``` title=".gitignore"
file.txt
folder/
```

## 参考
- [gitの管理対象から特定のファイルを外す](https://laraweb.net/environment/2929/)