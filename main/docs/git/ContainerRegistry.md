## コンテナレジストリ

DockerDocumentを見ながらやれば基本的にはできる。  

## Registry Install

```
docker run -d -p 5000:5000 --name registry registry:2
```

```
docker pull ubuntu
```

```
docker image tag ubuntu localhost:5000/myfirstimage
docker push localhost:5000/myfirstimage
```

## Docker Registry API

### 一覧取得

```
curl http://localhost:5000/v2/_catalog
```

```
StatusCode        : 200
StatusDescription : OK
Content           : {"repositories":["dearpygui_python3","ubuntu"]}

RawContent        : HTTP/1.1 200 OK
                    Docker-Distribution-Api-Version: registry/2.0
                    X-Content-Type-Options: nosniff
                    Content-Length: 48
                    Content-Type: application/json; charset=utf-8
                    Date: Sat, 03 Dec 2022 08:05:53 GMT...
Forms             : {}
Headers           : {[Docker-Distribution-Api-Version, registry/2.0], [X-Content-Type-Options,
                     nosniff], [Content-Length, 48], [Content-Type, application/json; charset=
                    utf-8]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
```

```
curl http://localhost:5000/v2/ubuntu/tags/list
```

```
StatusCode        : 200
StatusDescription : OK
Content           : {"name":"ubuntu","tags":["latest"]}

RawContent        : HTTP/1.1 200 OK
                    Docker-Distribution-Api-Version: registry/2.0
                    X-Content-Type-Options: nosniff
                    Content-Length: 36
                    Content-Type: application/json; charset=utf-8
                    Date: Sat, 03 Dec 2022 08:06:03 GMT...
Forms             : {}
Headers           : {[Docker-Distribution-Api-Version, registry/2.0], [X-Content-Type-Options,
                     nosniff], [Content-Length, 36], [Content-Type, application/json; charset=
                    utf-8]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 36
```

## 参考

- [Docker Registryを構築する](https://qiita.com/Brutus/items/da63d23be32d505409c6)
- [Docker Registry](https://docs.docker.com/registry/)
- [GitLab Container Registry](https://docs.gitlab.com/ee/user/packages/container_registry/)
- [GitLab Container Registry administration](https://docs.gitlab.com/ee/administration/packages/container_registry.html)

- [gitlabのコンテナレジストリ](https://qiita.com/infra_buld/items/cc4acfe70ec22b5ba82a)
- [GitLab Container Registry](https://qiita.com/masakura/items/802f4b8ce322d2543c80)
- [https://qiita.com/tukiyo3/items/2ca5b1eddd455e333016](https://qiita.com/tukiyo3/items/2ca5b1eddd455e333016)
- [GitLabによるDockerコンテナレジストリの使い方](https://www.nagarelab.com/ja/3501)
- [proxy環境下でDocker Registryの構築](https://qiita.com/kanegoon/items/e250c0a328673b0fca82)