# アプリ開発環境

DockerのContainerとして、Jenkins, Apache2, Swagger, Swagger Stub Serverを構築するためのDockerfile及びdocker-compose.yml等のファイル群です。

nginxから各サーバーにリバースプロキシして開放するポートは1つになるようにしています。

# ネットワーク
Dockerはデフォルトで、172.17.x.xのIPを割り振るので, 普段使っているIPと重複してたりすると以下の作業が必要.

+ `docker0`を削除するのと, 新しくネットワーク
+ 新しくネットワークを作ってそれをContainerが使うようにする

# 各Container
## VolumeContainer

### httpd_volume

Apacheの公開用ファイルのVolumeContainer. Jenkins, Apache2が参照できる.

### jenkins_volume

jenkinsで使うVolumeContainer. Jenkinsが参照できる.

### android_sdk

AndroidSDKが展開されているVolumeContainer.　Jenkinsが参照できる.

## Jenkins
Jenkins2.xです.

**FIXME**

+ jenkins/jenkinsを編集してnginxが待ち受けるポートと同じポートになるように修正する

## Apache

**FIXME**

+ httpd/ports.confを編集してnginxが待ち受けるポートと同じポートになるように修正する
+ httpd/000-default.confを編集してnginxが待ち受けるポートと同じポートになるように修正する
+ httpd/Dockerfileを編集して公開用ディレクトリにVolumeContainerを参照するシンボリックリンクを作成するようにする

## Swagger Stub Server
デフォルトでSwaggerの公式サンプルを動かす様にしようとしていたが、VolumeContainer経由でJenkinsから更新できるようにすると
imageのbuild時に追加したファイルが読み取れないので、swaggerで作るserverスクリプトは手作業で追加・実行するようにする.

Jenkinsで更新したときに再起動が不要になるように`node-dev index.js`で実行する.

**FIXME**

+ Swaggerで作成されるnodejsのプロジェクトがnginxが待ち受けるポートと同じポートになるように修正する

## nginx

+ proxy/default.confを編集して各Containerへのリバースプロキシの設定を行う.（ポートの変更だけで良い)
