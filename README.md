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
