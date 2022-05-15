# インストール方法

Docker imageを使用するインストールでGitLab公式ドキュメントを参考に実施。

* [GitLab Docker images](https://docs.gitlab.com/ee/install/docker.html)
* [dockerhub gitlab](https://hub.docker.com/u/gitlab)

## 準備処理

環境変数を追加。

```bash
export GITLAB_HOME=/srv/gitlab
```

## インストール(DockerEngine使用)

上記の環境変数を設定したら

``` docker
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 443:443 --publish 80:80 --publish 22:22 \
  --name gitlab \
  --restart always \
  --volume $GITLAB_HOME/config:/etc/gitlab \
  --volume $GITLAB_HOME/logs:/var/log/gitlab \
  --volume $GITLAB_HOME/data:/var/opt/gitlab \
  --shm-size 256m \
  gitlab/gitlab-ce:latest
```

## 初期化処理

初期化処理を実施。

```bash
sudo docker logs -f gitlab
```

!!! note annotate "処理時間"
    非常に時間がかかるので注意。

## 実行処理

以下を実行。

```bash
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

!!! Warning
    ここで発行されるパスワードは発行してから24時間が有効期限です。

## アクセス

ユーザネームは```root```でパスワードは上記のパスワードで以下にアクセス。
> gitlab.example.com

* [Install the Docker image and start the container](https://docs.gitlab.com/runner/install/docker.html)
