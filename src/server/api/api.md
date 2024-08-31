# TalentNexus API文档

## 求职者

### 求职者登录接口

- **接口地址**: `/seeke/login`
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

