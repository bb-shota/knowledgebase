# Gitlab CI/CD 導入

## docker-compose.yml

GitlabとGitlab runnerを同じネットワーク上に追加するため、docker-compose.ymlに記載する。

'''
version: '3'
services:
  gitlab:
    image: 'gitlab/gitlab-ee:latest'
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.example.com'
        gitlab_rails['gitlab_shell_ssh_port'] = 2222
        nginx['listen_port'] = 80
    ports:
      - '8080:80'
      - '22:22'
      - '443:443'
      
    volumes:
      - 'D:\01_ws\20221127_Gitlab\config:/etc/gitlab'
      - 'D:\01_ws\20221127_Gitlab\logs:/var/log/gitlab'
      - 'D:\01_ws\20221127_Gitlab\data:/var/opt/gitlab'
    shm_size: '256m'
    networks:
        gitlab_net:
            ipv4_address: 172.16.238.2
  gitlab-runner:
    image: 'gitlab/gitlab-runner:latest'
    restart: always
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
    ports:
      - "8093:8093"
    depends_on:
        - gitlab
    networks:
        gitlab_net:
            ipv4_address: 172.16.238.3

networks:
    gitlab_net:
        ipam:
            config:
            - subnet: 172.16.238.0/24


'''

- [Dockerを用いたGitLab Runnerのオンプレミス構築](https://e-penguiner.com/build-gitlab-runner-with-docker/)
- [Dockerコンテナでgitlabとgitlab-runnerを構築してCI/CD](https://syachiku.net/docker-gitlab-gitlab-runner/)
## gitlab runner登録

'''
docker exec -it <コンテナ名> gitlab-runner register --non-interactive --locked=false --url=<GitlabURL> --registration-token=<Gitlabで取得したトークン> --name=container-runner --tag-list=tag-runner --executor=docker --docker-privileged=true --docker-image=docker:20.10.15-dind
'''


- [Registering runners](https://docs.gitlab.com/runner/register/index.html#docker)
- [Dockerを用いたGitLab Runnerのオンプレミス構築](https://e-penguiner.com/build-gitlab-runner-with-docker/)

## 参考

- [GitLabを使ったCI/CD入門](https://gitlab-docs.creationline.com/ee/ci/introduction/)
- [GitLab CI/CD 基本編 ～チュートリアルで感覚を掴む～](https://www.insight-tec.com/tech-blog/cicd/20200929_gitlab/)
- [オンプレの GitLab サーバーに GitLab Runner を同居させて GitLab CI/CD を動かす（Docker編](https://qiita.com/n11sh1/items/f44764c74aca5c3bcfa1)
- [Dockerを用いたGitLab Runnerのオンプレミス構築](https://e-penguiner.com/build-gitlab-runner-with-docker/)
- [Docker Compose で GitLab + GitLab Runner の環境を整える](https://mikoto2000.blogspot.com/2018/07/docker-compose-gitlab-gitlab-runner.html)
- [GitとCI/CDに関する知識ゼロのSEが、GitLabでRunner (Docker) を登録するだけの話 (2022/09/26 改訂)](https://blogs.networld.co.jp/entry/2022/03/10/090000)


- [gitlab-ciでCouldn't resolve hostがでるとき](https://qiita.com/tsgkdt/items/67d5fb06ae9542966ed6)