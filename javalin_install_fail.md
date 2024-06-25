javalin


---
---
---

以下に、Gradleを使ってJavaプロジェクトにJavalinフレームワークをインストールし、`myapp` フォルダに配置された `index.html` をホストする方法を説明します。

### 手順

1. **Gradleのインストール**
2. **Gradleプロジェクトの初期化**
3. **Javalinの依存関係を追加**
4. **プロジェクト構造の作成**
5. **Javalinアプリケーションの実装**
6. **静的ファイルのホスト**

### 1. Gradleのインストール

まず、Gradleをインストールします。Gradleのインストール方法は公式サイトの[インストールガイド](https://gradle.org/install/)を参照してください。

### 2. Gradleプロジェクトの初期化

以下のコマンドを実行して、Gradleプロジェクトを初期化します。

```bash
gradle init --type java-application
```

これにより、基本的なプロジェクト構造が生成されます。

### 3. Javalinの依存関係を追加

`build.gradle` ファイルを開き、Javalinの依存関係を追加します。以下のように設定します。

```gradle
plugins {
    id 'application'
    id 'java'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'io.javalin:javalin:5.0.1' // 最新バージョンに合わせて変更
}

application {
    mainClassName = 'com.example.myapp.Main'
}
```




---

`Main.java` の階層を浅くするために、プロジェクトのディレクトリ構造をシンプルにし、`Main.java` をプロジェクトのルートに近い場所に配置します。以下に示すのは、`Main.java` を浅い階層に配置した構成です。

### プロジェクトのディレクトリ構造

```
myapp/
├── build.gradle
├── settings.gradle
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── Main.java
│   │   ├── resources/
│   │   │   └── public/
│   │   │       └── index.html
```

### 1. `build.gradle` ファイル

`build.gradle` ファイルは以下のように設定します。

```gradle
plugins {
    id 'application'
    id 'java'
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'io.javalin:javalin:5.0.1' // 最新バージョンに合わせて変更
}

application {
    mainClassName = 'Main'
}
```

### 2. `Main.java` ファイル

`src/main/java/Main.java` ファイルを作成し、次のように記述します。

```java
import io.javalin.Javalin;

public class Main {
    public static void main(String[] args) {
        Javalin app = Javalin.create(config -> {
            config.addStaticFiles("/public");
        }).start(7000);

        app.get("/", ctx -> ctx.redirect("/index.html"));
    }
}
```

### 3. `index.html` ファイル

`src/main/resources/public/index.html` ファイルを作成し、次のように記述します。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Welcome to Javalin</title>
</head>
<body>
    <h1>Hello, Javalin!</h1>
</body>
</html>
```

### プロジェクトのビルドと実行

次に、プロジェクトをビルドして実行します。

```bash
gradle build
gradle run
```

これにより、Javalinサーバーがポート7000で起動し、`index.html` がホストされます。ブラウザで `http://localhost:7000` にアクセスすると、`index.html` の内容が表示されます。

### まとめ

これで、プロジェクト構造を簡略化し、`Main.java` を浅い階層に配置した状態で、Gradleを使ってJavaプロジェクトにJavalinをインストールし、静的ファイル（`index.html`）をホストする方法が完了です。上述の手順に従うことで、簡単にJavalinを使用したWebアプリケーションを構築できます。

---
