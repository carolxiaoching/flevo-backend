<p align="center">
  <img src="https://res.cloudinary.com/dtgnh1wcu/image/upload/logo_gusoue.svg" alt="logo" width="200">
</p>

<h1 align="center">燃味廚房 | 後端</h1>

<p align="center">
  <strong>
  ⭐ 此為「燃味廚房」的後端專案 ⭐
  </strong>
</p>

<p align="center">
  <a href="https://flevo-backend.zeabur.app/api-doc/">API 文件</a>
  ·
  <a href="https://github.com/carolxiaoching/flevo">前端 Repo</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-5FA04E?style=for-the-badge&logo=nodedotjs&logoColor=white">
  <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white">
  <img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white">
  <img src="https://img.shields.io/badge/Firebase-DD2C00?style=for-the-badge&logo=firebase&logoColor=white">
  <img src="https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=black">
</p>

<p align="center">
  支援「燃味廚房」前端的 RESTful API 服務，提供食譜、會員、分類、標籤與圖片管理功能。
</p>

<br>

## 功能總覽

- 食譜、會員、分類、標籤、圖片的 CRUD API
- 圖片上傳：Multer 接收、Tinify 壓縮後存入 Firebase Storage
- 忘記密碼 Email 寄送（Nodemailer）
- JWT 身份驗證
- Swagger API 文件自動生成

## 技術棧

| 分類     | 技術                                                                                                                                     |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| 後端框架 | [Express](https://expressjs.com/)                                                                                                        |
| 資料庫   | [MongoDB](https://www.mongodb.com/)、[Mongoose](https://mongoosejs.com/)                                                                 |
| 認證     | [jsonwebtoken](https://www.npmjs.com/package/jsonwebtoken)、[bcryptjs](https://www.npmjs.com/package/bcryptjs)                           |
| 圖片處理 | [Multer](https://www.npmjs.com/package/multer)、[Tinify](https://tinypng.com/developers)                                                 |
| 儲存服務 | [Firebase Admin SDK](https://firebase.google.com/docs/admin/setup)                                                                       |
| 發送郵件 | [Nodemailer](https://nodemailer.com/)                                                                                                    |
| API 文件 | [Swagger Autogen](https://www.npmjs.com/package/swagger-autogen)、[Swagger UI Express](https://www.npmjs.com/package/swagger-ui-express) |
| 驗證     | [Validator](https://www.npmjs.com/package/validator)                                                                                     |
| 跨域處理 | [CORS](https://www.npmjs.com/package/cors)                                                                                               |
| 開發工具 | [Nodemon](https://www.npmjs.com/package/nodemon)、[Cross-env](https://www.npmjs.com/package/cross-env)                                   |

## 快速開始

```bash
git clone https://github.com/carolxiaoching/flevo-backend.git
cd flevo-backend
npm install

# 設定環境變數
cp example.env config.env
# 根據實際環境編輯 config.env

# 啟動開發伺服器
npm run start:dev

# 啟動正式環境
npm run start:prod

# 產生 Swagger 文件（開發）
npm run swagger:dev

# 產生 Swagger 文件（正式）
npm run swagger:prod
```

## 專案結構

```plaintext
flevo-backend
│
├── connections/                  # 資料庫連線
│   ├── firebase.js               # Firebase 連線
│   └── index.js                  # MongoDB 連線
│
├── controllers/                  # 控制器
│   ├── admin/                    # 管理員
│   │   ├── memberManage.js
│   │   ├── recipeManage.js
│   │   ├── imageManage.js
│   │   ├── categoryManage.js
│   │   └── tagManage.js
│   └── member/                   # 一般使用者
│       ├── users.js
│       ├── recipes.js
│       ├── images.js
│       ├── categories.js
│       └── tags.js
│
├── middleware/                   # 中介軟體
│   ├── authMiddleware.js         # JWT 驗證、權限控制
│   └── imageMiddleware.js        # 圖片驗證
│
├── models/                       # 資料庫 Schema
│   ├── user.js
│   ├── recipe.js
│   ├── image.js
│   ├── category.js
│   └── tag.js
│
├── routes/                       # API 路由
│   ├── admin/                    # 管理員路由
│   └── member/                   # 一般使用者路由
│
├── services/                     # 通用服務
│   ├── appError.js               # 自定義錯誤格式
│   ├── errorAsyncHandler.js      # async 錯誤捕捉
│   ├── errorHandler.js           # 錯誤統一處理
│   ├── notFound.js               # 404 處理
│   └── successHandler.js         # 成功回應格式
│
├── utils/                        # 工具函式
│   ├── authUtils.js              # JWT 處理
│   ├── imageUtils.js             # 圖片處理
│   ├── paginationUtils.js        # 分頁處理
│   └── validationUtils.js        # 資料驗證
│
├── app.js                        # Express 應用主體
├── example.env                   # 環境變數範例
└── swagger.json                  # Swagger 設定檔
```

## 資料庫設計

![資料庫設計](https://imgur.com/FmOVmGz.png)

## API 路由

### 管理員

#### 會員

| 方法     | 路徑                             | 描述         |
| -------- | -------------------------------- | ------------ |
| `POST`   | `/admin/member/signIn`           | 管理員登入   |
| `GET`    | `/admin/member/checkLoginStatus` | 確認登入狀態 |
| `GET`    | `/admin/members`                 | 取得所有會員 |
| `GET`    | `/admin/member/:memberId`        | 取得指定會員 |
| `PATCH`  | `/admin/member/:memberId`        | 更新指定會員 |
| `DELETE` | `/admin/member/:memberId`        | 刪除指定會員 |
| `DELETE` | `/admin/members`                 | 刪除全部會員 |

#### 食譜

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

#### 分類

| 方法     | 路徑                          | 描述         |
| -------- | ----------------------------- | ------------ |
| `GET`    | `/admin/categories`           | 取得全部分類 |
| `GET`    | `/admin/category/:categoryId` | 取得指定分類 |
| `POST`   | `/admin/category`             | 新增分類     |
| `PATCH`  | `/admin/category/:categoryId` | 更新分類     |
| `DELETE` | `/admin/category/:categoryId` | 刪除指定分類 |
| `DELETE` | `/admin/categories`           | 刪除全部分類 |

#### 標籤

| 方法     | 路徑                | 描述         |
| -------- | ------------------- | ------------ |
| `GET`    | `/admin/tags`       | 取得全部標籤 |
| `GET`    | `/admin/tag/:tagId` | 取得指定標籤 |
| `POST`   | `/admin/tag`        | 新增標籤     |
| `PATCH`  | `/admin/tag/:tagId` | 更新標籤     |
| `DELETE` | `/admin/tag/:tagId` | 刪除指定標籤 |
| `DELETE` | `/admin/tags`       | 刪除全部標籤 |

#### 圖片

| 方法     | 路徑                             | 描述                 |
| -------- | -------------------------------- | -------------------- |
| `GET`    | `/admin/images`                  | 取得所有圖片         |
| `GET`    | `/admin/image/:imageId`          | 取得指定圖片         |
| `POST`   | `/admin/image`                   | 上傳圖片             |
| `DELETE` | `/admin/image/:imageId`          | 刪除指定圖片         |
| `DELETE` | `/admin/images/member/:memberId` | 刪除指定會員所有圖片 |
| `DELETE` | `/admin/images`                  | 刪除所有圖片         |

---

### 一般使用者

#### 會員

| 方法    | 路徑                        | 描述                 |
| ------- | --------------------------- | -------------------- |
| `POST`  | `/api/user/signUp`          | 會員註冊             |
| `POST`  | `/api/user/signIn`          | 會員登入             |
| `GET`   | `/api/user/:userId/profile` | 取得指定會員公開資料 |
| `GET`   | `/api/user/profile`         | 取得我的資料         |
| `PATCH` | `/api/user/profile`         | 更新我的資料         |
| `POST`  | `/api/user/updatePassword`  | 重設密碼（已登入）   |
| `GET`   | `/api/user/getCollectList`  | 取得我的收藏列表     |

#### 忘記密碼

| 方法   | 路徑                   | 描述             |
| ------ | ---------------------- | ---------------- |
| `POST` | `/api/forget-password` | 寄送重設密碼信件 |
| `POST` | `/api/reset-password`  | 重設密碼         |

#### 食譜

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

#### 分類

| 方法  | 路徑                        | 描述         |
| ----- | --------------------------- | ------------ |
| `GET` | `/api/categories`           | 取得全部分類 |
| `GET` | `/api/category/:categoryId` | 取得指定分類 |

#### 標籤

| 方法  | 路徑              | 描述         |
| ----- | ----------------- | ------------ |
| `GET` | `/api/tags`       | 取得全部標籤 |
| `GET` | `/api/tag/:tagId` | 取得指定標籤 |

#### 圖片

| 方法     | 路徑                  | 描述         |
| -------- | --------------------- | ------------ |
| `POST`   | `/api/image`          | 上傳圖片     |
| `DELETE` | `/api/image/:imageId` | 刪除指定圖片 |

> 部分 API 需在 request header 攜帶有效的 Bearer JWT token

## Swagger 文件

[https://flevo-backend.zeabur.app/api-doc/](https://flevo-backend.zeabur.app/api-doc/)
