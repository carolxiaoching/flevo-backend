<p align="center">
  <img src="https://res.cloudinary.com/dtgnh1wcu/image/upload/logo_gusoue.svg" alt="logo" width="200">
</p>

<h1 align="center">燃味廚房</h1>

<p align="center">
  <strong>
  ⭐ 此為「燃味廚房」的後端專案 ⭐
  </strong>
</p>

<p align="center">
  <a href="https://flevo-backend.zeabur.app/api-doc/">
  👉 查看 API 文件
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Express-brightgreen?style=for-the-badge&logo=express&logoColor=white&color=000000">
  <img src="https://img.shields.io/badge/Node.js-brightgreen?style=for-the-badge&logo=nodedotjs&logoColor=white&color=5FA04E">
  <img src="https://img.shields.io/badge/firebase-brightgreen?style=for-the-badge&logo=firebase&logoColor=white&color=DD2C00">
  <img src="https://img.shields.io/badge/swagger-brightgreen?style=for-the-badge&logo=swagger&logoColor=white&color=85EA2D">
  <img src="https://img.shields.io/badge/mongodb-brightgreen?style=for-the-badge&logo=mongodb&logoColor=white&color=47A248">
  <img src="https://img.shields.io/badge/Nodemailer-brightgreen?style=for-the-badge&color=4B5563">  
</p>

## 📒 專案簡介

**「燃味廚房 | 後端」** 是支援 [「燃味廚房 | 前端」](https://github.com/carolxiaoching/flevo-frontend) 的後端服務，主要功能包括提供食譜、分類、標籤、會員資料的儲存 （使用 MongoDB）、、圖片儲存（上傳至 Firebase Storage，並將圖片資料儲存於 MongoDB）、電子郵件寄送（Nodemailer）等功能的 RESTful API

## ✨ 主要功能

- 🔐 管理員功能：管理會員、食譜、圖片、分類、標籤
- 📝 訪客與會員功能：瀏覽與操作會員、食譜、圖片、分類、標籤
- 🖼️ 圖片處理：支援 png、jpg、jpeg、webp 格式，使用 Multer 上傳、Tinify 壓縮後存入 Firebase Storage，並將圖片資料存入 MongoDB
- 📧 忘記密碼信件寄送（Nodemailer）
- 🧩 身份驗證（JWT）
- 📊 API 文件生成（Swagger）
- 🗃️ 資料儲存與驗證（MongoDB + Validator）

## 💡 使用技術

| 分類       | 技術                                                                                                                                     |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 後端框架   | [Express](https://expressjs.com/)、[Express-Generator](https://expressjs.com/en/starter/generator.html) (快速生成)                       |
| 資料庫     | [Mongoose](https://mongoosejs.com/)、[MongoDB](https://www.mongodb.com/)                                                                 |
| 認證與驗證 | [bcryptjs](https://www.npmjs.com/package/bcryptjs)、[jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)                           |
| 跨域處理   | [CORS](https://www.npmjs.com/package/cors)                                                                                               |
| 儲存服務   | [Firebase Admin SDK](https://firebase.google.com/docs/admin/setup) (Firebase Storage 圖片儲存)                                           |
| 圖片處理   | [Multer](https://www.npmjs.com/package/multer)、[Tinify](https://tinypng.com/developers)                                                 |
| 發送郵件   | [Nodemailer](https://nodemailer.com/)                                                                                                    |
| API 文檔   | [Swagger Autogen](https://www.npmjs.com/package/swagger-autogen)、[Swagger UI Express](https://www.npmjs.com/package/swagger-ui-express) |
| 驗證       | [Validator](https://www.npmjs.com/package/validator)                                                                                     |
| 開發工具   | [Nodemon](https://www.npmjs.com/package/nodemon)、[Cross-env](https://www.npmjs.com/package/cross-env)                                   |

🛠️ **安裝與執行**

```bash
# 1. 複製專案
git clone https://github.com/carolxiaoching/flevo-backend.git

# 2. 安裝依賴
cd flevo-backend
npm install

# 3. 設定環境變數
cp example.env config.env
# 根據實際環境編輯 config.env 內容

# 4. 啟動開發伺服器
npm run start:dev

# 5. 啟動正式環境伺服器
npm run start:prod

# 6. 產生 Swagger 文件：開發環境
npm run swagger:dev

# 7. 產生 Swagger 文件：正式環境
npm run swagger:prod
```

## 📁 專案結構

```plaintext
flevo-backend
│
├── connections/                  # 連接資料庫
│   └── firebase.js               # 連接 Firebase
│   └── index.js                  # 連接 MongoDB
│
├── controllers/                  # 控制器
│   └── admin/                    # 管理員控制器
│   │   └── memberManage.js       # 管理員會員 API 控制器
│   │   └── recipeManage.js       # 管理員食譜 API 控制器
│   │   └── imageManage.js        # 管理員圖片 API 控制器
│   │   └── categoryManage.js     # 管理員分類 API 控制器
│   │   └── tagManage.js          # 管理員標籤 API 控制器
│   │
│   └── member/                   # 一般用戶控制器
│       └── users.js              # 會員 API 控制器
│       └── recipes.js            # 食譜 API 控制器
│       └── images.js             # 圖片 API 控制器
│       └── categories.js         # 分類 API 控制器
│       └── tags.js               # 標籤 API 控制器
│
├── middleware/                   # 中介軟體
│   └── authMiddleware.js         # 驗證使用者身份的中介軟體（處理 JWT、設定及驗證會員身分與權限）
│   └── imageMiddleware.js        # 驗證圖片的中介軟體
│
├── models/                       # 資料庫模型
│   └── user.js                   # 使用者模型
│   └── recipe.js                 # 食譜模型
│   └── image.js                  # 圖片模型
│   └── category.js               # 分類模型
│   └── tag.js                    # 標籤模型
│
├── routes/                       # API 路由
│   └── admin/                    # 管理員路由
│   │   └── memberManage.js       # 管理員會員 API 路由
│   │   └── recipeManage.js       # 管理員食譜 API 路由
│   │   └── imageManage.js        # 管理員圖片 API 路由
│   │   └── categoryManage.js     # 管理員分類 API 路由
│   │   └── tagManage.js          # 管理員標籤 API 路由
│   │
│   └── member/                   # 一般用戶路由
│       └── users.js              # 會員 API 路由
│       └── recipes.js            # 食譜 API 路由
│       └── images.js             # 圖片 API 路由
│       └── categories.js         # 分類 API 路由
│       └── tags.js               # 標籤 API 路由
│       └── forget.js             # 忘記密碼 API 路由
│
├── services/                     # 服務層
│   └── appError.js               # 自定義錯誤格式
│   └── errorAsyncHandler.js      # 捕捉 async 函式錯誤的中介處理器
│   └── errorHandler.js           # 錯誤統一處理（dev / prod）
│   └── notFound.js               # 404 找不到資源處理
│   └── successHandler.js         # 統一成功回應格式
│
├── utils/                        # 通用工具
│   └── authUtils.js              # JWT 處理工具
│   └── imageUtils.js             # 圖片處理工具
│   └── paginationUtils.js        # 分頁處理工具
│   └── validationUtils.js        # 資料驗證工具
│
├── app.js                        # Express 應用主體
├── config.env                    # 環境變數檔
├── .gitignore                    # Git 忽略設定
├── config.js                     # 載入環境變數設定（已加入 .gitignore）
├── example.env                   # env 環境變數範例
├── README.md                     # 專案說明文件
├── package.json                  # 專案依賴與腳本設定
├── package-lock.json             # 套件鎖定檔
├── swagger-output.json           # Swagger 自動產出檔案
└── swagger.json                  # Swagger 設定檔

```

## 📁 專案結構說明

本專案以模組化方式拆分功能資料夾，讓程式碼結構更清晰易維護，說明如下：

- `connections/`：設定與 Firebase、MongoDB 的資料庫連線
- `controllers/`：負責處理使用者的請求，依身分與功能分類
- `middleware/`：中介軟體，用來處理像是 JWT 驗證、圖片檢查等功能
- `models/`：定義資料庫 Schema
- `routes/`：設定 API 路由，依身分與功能分類
- `services/`：統一處理錯誤回應、成功回應等通用邏輯
- `utils/`：通用的工具函式（例如圖片處理、JWT、分頁、驗證等功能）
- `swagger.json` / `swagger-output.json`：API 文件設定與自動產出檔案
- `app.js`：Express 應用程式主體
- `config.env` / `example.env`：環境變數與設定範例

## 💼 資料庫設計

![資料庫設計](https://imgur.com/FmOVmGz.png)

## 🚀 API 路由

### 管理員 API 路由

#### 管理員 - 會員 API 路由

| 方法     | 路徑                             | 描述               |
| -------- | -------------------------------- | ------------------ |
| `POST`   | `/admin/member/signIn`           | 管理員登入         |
| `GET`    | `/admin/member/checkLoginStatus` | 確認管理員登入狀態 |
| `GET`    | `/admin/members`                 | 取得所有會員       |
| `GET`    | `/admin/member/:memberId`        | 取得指定會員       |
| `PATCH`  | `/admin/member/:memberId`        | 更新指定會員       |
| `DELETE` | `/admin/member/:memberId`        | 刪除指定會員       |
| `DELETE` | `/admin/members`                 | 刪除全部會員       |

#### 管理員 - 食譜 API 路由

| 方法     | 路徑                              | 描述                 |
| -------- | --------------------------------- | -------------------- |
| `POST`   | `/admin/recipe`                   | 建立食譜             |
| `GET`    | `/admin/recipes`                  | 取得所有食譜         |
| `GET`    | `/admin/recipe/:recipeId`         | 取得指定食譜         |
| `PATCH`  | `/admin/recipe/:recipeId`         | 更新指定食譜         |
| `GET`    | `/admin/recipes/member/:memberId` | 取得指定會員所有食譜 |
| `DELETE` | `/admin/recipe/:recipeId`         | 刪除指定食譜         |
| `DELETE` | `/admin/recipes/member/:memberId` | 刪除指定會員所有食譜 |
| `DELETE` | `/admin/recipes`                  | 刪除所有食譜         |

#### 管理員 - 分類 API 路由

| 方法     | 路徑                          | 描述         |
| -------- | ----------------------------- | ------------ |
| `GET`    | `/admin/categories`           | 取得全部分類 |
| `GET`    | `/admin/category/:categoryId` | 取得指定分類 |
| `POST`   | `/admin/category`             | 新增分類     |
| `PATCH`  | `/admin/category/:categoryId` | 更新分類     |
| `DELETE` | `/admin/category/:categoryId` | 刪除指定分類 |
| `DELETE` | `/admin/categories`           | 刪除全部分類 |

#### 管理員 - 標籤 API 路由

| 方法     | 路徑                | 描述         |
| -------- | ------------------- | ------------ |
| `GET`    | `/admin/tags`       | 取得全部標籤 |
| `GET`    | `/admin/tag/:tagId` | 取得指定標籤 |
| `POST`   | `/admin/tag`        | 新增標籤     |
| `PATCH`  | `/admin/tag/:tagId` | 更新標籤     |
| `DELETE` | `/admin/tag/:tagId` | 刪除指定標籤 |
| `DELETE` | `/admin/tags`       | 刪除全部標籤 |

#### 管理員 - 圖片上傳 API 路由

| 方法     | 路徑                             | 描述                 |
| -------- | -------------------------------- | -------------------- |
| `GET`    | `/admin/images`                  | 取得所有圖片         |
| `GET`    | `/admin/image/:imageId`          | 取得指定圖片         |
| `DELETE` | `/admin/images/member/:memberId` | 刪除指定會員所有圖片 |
| `DELETE` | `/admin/images`                  | 刪除所有圖片         |
| `POST`   | `/admin/image`                   | 上傳圖片             |
| `DELETE` | `/admin/image/:imageId`          | 刪除指定圖片         |

### 一般使用者 (訪客或會員) API 路由

#### 一般使用者 - 會員 API 路由

| 方法    | 路徑                        | 描述                 |
| ------- | --------------------------- | -------------------- |
| `POST`  | `/api/user/signUp`          | 會員註冊             |
| `POST`  | `/api/user/signIn`          | 會員登入             |
| `GET`   | `/api/user/:userId/profile` | 取得指定會員公開資料 |
| `GET`   | `/api/user/profile`         | 取得我的資料         |
| `PATCH` | `/api/user/profile`         | 更新我的資料         |
| `POST`  | `/api/user/updatePassword`  | 重設密碼(已登入狀態) |
| `GET`   | `/api/user/getCollectList`  | 取得我的收藏列表     |

#### 一般使用者 - 忘記密碼相關 API 路由

| 方法   | 路徑                   | 描述                        |
| ------ | ---------------------- | --------------------------- |
| `POST` | `/api/forget-password` | 忘記密碼 - 寄送重設密碼信件 |
| `POST` | `/api/reset-password`  | 忘記密碼 - 重設密碼         |

#### 一般使用者 - 食譜 API 路由

| 方法     | 路徑                              | 描述                     |
| -------- | --------------------------------- | ------------------------ |
| `GET`    | `/api/publicRecipes`              | 取得所有公開食譜         |
| `GET`    | `/api/publicRecipes/user/:userId` | 取得指定會員所有公開食譜 |
| `GET`    | `/api/recipe/:recipeId`           | 取得指定食譜             |
| `GET`    | `/api/recipes`                    | 取得我的所有食譜         |
| `POST`   | `/api/recipe`                     | 建立食譜                 |
| `PATCH`  | `/api/recipe/:recipeId`           | 更新我的食譜             |
| `DELETE` | `/api/recipe/:recipeId`           | 刪除我的食譜             |
| `POST`   | `/api/recipe/:recipeId/collect`   | 收藏食譜                 |
| `DELETE` | `/api/recipe/:recipeId/collect`   | 取消收藏食譜             |

#### 一般使用者 - 分類 API 路由

| 方法  | 路徑                        | 描述         |
| ----- | --------------------------- | ------------ |
| `GET` | `/api/categories`           | 取得全部分類 |
| `GET` | `/api/category/:categoryId` | 取得指定分類 |

#### 一般使用者 - 標籤 API 路由

| 方法  | 路徑              | 描述         |
| ----- | ----------------- | ------------ |
| `GET` | `/api/tags`       | 取得全部標籤 |
| `GET` | `/api/tag/:tagId` | 取得指定標籤 |

#### 一般使用者 - 圖片上傳 API 路由

| 方法     | 路徑                  | 描述         |
| -------- | --------------------- | ------------ |
| `POST`   | `/api/image`          | 上傳圖片     |
| `DELETE` | `/api/image/:imageId` | 刪除指定圖片 |

> **注意：** 以上 API 路由可能會需要用戶驗證，請在請求中攜帶有效的 Bearer JWT token

## 📚 Swagger 文件

[Flevo API](https://flevo-backend.zeabur.app/api-doc/)

## 📁 專案結構

| 專案 | 連結                                                                                                                          |
| ---- | ----------------------------------------------------------------------------------------------------------------------------- |
| 前端 | [GitHub Repo](https://github.com/carolxiaoching/flevo-frontend) 🌞 [Demo](https://carolxiaoching.github.io/flevo-frontend/#/) |
| 後端 | [GitHub Repo](https://github.com/carolxiaoching/flevo-backend)                                                                |

## 📌 備註

本專案僅作為學習與展示用途，無任何商業營利行為
