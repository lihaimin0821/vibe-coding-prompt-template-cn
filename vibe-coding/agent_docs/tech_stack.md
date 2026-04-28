# 技术栈与工具

## 前端 Web

- **框架：** [React / Vue / Next.js / Nuxt]
- **语言：** [TypeScript / JavaScript]
- **样式：** [Tailwind CSS / CSS Modules / Styled Components]
- **状态管理：** [Zustand / Redux / Context API]

## Android 移动端

- **语言：** [Kotlin / Java]
- **UI 框架：** [Jetpack Compose / XML 布局]
- **架构：** [MVVM / MVI / Clean Architecture]
- **依赖注入：** [Hilt / Koin / Dagger]
- **网络：** [Retrofit / OkHttp / Ktor]
- **本地数据库：** [Room / SQLite / DataStore]
- **异步：** [Kotlin Coroutines / Flow]
- **导航：** [Jetpack Navigation]
- **构建：** Gradle (Kotlin DSL)

### Android 项目结构

```
app/
├── src/main/
│   ├── java/com/example/
│   │   ├── data/           # 数据层
│   │   │   ├── repository/
│   │   │   ├── local/
│   │   │   └── remote/
│   │   ├── domain/          # 领域层
│   │   │   ├── model/
│   │   │   └── usecase/
│   │   ├── ui/              # UI 层
│   │   │   ├── screens/
│   │   │   ├── components/
│   │   │   └── viewmodel/
│   │   └── di/              # 依赖注入
│   ├── res/
│   │   ├── layout/
│   │   ├── values/
│   │   └── drawable/
│   └── AndroidManifest.xml
├── build.gradle.kts
└── proguard-rules.pro
```

### Android 开发命令

```bash
# 构建 Debug APK
./gradlew assembleDebug

# 构建 Release APK
./gradlew assembleRelease

# 运行单元测试
./gradlew test

# 运行 UI 测试
./gradlew connectedAndroidTest

# 清理并重新构建
./gradlew clean assembleDebug

# 分析依赖
./gradlew dependencies
```

## 后端（如有）

- **框架：** [Node.js + Express / FastAPI / Spring Boot]
- **语言：** [TypeScript / Python / Java / Kotlin]
- **数据库：** [PostgreSQL / MongoDB / MySQL / SQLite]

## 部署

- **Web 前端：** [Vercel / Netlify / Cloudflare Pages]
- **Android APK：** [Firebase App Distribution / 蒲公英 / fir.im / 自建服务器]
- **后端服务：** [Railway / Vercel / AWS / 阿里云]

## 开发命令

### Web 项目
```bash
npm install
npm run dev
npm test
npm run build
```

### Android 项目
```bash
# 使用 Gradle
./gradlew assembleDebug
./gradlew test
./gradlew connectedAndroidTest

# 或使用 Make
make install    # 安装到设备
make test       # 运行测试
make build      # 构建 APK
```

## 项目结构

### Web 项目
```
src/
├── components/     # UI 组件
├── pages/          # 页面
├── hooks/          # 自定义 Hooks
├── utils/          # 工具函数
└── types/          # 类型定义
```

### Android 项目
```
app/
├── src/main/java/  # Kotlin/Java 源码
├── src/main/res/   # 资源文件
├── src/test/       # 单元测试
└── src/androidTest/ # UI 测试
```