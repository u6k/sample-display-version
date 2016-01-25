# sample-display-version

Spring Bootのinfoエンドポイントでバージョン情報を表示するサンプルコードです。

## Mavenプロジェクトを作成

Mavenプロジェクトを作成するには、以下のコマンドを実行します。

```
mvn -B archetype:generate \
    -DarchetypeGroupId=org.apache.maven.archetypes \
    -DgroupId=me.u6k.sample \
    -DartifactId=sample-display-version
```

> *NOTE:* [Maven – Maven Getting Started Guide](https://maven.apache.org/guides/getting-started/)

MavenプロジェクトからEclipseプロジェクトを生成するには、以下のコマンドを実行します。

```
mvn eclipse:eclipse
```

生成物をgitコミットから除外するために、`.gitignore`を作成します。

```
/target/
.project
.classpath
```

Eclipseでプロジェクトを開き、コンパイルが成功することを確認します。

> *NOTE:* `-DgroupId`にパッケージ名には使えない文字を指定した場合、コンパイルが失敗するので、フォルダ名やソースコードを修正します。
