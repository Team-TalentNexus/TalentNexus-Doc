# TalentNexus API文档

## 求职者

### 求职者登录接口

- **接口地址**: `/seeker/login`
- **请求方式**: `POST`
- **请求格式**: `application/json`

#### 请求参数

请求体 `JobSeekerLoginDto`

字段:

- `username` (string, 必填): 用户名
- `password` (string, 必填): 密码

#### 请求示例

```json
{
  "username": "exampleUser",
  "password": "examplePassword"
}
```

#### 响应

- **成功响应**:

  - **状态码**: `200 OK`

  - **响应体**: `ApiResponse<String>`

    字段:

    - `status` (integer): 状态码，`200` 表示成功
    - `message` (string): 响应消息
    - `data` (string): 登录成功后返回的 JWT

  - **响应示例**:

    ```json
    {
      "status": 200,
      "message": "Success",
      "data": "your-jwt-token"
    }
    ```

- **失败响应**:

  - **状态码**: `401 Unauthorized`

  - **响应体**: `ApiResponse<String>`

    字段:

    - `status` (integer): 状态码，`401` 表示认证失败
    - `message` (string): 错误消息

  - **响应示例**:

    ```Json
    {
      "status": 401, 
      "message": "Invalid credentials"
    }
    ```

#### 错误码说明

- `401 Unauthorized` - 用户名或密码错误

### 求职者注册接口

- **接口地址**: `/seeker/register`
- **请求方式**: `POST`
- **请求格式**: `application/json`

#### 请求参数

请求体 `JobSeeker`

字段:

- `username` (string, 必填): 用户名。唯一标识符，不能与其他用户重复。
- `password` (string, 必填): 密码的原始值(明文，加密存储由后端进行)。
- `email` (string, 必填): 用户的电子邮件地址。必须是一个有效的电子邮件地址格式。不能重复。
- `phone` (string, 选填): 用户的联系电话号码。
- `fullName` (string, 必填): 用户的全名。
- `gender` (string, 必填): 性别。可接受的值为 `"male"`、`"female"` 或 `"other"`。
- `birthDate` (string, 必填): 出生日期，格式为 YYYY-MM-DD。
- `address` (string, 选填): 用户的家庭住址。

#### 请求示例

```json
{
    "username": "voo",
    "password": "123",
    "email": "kkzeee@example.com2",
    "phone": "1234567890",
    "fullName": "John Doe",
    "gender": "male",
    "birthDate": "1990-01-01",
    "address": "123 Elm Street, Springfield"
}
```

#### 响应

- **成功响应**:

  - **状态码**: `200 OK`

  - **响应体**: `ApiResponse<String>`

    字段:

    - `status` (integer): 状态码，`200` 表示成功
    - `message` (string): 响应消息
    - `data` (string): 登录成功后返回的 JWT

  - **响应示例**:

    ```json
    {
        "code": 200,
        "message": "Success",
        "data": "Success"
    }
    ```

- **失败响应**:

  重复的用户名或邮箱

  - **状态码**: `409 Conflict`

  - **响应体**: `ApiResponse<String>`

    字段:

    - `status` (integer): 状态码，`409 Conflict` 
    - `message` (string): 错误消息

  - **响应示例**:

    ```Json
    {
        "code": 409,
        "message": "用户名或邮箱已存在",
        "data": null
    }
    ```

  参数不全
  
  - **状态码**: `400 Bad Request`
  
  - **响应体**: `ApiResponse<String>`
  
    字段:
  
    - `status` (integer): 状态码，`400 Bad Request` 
    - `message` (string): 错误消息
  
  - **响应示例**:
  
    ```json
    {
        "code": 400,
        "message": "username_empty",
        "data": null
    }
    ```
  
    

#### 错误码说明

- `409 Conflict` - 用户名或邮箱已存在
- `400 Bad Request` -参数缺失

### 求职者新建简历

