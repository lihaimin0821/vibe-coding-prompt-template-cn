# 测试策略

## Web 项目测试

### 测试工具

- **单元测试：** [Vitest / Jest]
- **E2E 测试：** [Playwright / Cypress]

### 测试要求

- 新函数必须有单元测试
- 核心功能需要集成测试
- 每个功能后运行测试

### Web 测试命令

```bash
# 运行所有测试
npm test

# 运行测试（监听模式）
npm run test:watch

# 运行覆盖率
npm run test:coverage

# E2E 测试
npm run test:e2e
```

### Web 手动检查清单

- [ ] 功能按预期工作
- [ ] UI 在桌面端正常
- [ ] UI 在移动端正常
- [ ] 无控制台错误

---

## Android 项目测试

### 测试工具

- **单元测试：** [JUnit 5 / Kotest]
- **Instrumented 测试：** [AndroidJUnitRunner / Espresso]
- **UI 测试：** [Compose UI Testing]
- **Mock：** [MockK / Mockito]

### 测试要求

- ViewModel 必须有单元测试
- Repository 必须有单元测试
- 关键 UI 组件需要有 Compose UI 测试
- 每个功能后运行测试

### Android 测试命令

```bash
# 运行单元测试
./gradlew test

# 运行 Debug APK 的单元测试
./gradlew testDebugUnitTest

# 运行 Release APK 的单元测试
./gradlew testReleaseUnitTest

# 运行 UI 测试（需要设备或模拟器）
./gradlew connectedAndroidTest

# 运行 Debug UI 测试
./gradlew connectedDebugAndroidTest

# 运行测试并生成覆盖率报告
./gradlew testDebugUnitTest createDebugCoverageReport

# 只运行特定测试类
./gradlew testDebugUnitTest --tests "com.example.app.UserViewModelTest"
```

### Android 测试结构

```
app/src/test/                    # 单元测试
├── java/com/example/
│   ├── data/
│   │   └── repository/
│   │       └── UserRepositoryTest.kt
│   └── domain/
│       └── usecase/
│           └── GetUserUseCaseTest.kt

app/src/androidTest/             # Instrumented 测试
├── java/com/example/
│   └── ui/
│       └── screens/
│           └── UserProfileScreenTest.kt
```

### Android 单元测试示例

```kotlin
// ViewModel 单元测试
@OptIn(ExperimentalCoroutinesApi::class)
class UserViewModelTest {

    @MockK
    private lateinit var repository: UserRepository

    private lateinit var viewModel: UserViewModel

    @Before
    fun setup() {
        MockKAnnotations.init(this)
        viewModel = UserViewModel(repository)
    }

    @Test
    fun `loadUser should update uiState with user on success`() = runTest {
        // Given
        val userId = "123"
        val user = User(id = userId, name = "Test", email = "test@test.com")
        coEvery { repository.getUser(userId) } returns user

        // When
        viewModel.loadUser(userId)

        // Then
        val state = viewModel.uiState.value
        assertTrue(state is UserUiState.Success)
        assertEquals(user, (state as UserUiState.Success).user)
    }

    @Test
    fun `loadUser should update uiState with error on failure`() = runTest {
        // Given
        val userId = "123"
        coEvery { repository.getUser(userId) } throws Exception("Network error")

        // When
        viewModel.loadUser(userId)

        // Then
        val state = viewModel.uiState.value
        assertTrue(state is UserUiState.Error)
    }
}
```

### Android UI 测试示例

```kotlin
// Compose UI 测试
@ComposeUiTest
@Composable
fun UserProfileScreenTest() {
    val testUser = User(id = "1", name = "Test User", email = "test@test.com")

    composeTestRule.setContent {
        UserProfileScreen(
            uiState = UserUiState.Success(testUser)
        )
    }

    // 验证 UI 元素
    composeTestRule.onNodeWithText("Test User").assertIsDisplayed()
    composeTestRule.onNodeWithText("test@test.com").assertIsDisplayed()
}
```

### Android 手动检查清单

- [ ] Debug APK 构建成功
- [ ] Release APK 构建成功（签名配置正确）
- [ ] App 在真机上正常启动
- [ ] 主要功能可正常使用
- [ ] 无崩溃或 ANR
- [ ] 内存使用正常
- [ ] 电池消耗正常

---

## 通用测试原则

1. **测试不是可选的** — 每个功能必须有测试覆盖
2. **测试隔离** — 单元测试不应依赖外部资源
3. **快速反馈** — 单元测试应在几秒内完成
4. **可重复** — 测试结果应始终一致

---

## 预提交钩子

### Web 项目
提交前必须通过：
1. `npm run lint`
2. `npm test`

### Android 项目
提交前必须通过：
1. `./gradlew lintDebug`（代码检查）
2. `./gradlew testDebugUnitTest`（单元测试）

---

*测试是质量保证的基础，不要跳过。*