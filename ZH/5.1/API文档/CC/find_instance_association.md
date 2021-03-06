### 请求地址

/api/c/compapi/v2/cc/find_instance_association/

### 请求方法

POST

### 功能描述

查询模型的实例关联关系。

### 请求参数

#### 通用参数

| 字段 | 类型 | 必选 | 描述 |
|-----------|------------|--------|------------|
| bk_app_code | string | 是 | 应用  ID |
| bk_app_secret| string | 是 | 安全密钥(应用 TOKEN)，可以通过 蓝鲸智云开发者中心 -&gt; 点击应用 ID -&gt; 基本信息 获取 |
| bk_token | string | 否 | 当前用户登录态，bk_token 与 bk_username 必须一个有效，bk_token 可以通过 Cookie 获取 |
| bk_username | string | 否 | 当前用户用户名，应用免登录态验证白名单中的应用，用此字段指定当前用户 |

#### 接口参数

| 字段 | 类型 | 是否必填	 | 描述 |
|----------------------|------------|--------|-----------------------------|
| metadata | object | Yes | meta data |
| condition | string map | Yes | 查询条件 |

##### metadata params

| 字段 | 类型 | 是否必填	 | 描述 |
|---------------------|------------|--------|-----------------------------|
| label | string map | Yes | 标签信息 |

##### label params

| 字段 | 类型 | 是否必填	 | 描述 |
|---------------------|------------|--------|-----------------------------|
| bk_biz_id | string | Yes | 业务 ID |

##### condition params

| 字段 | 类型 | 是否必填	 | 描述 |
|---------------------|------------|--------|-----------------------------|
| bk_obj_asst_id | string | Yes | 模型关联关系的唯一 id|
| bk_asst_id | string | NO | 关联类型的唯一 id|
| bk_obj_id | string | NO | 源模型 id|
| bk_asst_id | string | NO | 目标模型 id|

### 请求参数示例

```json
{
    "condition": {
        "bk_obj_asst_id": "bk_switch_belong_bk_host",
        "bk_asst_id": "",
        "bk_object_id": "",
        "bk_asst_obj_id": ""
    },
    "metadata":{
        "label":{
            "bk_biz_id":"3"
        }
    }
}
```

### 返回结果示例

```json
{
    "result": true,
    "code": 0,
    "message": "",
    "data": [{
        "bk_obj_asst_id": "bk_switch_belong_bk_host",
        "bk_obj_id":"switch",
        "bk_asst_obj_id":"host",
        "bk_inst_id":12,
        "bk_asst_inst_id":13
    }]
}

```

### 返回结果参数说明

| 字段 | 类型 | 描述 |
|-----------|-----------|-----------|
| result | bool | 请求成功与否，true:请求成功，false:请求失败 |
| code | string | 组件返回错误编码，0 表示 success，>0 表示失败错误 |
| message | string | 请求失败返回的错误消息 |
| data | object | 请求返回的数据 |

#### data

| 字段 | 类型 | 描述 |
|------------|----------|--------------|
| id|int64|the association's unique id|
| bk_obj_asst_id| string| 自动生成的模型关联关系 id.|
| bk_obj_id| string| 关联关系源模型 id |
| bk_asst_obj_id| string| 关联关系目标模型 id|
| bk_inst_id| int64| 源模型实例 id|
| bk_asst_inst_id| int64| 目标模型实例 id|
