---


---


---

Springフレームワークをインストールし、基本的なSpring Bootアプリケーションを作成する方法を説明します。Spring Bootは、Springアプリケーションを簡単に構築、設定、実行できるフレームワークです。

以下は、Gradleを使用してSpring Bootアプリケーションをセットアップする手順です。

### プロジェクトのディレクトリ構造

```
myapp/
├── build.gradle.kts
├── settings.gradle.kts
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── MainApplication.java
│   │   ├── resources/
│   │   │   └── templates/
│   │   │       └── index.html
```

### 1. Gradleプロジェクトの初期化

まず、プロジェクトディレクトリを作成し、Gradleプロジェクトを初期化します。

```bash
mkdir myapp
cd myapp
gradle init --type java-application
```

### 2. `build.gradle.kts` ファイルの編集

`build.gradle.kts` ファイルを以下のように編集します。

```kotlin
plugins {
    id("org.springframework.boot") version "3.0.0" // 最新バージョンに変更
    id("io.spring.dependency-management") version "1.0.11.RELEASE"
    application
    java
}

repositories {
    mavenCentral()
}

dependencies {
    implementation("org.springframework.boot:spring-boot-starter-web")
    testImplementation("org.springframework.boot:spring-boot-starter-test")
}

java {
    toolchain {
        languageVersion.set(JavaLanguageVersion.of(17))
    }
}

application {
    mainClass.set("MainApplication")
}

tasks.named<Test>("test") {
    useJUnitPlatform()
}
```

### 3. `settings.gradle.kts` ファイルの編集

`settings.gradle.kts` ファイルを以下のように編集します。

```kotlin
rootProject.name = "myapp"
```

### 4. `MainApplication.java` ファイルの作成

`src/main/java/MainApplication.java` ファイルを作成し、以下のコードを記述します。

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class, args);
    }

    @RestController
    public static class MyController {
        @GetMapping("/")
        public String index() {
            return "Hello, Spring Boot!";
        }
    }
}
```

### 5. `index.html` ファイルの作成

`src/main/resources/templates/index.html` ファイルを作成し、以下のように記述します。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Welcome to Spring Boot</title>
</head>
<body>
    <h1>Hello, Spring Boot!</h1>
</body>
</html>
```

### 6. プロジェクトのビルドと実行

プロジェクトのルートディレクトリに戻り、以下のコマンドを実行してプロジェクトをビルドおよび実行します。

```bash
./gradlew build
./gradlew bootRun
```

これにより、Spring Bootアプリケーションが起動します。ブラウザで `http://localhost:8080` にアクセスすると、`Hello, Spring Boot!` というメッセージが表示されます。

### まとめ

この手順に従って、Gradleを使用してSpring Bootアプリケーションをセットアップし、基本的なWebアプリケーションを構築することができます。Spring Bootを使用すると、Webアプリケーションの開発が非常にシンプルかつ迅速になります。

---
