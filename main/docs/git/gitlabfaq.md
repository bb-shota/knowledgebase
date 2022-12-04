# Gitlab FAQ

## パスワードリセット

```
sudo gitlab-rake "gitlab:password:reset[root]"
Enter password: 
Confirm password: 
Password successfully updated for user with username root.
```

- [GitLabの初期パスワード](https://www.gitlab.jp/blog/2022/05/27/initial-password/#%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%83%AA%E3%82%BB%E3%83%83%E3%83%88)

## Gitlab Runner名前解決

```
Preparing environment
00:01
Running on runner-vs5qybyi-project-3-concurrent-0 via 5202a64f8037...
Getting source from Git repository
00:01
Fetching changes with git depth set to 20...
Reinitialized existing Git repository in /builds/bbshota/test/.git/
fatal: unable to access 'http://gitlab.example.com/bbshota/test.git/': Could not resolve host: gitlab.example.com
ERROR: Job failed: exit code 1
```

/etc/gitlab-runnerの config.tomlにextra_hostsを追加する
host名はdocker-compose.yml内で ```hostname: 'gitlab.example.com``` を追加する

```
extra_hosts = ["gitlab.example.com:172.16.238.2"]
```