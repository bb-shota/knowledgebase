# Githubにデプロイする

## Github Page作り方
Github上でリポジトリをすでに作成済の場合を想定。  
以下のコマンドをターミナル上で実行することでGithubPageにデプロイできる。  

```bash
mkdocs gh-deploy  
```

このコマンドは以下のことを行っているよう。  
> Behind the scenes, MkDocs will build your docs and use the ghp-import tool to commit them to the gh-pages branch and push the gh-pages branch to GitHub.  

引用元 (https://www.mkdocs.org/user-guide/deploying-your-docs/)  

つまりローカルリポジトリでgh-pagesブランチにコミットし、それをGithub上のgh-pagesブランチにプッシュし、このブランチをGithub Pagesに公開するように自動で設定しているみたい。  

## 参考

- [Mkdocs Deploying your docs](https://www.mkdocs.org/user-guide/deploying-your-docs/)

- [mkdocsを使ったGitHub Pagesの作成方法](https://aiedoc.github.io/note/Tips/Mkdocs/mkdocs%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%9FGitHubPages/)