---
title: RabbitMQ学习
comments: true
date: 2023-07-29 21:46:53
layout:
updated:
categories:
- 技术
tags:
- Rabbit
- 微服务
- SpringCloud
lang:
---
### 资源

[百度网盘 (baidu.com)](https://pan.baidu.com/disk/main?from=homeSave&_at_=1690637029498#/index?category=all&path=%2F%E7%A7%8B%E6%8B%9B%E5%89%8D%2FspringCloud)

1. 同步和异步
2. 什么是事件驱动？![img](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=OTBhZDViYmU3NTc1OTdiZmM0NDJjYjgzYTdiZDMzNWNfdGk1Z3k5anlPSlhrYnZPVFZZSzBkUDB1b2RmdVF0emhfVG9rZW46RmdGSmIwajVrb1RkRGd4YUx5ZGNROEZUbkFjXzE2OTA2MzkyODk6MTY5MDY0Mjg4OV9WNA)

   ![img](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=ODczYzk3OTFiODIyNDkwNTlmYTdkMmM3YWNkYTZkNWZfOERGUjZFSUw1dXhqNDRWTzdqd2l1ck9sWk95NldaVnpfVG9rZW46RGFIU2JwTHNOb3dKcXV4a1FIdmNXV3RUbmRnXzE2OTA2MzkzOTg6MTY5MDY0Mjk5OF9WNA)
3. MQ是一个事件驱动的broker，消息队列

![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=NjdlM2U1NzgxODAyM2U2MWViYjc2YmE0ZjNlNzlhMTJfRzhEUmU5TzVTMzRTaFhHMUhXWHE1UFVhbHBEMTRVNHdfVG9rZW46V0YxUGJHam1ZbzJHcHB4SzVJUmMwZWo2bkJjXzE2OTA2Mzk3OTQ6MTY5MDY0MzM5NF9WNA)

![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=MWJmZTkyOGQ3Mjc1ODA4NWExZjRiMWUwZWJmMmE0MzFfdjVOTDJGYm1ER3NoOUMwSVI2blVsNjVGMlpnd2RkZzNfVG9rZW46V2lETGJ3UHNOb0Z5VUt4MmMwaGNHb2ZhbldjXzE2OTA2NDA3NzQ6MTY5MDY0NDM3NF9WNA)

![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjhhYWIxNTY0YmIyZDc2YjkwOWE4OGYwYmY1MDIyY2FfUlM0ck1PV01zVVRFSmVXZU5GNTljQXpsM3R4dEJwWkZfVG9rZW46VDJWSWI0dWxpb2gyOVJ4ekVNc2NiNG1IbkwzXzE2OTA2NDA4NTA6MTY5MDY0NDQ1MF9WNA)

和安卓的异步机制好像

![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=Yzc1NTFiMWFlYzQwMWZmNjg3YWRhZDIyZWQwZjAxYThfcVhpVldYRWhIYmo0SlN5NkN1NmtDZFRqb3dXUFNENWdfVG9rZW46S0VPSmJ0RXBhb1U1eTB4bGFpQWNUUmxzbk1kXzE2OTA2NDE1Mjg6MTY5MDY0NTEyOF9WNA)

SpringAMQP

4. 工作队列，预取机制，保证信息不堆积 pretch
5. ![img](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=MjE1MGM3MTk4ZTgwYjQ4M2E2Y2NlMTBlOTNlY2I0ZThfREJRQUE3TmpyWXcwZ3dsanloYzJHRWJ1MnNJNVBYbklfVG9rZW46TTBmR2JSQ3l1bzlrYU94RzJmeGNqQUNpbnVjXzE2OTA3MDkwMDE6MTY5MDcxMjYwMV9WNA)

![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=ODNmMzQ3OWQ5MGFhMzgyYjIzYmZkNjk1ZjQ0OGI4ZWVfZ2RJeXVRQlVqck11ZkpraU1vOE1DMkpoUk5rbmg1RHVfVG9rZW46RllYamJFOVFib3ZKbFB4QUs1VWM5bVdlbmdkXzE2OTA2NDE2NDM6MTY5MDY0NTI0M19WNA)![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=YmJiYTdmNGI2OWE2NzZlYjM4MGU3ZjQ2NzZlYTM0NzJfY01ER3Fod0tMSHM5MlRNSjlNMWhqVm52MjZ5cjhiUlBfVG9rZW46QnV3a2I3QWVjbzJpYzl4VG5nUWM3MWNabnllXzE2OTA3MjQyNDk6MTY5MDcyNzg0OV9WNA)

3种类型的交换机

![img](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=MDIxNWRiNzY5OGNiM2Y3MWEwYmVlNjgyZDVkYTIxMTZfSnptbjBNRlN6NURhSlZYRzA5bDRtY3E5dzQ2cEFzdzZfVG9rZW46TVdjOGJ3Y3Rmb1hUVld4UlVJeGNBM1JBbjFDXzE2OTA3MjU2NzY6MTY5MDcyOTI3Nl9WNA)


序列化工具

![](https://regws02vdj.feishu.cn/space/api/box/stream/download/asynccode/?code=MmQ4OGQyMDVkYmZhOTQ1ZDhlMDYzYzA0MjYyNjE2YmNfYXlZSG1XVzl6MFVDTWpsa2ZYT1o3VHUyb2ZLM3REcUNfVG9rZW46WTA1NWJzdER1b3A5a0F4WWNiSmNNMXc0bjJkXzE2OTA3MjcyMzE6MTY5MDczMDgzMV9WNA)





a
