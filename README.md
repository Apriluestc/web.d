# WebServer

[![](https://img.shields.io/badge/build-pass-brightgreen)](https://github.com/Apriluestc/web.d/edit/master/README.md)

**测试页：**[Apriluestc's.pub](http://39.107.70.253:20000/)

## 项目介绍

本项目为 C++ 11 编写的高性能 Web 服务器，解析了 GET、POST 请求，可静态处理资源，支持 HTTP 长连接、支持
管线化请求，并实现了异步日志，实时记录服务器运行状态

## 技术特点

- 程序使用 Epoll 边沿触发、非阻塞 IO、Reactor 模式
- 使用多线程技术充分发挥多核 CPU 性能，并使用线程池规避线程频繁创建销毁的开销
- 使用基于时间轮的定时器关闭超时请求和剔除不活跃连接
- 主线程负责 accept 请求，并轮询分发 fd 给其他 IO 线程，这样一来锁竞争只会出现在主线程和某一特定线程
- 使用 eventfd 跨线程异步唤醒
- 使用 TCP 环形缓冲区，减少 read、write 等系统调用的次数，进而减少系统开销
- 使用智能指针、RAII 机制规避程序中出现内存泄漏的可能
- 实现异步日志实时记录服务器运行状态(便于 Debug)
- webd 服务以 dameon 进程运行

## 项目来源

- [陈硕](https://github.com/chenshuo/muduo/tree/master/muduo/net)
- 林亚
- 陈帅豪
