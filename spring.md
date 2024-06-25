---


---


---

Javalinは軽量でシンプルなJavaのWebフレームワークです。Spring Initializrを使ってSpring BootプロジェクトにJavalinを統合し、index.htmlをホストする方法について説明します。

### 手順

1. **Spring Initializrでプロジェクトを作成する**

   - Webサービスに必要な依存関係を持った新しいSpring Bootプロジェクトを作成します。Spring Initializrにアクセスし、以下の設定を行います：
     - Project: Maven Project
     - Language: Java
     - Spring Boot: 最新の安定版を選択
     - Group、Artifact: 自由に設定してください
     - Dependencies: Web (これはSpring MVCを含みます)

   Spring Initializrにアクセスするには、ブラウザで `https://start.spring.io/` を開きます。

2. **プロジェクトをダウンロードまたは生成する**

   必要な依存関係（主にSpring Web）を選択したら、"Generate"ボタンをクリックしてプロジェクトを生成し、ZIPファイルとしてダウンロードします。

3. **プロジェクトを展開し、Javalinの統合を追加する**

   ダウンロードしたZIPファイルを展開し、IDEで開きます。`pom.xml`（Mavenプロジェクト）または`build.gradle`（Gradleプロジェクト）を開き、Javalinの依存関係を追加します。

   - Mavenの場合（`pom.xml`）：

     ```xml
     <dependency>
         <groupId>io.javalin</groupId>
         <artifactId>javalin</artifactId>
         <version>4.0.0</version> <!-- 最新のバージョンに置き換えてください -->
     </dependency>
     ```

   - Gradleの場合（`build.gradle`）：

     ```groovy
     implementation 'io.javalin:javalin:4.0.0' // 最新のバージョンに置き換えてください
     ```

   依存関係を追加したら、ビルドツールを使用して依存関係を解決します。

4. **Javalinでindex.htmlをホストする設定**

   Javalinを使用して、index.htmlをホストするために以下のようにコードを追加します。

   ```java
   import io.javalin.Javalin;
   import static io.javalin.apibuilder.ApiBuilder.*;

   public class MyApp {
       public static void main(String[] args) {
           Javalin app = Javalin.create(config -> {
               config.addStaticFiles("/public"); // index.htmlなどの静的ファイルを配置するディレクトリ
           }).start(7000); // ポート番号は適宜変更可能

           app.routes(() -> {
               get("/", ctx -> ctx.redirect("/index.html")); // ルートへのアクセスをindex.htmlにリダイレクト
           });
       }
   }
   ```

   - `addStaticFiles("/public")`は、`/public`ディレクトリに静的ファイルを配置することを示しています。このディレクトリには`index.html`などのファイルを配置します。

   - `get("/", ctx -> ctx.redirect("/index.html"))`は、ルートパス(`/`)へのアクセスを`index.html`にリダイレクトする設定です。

5. **プロジェクトのビルドと実行**

   IDEやコマンドラインでプロジェクトをビルドし、Javalinのアプリケーションを起動します。これにより、指定したポート（例：7000）でアプリケーションが実行され、`index.html`がホストされます。

6. **ブラウザで確認**

   ブラウザで `http://localhost:7000/` にアクセスし、`index.html`が正しく表示されることを確認します。

以上が、Spring Initializrを使用してJavalinをSpring Bootプロジェクトに統合し、`index.html`をホストする手順です。

---
