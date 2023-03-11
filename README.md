# Actix的基本组件

- 设备浏览器通过互联网 到达Actix HTTP Server（包含Actix APP） 访问 Actix Route 找到 Actix Handler
- Actix Handler 返回资源到设备浏览器


## Actix 的并发
- 异步I/O：给定的OS原生线程在等待I/O时执行其他任务；例如侦听网络连接
- 多线程并行：默认情况下启动OS原声线程的数量与系统逻辑CPU数量相同


# 构建的内容

POST A Course <---> Handler 1

GET A Course <---> Handler 2

GET all course for teacher <---> Handler 3

## 具体
- POST: /courses
- GET: /courses/teacher_id
- GET: /courses/teacher_id/course_id

## Test

```shell
curl -x POST localhost:3000/courses/ -H "Content-Ty
pe: application/json" -d '{"teacher_id":1, "name":"First course"}'
```

# 连接数据库

- sqlx
- PostgreSQL

# 错误处理

- 数据库错误
- seder错误（串行化）
- I/O错误
- Actix错误
- 用户非法输入错误

- 上述错误通过自定义错误类型，转为 HTTP Response 错误

## 错误处理方式
- 异常
- 返回值（rust 使用这种）

## Actix-Web把错误转化为 HTTP Response

- actix_web::error::Error
  - 实现了std::error::Error这个trait
  - 这个trait，实现了常见错误内置
    - rust 标准 i/o错误
    - serde错误
    - web错误
    - 其他错误类型

- 任何实现了标准库Error trait的类型，都可以通过?运算符，转化为 Actix的 Error类型

- Actix的Error类型会自动的转化为 HTTP Response 返回给客户

## 创建自定义错误处理器
1. 创建一个自定义错误类型
2. 实现From trait，用于把其他错误类型转化为该类型
3. 为自定义错误类型实现ResponseError trait
4. 在handler里返回自定义错误类型
5. Actix会把错误转化为HTTP响应
