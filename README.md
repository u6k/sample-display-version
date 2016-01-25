# sample-display-version

Spring Bootのinfoエンドポイントでバージョン情報を表示するサンプルコードです。

## 目的

動作しているSpring Bootアプリのバージョンが何かを外部から確認したい場合がありますが、infoエンドポイントで簡単にバージョン情報などを返すことができます。

## Mavenプロジェクトを作成

```
mvn -B archetype:generate \
    -DarchetypeGroupId=org.apache.maven.archetypes \
    -DgroupId=me.u6k.sample \
    -DartifactId=sample-display-version
```

> *NOTE:* [Maven – Maven Getting Started Guide](https://maven.apache.org/guides/getting-started/)

MavenプロジェクトからEclipseプロジェクトを生成します。

```
mvn eclipse:eclipse
```

`.gitignore`を作成します。

```
/target/
.project
.classpath
```

Eclipseでプロジェクトを開き、コンパイルが成功することを確認します。

> *NOTE:* `-DgroupId`にパッケージ名には使えない文字を指定した場合、コンパイルが失敗するので、フォルダ名やソースコードを修正します。

## Spring Bootアプリケーションに仕立てる

`pom.xml`を修正して、Spring Bootアプリケーションに仕立てます。詳細は`pom.xml`を参照。

`pom.xml`を修正後、Eclipseプロジェクトに設定を反映するため、`mvn eclipse:eclipse`を実行します。

Spring Bootアプリケーションとして起動するため、`App`クラスを修正します。詳細は`pom.xml`を参照。

## infoエンドポイントにアクセスしてみる

とりあえず素のSpring Bootアプリケーションとなったので、起動してみます。

```
mvn spring-boot:run
```

起動が完了したら、infoエンドポイントにアクセスしてみます。spring-boot-actuatorが有効になっているので`200 OK`が帰りますが、ボディは空JSONになります。

```
$ curl -v http://localhost:8080/info
> GET /info HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.45.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Server: Apache-Coyote/1.1
< X-Application-Context: application
< Content-Type: application/json;charset=UTF-8
< Transfer-Encoding: chunked
< Date: Mon, 25 Jan 2016 08:21:37 GMT
<
{}
```

## 設定ファイルにinfoで返す値を記載する

infoエンドポイントで返す値は、`application.properties`に`info.`で始まるプロパティを記述することで設定できます。`maven-resources-plugin`で`pom.xml`のプロパティで`application.properties`を置換することで、アプリ名やバージョン情報をinfoエンドポイントで返すことが出来ます。

`application.properties`に以下を記載します。

```
info.name=${project.artifactId}
info.version=${project.version}
```

アプリを起動します。

```
mvn spring-boot:run
```

先程と同様にinfoエンドポイントにアクセスすると、今度はアプリ名とバージョン情報が返ることが確認できます。

```
$ curl -v http://localhost:8080/info
> GET /info HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.45.0
> Accept: */*
>
< HTTP/1.1 200 OK
< Server: Apache-Coyote/1.1
< X-Application-Context: application
< Content-Type: application/json;charset=UTF-8
< Transfer-Encoding: chunked
< Date: Mon, 25 Jan 2016 08:26:15 GMT
<
{"name":"sample-display-version","version":"1.0-SNAPSHOT"}
```
