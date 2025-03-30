### 关键组件

/dev/input/eventX

EventHub

InputReader

InputDispatcher

InputMonitor

InputManagerService

WindowManagerService

ViewRootImpl

### 事件的分类

- keyEvent
- TouchEvent
- MouseEvent
- TrackBallEvent 轨迹球，基本被淘汰

基础接口和基础事件

- onKeyDown()
- onkeyUp()
- onKeyLongPress()
- onKeyMultiple()



1. onTouchDown()
2. onTouchUp()
3. onTouchMove()
4. onTouchLongPress()
5. onTouchMultiple()  多点触控

#### 硬件源、输入源

SOURCE_KEYBOARD

SOURCE_MOUSE

SOURCE_TOUCHPAD



接口的3要素

View、KeyCode、KeyEvent：响应的视图、输入的按键、事件描述体



#### 输入事件处理流程

1. 采集，EventHub从/dev/input中采集输入事件
2. 前期处理，InputReader将原始事件转换成对应的按键/触摸等事件
3. WMS分配，InputDispatcher把事件交给当前聚焦的窗口。InputMonitor是InputDispatcher与WMS之间的中介，
   - InputDispatcher有InputChannel，WMS的addWindows() 会打开这个InputChannel
   - InputChannel的mFd就是socket编号，InputDispatcher与窗口是通过域通信交流
4. 应用程序处理，ViewRootImpl对事件进行派发



#### ViewRootImpl对事件的派发

