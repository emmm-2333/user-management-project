# 用户管理系统 - 项目结构说明

## 项目概述
这是一个前后分离的用户管理系统，基于 Spring Boot 3.3.4 和 Vue 3 构建。项目支持用户注册、登录、JWT认证和用户信息管理等功能。

---

## 项目文件夹结构

### 📁 backend/ - 后端服务
Java Spring Boot 后端应用，负责处理业务逻辑、数据持久化和API接口。

**主要技术栈：**
- Spring Boot 3.3.4
- MySQL 数据库
- MyBatis 框架
- JWT 认证
- Java 21

#### backend/ 子文件夹说明：

##### `src/main/java/com/example/aichat/` - 应用源代码
###### `config/` - 配置类
- `CorsConfig.java` - 跨域请求配置，允许前端跨域调用API
- `FilterConfig.java` - 过滤器配置，注册JWT认证过滤器

###### `controller/` - 控制层
- `AuthController.java` - 认证相关接口（登录、注册）
- `UserController.java` - 用户管理接口（CRUD操作）

###### `dto/` - 数据传输对象

- `ApiResponse.java` - 统一的API响应封装格式
- `AuthRequest.java` - 登录请求的数据模型
- `RegisterRequest.java` - 注册请求的数据模型
- `UserRequest.java` - 用户信息请求的数据模型

###### `entity/` - 数据实体

- `User.java` - 用户实体，对应数据库中的user表

###### `exception/` - 异常处理
- `ApiException.java` - 自定义业务异常类
- `GlobalExceptionHandler.java` - 全局异常处理器，统一处理应用中的异常

###### `filter/` - 过滤器
- `JwtAuthenticationFilter.java` - JWT令牌认证过滤器，验证请求的合法性

###### `mapper/` - 数据访问层
- `UserMapper.java` - 用户数据库操作接口（MyBatis Mapper）

###### `service/` - 业务逻辑层
- `UserService.java` - 用户业务逻辑接口
- `impl/UserServiceImpl.java` - 用户业务逻辑实现类

###### `util/` - 工具类
- `JwtUtil.java` - JWT令牌生成和验证工具类

##### `src/main/resources/` - 资源文件
- `application.yml` - Spring Boot 主配置文件
  - 数据库连接配置
  - 服务器端口配置（8080）
  - JWT密钥和过期时间配置
- `schema.sql` - 数据库初始化脚本，定义user表结构
- `mapper/` - MyBatis映射XML文件目录

##### `src/test/` - 单元测试
- `java/com/example/aichat/controller/UserControllerTest.java` - 用户控制器单元测试

##### `target/` - 编译输出目录（自动生成）
- `classes/` - 编译后的Java类文件和资源文件
- `generated-sources/` - 注解处理生成的源文件
- `test-classes/` - 编译后的测试类文件

##### `secrets/` - 敏感信息配置
- `deepseek/api-key` - API密钥文件（仅在本地开发使用）

##### `pom.xml` - Maven项目配置文件

定义项目依赖、版本、编译插件等配置

##### `backend.iml` - IntelliJ IDEA 项目配置文件

---

### 📁 frontend/ - 前端应用
Vue 3 单页应用，提供用户交互界面。

**主要技术栈：**
- Vue 3.4.21
- Vite 5.2.0（构建工具）
- Vue Router 4.3.0（路由管理）
- Pinia 2.1.7（状态管理）
- Axios 1.6.8（HTTP客户端）
- Element Plus 2.8.4（UI组件库）

#### frontend/ 子文件夹说明：

##### `src/` - 应用源代码

###### `views/` - 页面组件
- `Login.vue` - 登录页面
- `Register.vue` - 注册页面
- `UserManagement.vue` - 用户管理页面

###### `router/` - 路由配置
- `index.js` - 定义应用的路由规则和导航

###### `stores/` - 状态管理
- `user.js` - 用户状态存储（Pinia），管理用户信息和认证状态

###### `api/` - API接口调用
- `auth.js` - 认证相关接口调用（登录、注册）
- `user.js` - 用户相关接口调用（查询、更新等）

###### `utils/` - 工具函数
- `axios.js` - Axios HTTP客户端配置和拦截器

##### `App.vue` - 根组件
应用的主容器组件，包含导航和布局

##### `main.js` - 应用入口
初始化Vue应用、挂载路由和状态管理

##### `index.html` - HTML入口文件
定义应用的基础HTML结构

##### `package.json` - NPM项目配置
定义依赖包、构建脚本等

##### `vite.config.js` - Vite构建配置
定义开发服务器和构建输出选项

---

### 📁 docs/ - 项目文档
存放项目相关文档、说明和配置信息。

---

## 整体架构流程

```
用户浏览器
    ↓
frontend (Vue 3)
    ├─ 页面展示 (Login, Register, UserManagement)
    ├─ 路由管理 (Router)
    ├─ 状态管理 (Pinia)
    └─ API请求 (Axios)
    ↓
backend (Spring Boot)
    ├─ 接收HTTP请求 (Controller)
    ├─ 验证JWT令牌 (Filter)
    ├─ 业务处理 (Service)
    ├─ 数据访问 (Mapper)
    └─ 数据库操作 (MySQL)
    ↓
MySQL 数据库
    └─ 存储用户信息
```

---

## 开发流程

### 后端开发
1. **修改实体类** → `entity/User.java`
2. **编写业务逻辑** → `service/UserService.java` 和实现类
3. **创建或修改接口** → `controller/` 中的控制器
4. **更新数据库** → 修改 `schema.sql`
5. **编写测试** → `src/test/`

### 前端开发
1. **设计页面** → `src/views/` 创建Vue组件
2. **配置路由** → `src/router/index.js`
3. **编写API调用** → `src/api/` 中的接口函数
4. **管理状态** → `src/stores/` 中的Pinia store
5. **样式美化** → 使用Element Plus组件和CSS

---

## 部署注意事项

- **后端端口**：默认 8080
- **数据库**：MySQL 配置在 `application.yml`
- **JWT密钥**：需要修改为安全密钥，配置在 `application.yml`
- **前端构建**：运行 `npm run build` 生成dist目录
- **跨域配置**：已在 `CorsConfig.java` 中配置允许前端跨域请求
