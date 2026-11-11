## AniPixel Java

Dependency-free Java 21 server. Build with JDK 21:

    mkdir -p build/classes
    javac --release 21 --add-modules jdk.httpserver -encoding UTF-8 -d build/classes $(find src/main/java -name '*.java')
    cp -R src/main/resources/. build/classes/
    jar --create --file anipixel-java.jar --main-class com.kudopixel.anipixel.Main -C build/classes .

GitHub Actions builds the JAR on pushes to main. Download it from Actions > Build executable JAR > Artifacts.

Run on Linux:

    export HOST=127.0.0.1 PORT=8080
    export TELEGRAM_BOT_TOKEN='your-token'
    export TELEGRAM_WEBHOOK_SECRET='random-secret'
    java --add-modules jdk.httpserver -jar anipixel-java.jar

Put Nginx/Caddy in front for HTTPS and proxy to 127.0.0.1:8080. Configure Telegram setWebhook to https://your-domain/telegram/webhook with secret_token equal to TELEGRAM_WEBHOOK_SECRET.

Routes: GET /health, /api/home, /api/search?q=naruto, /api/media/ID; POST /telegram/webhook. Other GET paths serve static assets. Callback state is currently minimal and in-memory.