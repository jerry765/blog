---
title: websocket 在 vue 中的使用
tags:
  - vue
  - websocket
  - frontend
categories: project
date: 2023-08-22 11:13:38
---


### 依赖

socket.io-client

``` bash
pnpm i socket.io-client
```

<!-- more -->

### 使用

1. 规范 socket api

``` ts
// socket.ts

import { reactive } from "vue"
import { io, Socket } from "socket.io-client"

class SocketService {
  socket: Socket
  state: any

  constructor() {
    this.state = reactive({
      id: "",
      room: "",
      sio: null,
      flag: 60,
      sid: "",
      heartbeatTimer: null
    })

    this.socket = io("/websocket", {
      autoConnect: false, // 禁止自动连接
      extraHeaders: {
        "Access-Control-Allow-Origin": "*" // 设置跨域请求头
      }
    })

    // connect, get_sid 只执行一次，采用 once
    this.socket.once("connect", () => {
      this.handleConnect()
    })

    this.socket.once("get_sid", (data) => {
      this.handleGetSid(data)
    })

    this.socket.on("join_room_result", (res) => {
      this.handleJoinRoomResult(res)
    })

    this.socket.on("test", (data) => {
      this.handleTest(data)
    })

    this.socket.on("leave", (room) => {
      this.handleLeave(room)
    })

    this.socket.on("leave_all", () => {
      this.handleLeaveAll()
    })

    this.socket.on("connect_error", (err) => {
      this.handleConnectError(err)
    })
  }

  connect() {
    this.socket.connect()
    console.log("socket connect")
  }

  disconnect() {
    this.handleLeaveAll()
    this.stopHeartbeat()
    this.socket.disconnect()
    console.log("socket disconnect")
  }

  joinRoom(room: string) {
    this.socket.emit("join", { rooms: [room] })
  }

  leaveRoom(room: string) {
    this.handleLeave(room)
  }

  leaveAll() {
    this.handleLeaveAll()
  }

  private handleConnect() {
    this.socket.emit("get_sid", {})
  }

  private handleGetSid(data: any) {
    this.state.sid = data.sid
    console.log("get_sid:", this.state.sid)
  }

  private handleJoinRoomResult(res: any) {
    console.log(res)
  }

  private handleTest(data: any) {
    console.log("test data:" + data)
  }

  // 离开指定房间
  private handleLeave(room: string) {
    this.socket.emit("leave", { rooms: [room] })
    console.log("leave room " + room)
  }

  // 离开所有房间
  private handleLeaveAll() {
    this.socket.emit("leave_all")
    console.log("leave all room")
  }

  // 处理连接错误
  private handleConnectError(err: any) {
    this.stopHeartbeat() // 停止心跳，避免不必要的心跳消息
    console.log(err)
  }
  
  // 启动心跳计时器
  private startHeartbeat() => {
    if(this.heartbeatTimer === null) {
        this.heartbeatTimer = setInterval(() => {
            this.sendHeartbeat()
        }, 15000) // 15秒发送一次心跳，可以根据需求调整
    }
  }

  // 停止心跳计时器
  private stopHeartbeat() => {
    if(this.heartbeatTimer !== null) {
        clearInterval(this.heartbeatTimer)
        this.heartbeatTimer = null
    }
  }

  // 发送心跳数据
  private sendHeartbeat() {
    this.socket.emit("heartbeat", { /* 心跳数据 */ })
  }
}

export const socketService = new SocketService()
export const socket = socketService.socket
export const state = socketService.state
```

2. 设置 url

``` ts
// vite.config.ts

proxy: {
    "/socket.io": {
        target: "http://example.com" // 代理目标（后端 socket URL ）
        ws: true, // 设置代理 WebSocket 连接
        changeOrigin: true, // 允许跨域
    }
}
```

3. 建立 socket 连接

websocket 连接应在打开页面时建立，关闭页面时销毁，所以应选择在入口文件建立。

``` ts
// App.vue

import { socketService } from "@/api/socket"
import { onBeforeUnmount } from "vue"

socketService.connect()

onBeforeMount(() => {
    socketService.disconnect()
})
```

4. 进入 socket 房间

为保证浏览器性能，房间应该在进入特定路由时建立，离开特定路由时退出，所以选择在路由守卫文件编写相关逻辑。

``` ts
// permission.ts

import router from "@/router"
import { socketService } from "@/api/socket"

router.afterEach((to, from) => {
    // 离开特定路由时离开对应房间
    if( from.name === "room-name" ) {
        socketService.leaveRoom("room-name")
    }

    // 进入特定路由时进入特定房间
    if( to.name !== "room-name" ) {
        socketService.joinRoom("room-name")
    }
})
```

5. 监听数据

后端通过 WebSocket 发送的数据在前端页面渲染的部分，应在前端对应页面监听。

``` ts
// index.vue

import { socket } from "@/api/socket"

const subscribeChannel = (channel: string) => {
    unsubscribeChannel(channel) // 避免重复订阅

    socket.on(channel, (data) => {
        // 处理数据...
    })
}

const unsubscribeChannel = (channel: string) => {
    socket.off(channel)
}
```

## 参考

[WebSocket - Web Api 接口参考|MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/WebSocket)
[Socket.io](https://socket.io/zh-CN/)