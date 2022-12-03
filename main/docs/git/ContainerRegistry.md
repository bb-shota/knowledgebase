## コンテナレジストリ

DockerDocumentを見ながらやれば基本的にはできる。  

## Registry Install

'''
docker run -d -p 5000:5000 --name registry registry:2
'''

'''
docker pull ubuntu
'''

'''
docker image tag ubuntu localhost:5000/myfirstimage
docker push localhost:5000/myfirstimage
'''
## 参考

- [Docker Registryを構築する](https://qiita.com/Brutus/items/da63d23be32d505409c6)
- [Docker Registry](https://docs.docker.com/registry/)

- [gitlabのコンテナレジストリ](https://qiita.com/infra_buld/items/cc4acfe70ec22b5ba82a)
- [GitLab Container Registry](https://qiita.com/masakura/items/802f4b8ce322d2543c80)