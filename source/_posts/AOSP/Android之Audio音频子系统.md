- 底层硬件抽象（TinyALSA、AudioHAL）
- 核心服务（AudioFlinger、AudioPolicyService）
- 上层应用接口（MediaPlayer、MediaRecorder）



---

音频系统架构()

应用层：AudioTrack（播放）、AudioRecorder（录音）

框架层：AudioFlinger和AudioPolicyService

HAL层：

内核层：ALSA

---

音频的工作流程（播放）

- AudioTrack创建音频流，设置音频属性(采样率、音道数)
- AudioTrack将音频数据传递给AudioFlinger
- AudioFlinger会访问AudioPolicyService获取音频策略，将音频路由到合适的输出设备
- AudioFlinger通过HAL层发送数据到硬件

---

音频的核心

AudioFlinger、AudioPolicyService、AudioTrack和AudioRecorder。

AudioFlinger、AudioPolicyService是SystemService，在mediaserver进程中

------

### 如何去学习一个模块

- 以**库**为线索，AudioPolicyService和AudioFlinger都封装在libaudioflinger库中，AudioTrack和AudioRecorder等在media库中。
- 以**进程**为线索，AudioPolicyService和AudioFlinger都驻留在mediaserver的系统进程中，AudioTrack和AudioRecorder等只是应用进程的一部分。

**HAL**

硬抽象层主要2个核心，即AudioFlinger，AudioPolicyService。AudioPolicy并不是一个真实设备，而是采用虚拟设备方便厂商定制自己的音频策略