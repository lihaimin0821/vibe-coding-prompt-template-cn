# 代码规范与模式

## TypeScript/JavaScript（Web）

### 命名约定

- **组件：** PascalCase（如 `UserProfile.tsx`）
- **函数：** camelCase（如 `getUserData`）
- **常量：** UPPER_SNAKE_CASE（如 `MAX_RETRIES`）
- **文件：** kebab-case（如 `my-component.ts`）

### TypeScript 规范

```typescript
// ✅ 好的做法
interface User {
  id: string;
  name: string;
  email: string;
}

function getUser(id: string): Promise<User> {
  return fetch(`/api/users/${id}`).then(res => res.json());
}

// ❌ 避免
function getUser(id: any): any {
  // ...
}
```

### 组件规范

```tsx
// 组件模板
interface Props {
  title: string;
  onClick?: () => void;
}

export function MyComponent({ title, onClick }: Props) {
  return (
    <button onClick={onClick}>
      {title}
    </button>
  );
}
```

## Kotlin（Android）

### 命名约定

- **类：** PascalCase（如 `UserProfileActivity`）
- **函数：** camelCase（如 `getUserData`）
- **常量：** UPPER_SNAKE_CASE（如 `MAX_RETRIES`）
- **文件：** PascalCase（如 `UserProfile.kt`）
- **包名：** 全小写（如 `com.example.app`）

### 数据类

```kotlin
// ✅ 好的做法
data class User(
    val id: String,
    val name: String,
    val email: String
)

// ❌ 避免使用 var
data class User(
    var id: String = "",  // 不要这样
    var name: String = ""
)
```

### ViewModel

```kotlin
// ✅ 好的做法 - 使用 Kotlin Coroutines
class UserViewModel(
    private val repository: UserRepository
) : ViewModel() {

    private val _uiState = MutableStateFlow<UserUiState>(UserUiState.Loading)
    val uiState: StateFlow<UserUiState> = _uiState.asStateFlow()

    fun loadUser(userId: String) {
        viewModelScope.launch {
            _uiState.value = UserUiState.Loading
            try {
                val user = repository.getUser(userId)
                _uiState.value = UserUiState.Success(user)
            } catch (e: Exception) {
                _uiState.value = UserUiState.Error(e.message ?: "Unknown error")
            }
        }
    }
}

// UI 状态
sealed class UserUiState {
    data object Loading : UserUiState()
    data class Success(val user: User) : UserUiState()
    data class Error(val message: String) : UserUiState()
}
```

### Repository

```kotlin
// ✅ 好的做法
interface UserRepository {
    suspend fun getUser(id: String): User
    suspend fun saveUser(user: User)
}

class UserRepositoryImpl(
    private val localDataSource: UserLocalDataSource,
    private val remoteDataSource: UserRemoteDataSource
) : UserRepository {

    override suspend fun getUser(id: String): User {
        return try {
            remoteDataSource.getUser(id)
        } catch (e: Exception) {
            localDataSource.getUser(id)
        }
    }
}
```

### Jetpack Compose

```kotlin
// ✅ 好的做法
@Composable
fun UserProfileScreen(
    viewModel: UserViewModel = hiltViewModel()
) {
    val uiState by viewModel.uiState.collectAsState()

    when (val state = uiState) {
        is UserUiState.Loading -> LoadingScreen()
        is UserUiState.Success -> UserProfileContent(user = state.user)
        is UserUiState.Error -> ErrorScreen(message = state.message)
    }
}
```

### 依赖注入（Hilt）

```kotlin
// ✅ 好的做法
@HiltViewModel
class UserViewModel @Inject constructor(
    private val repository: UserRepository,
    private val savedStateHandle: SavedStateHandle
) : ViewModel() {
    // ...
}

@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    @Singleton
    fun provideUserRepository(
        localDataSource: UserLocalDataSource,
        remoteDataSource: UserRemoteDataSource
    ): UserRepository {
        return UserRepositoryImpl(localDataSource, remoteDataSource)
    }
}
```

## 通用代码模式

### 错误处理

```typescript
// Web
async function fetchData() {
  try {
    const response = await fetch('/api/data');
    if (!response.ok) throw new Error('请求失败');
    return await response.json();
  } catch (error) {
    console.error('错误:', error);
    throw error;
  }
}
```

```kotlin
// Android
suspend fun fetchData(): Result<Data> {
    return try {
        val response = apiService.getData()
        Result.success(response)
    } catch (e: Exception) {
        Result.failure(e)
    }
}
```

## 项目文件结构

### Web 项目
```
src/
├── components/     # 可复用组件
├── pages/          # 页面组件
├── hooks/          # 自定义 Hooks
├── utils/          # 工具函数
├── types/          # 类型定义
└── styles/         # 样式文件
```

### Android 项目
```
app/src/main/java/com/example/
├── data/           # 数据层
│   ├── repository/
│   ├── local/
│   ├── remote/
│   └── model/
├── domain/          # 领域层
│   ├── model/
│   ├── repository/
│   └── usecase/
├── ui/              # UI 层
│   ├── screens/
│   ├── components/
│   ├── navigation/
│   └── theme/
└── di/              # 依赖注入
```