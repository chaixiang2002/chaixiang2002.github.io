[日志文件高亮显示器 - Visual Studio Marketplace --- Log File Highlighter - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=emilast.LogFileHighlighter)

Log File Highlighter 日志文件荧光笔插件

C:\Users\Administrator\AppData\Roaming\Code\User\settings.json

```json
"cmake.pinnedCommands": [
"workbench.action.tasks.configureTaskRunner",
"workbench.action.tasks.runTask"
],
 "logFileHighlighter.enableProgressIndicator": true,
    "logFileHighlighter.progressIndicatorUnderlineColor": "#ffee00",
    "logFileHighlighter.customPatterns": [
        // {
        //     "pattern": "I/", // Info 日志
        //     "background": "#008f58", // 绿色背景
        //     "textDecoration": "underline", // 下划线
        //     "foreground": "#ffffff" // 白色文字
        // },
        {
            "pattern": "fail", // Debug 日志
            "background": "#007acc", // 蓝色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": "Fail", // Debug 日志
            "background": "#007acc", // 蓝色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },





        {
            "pattern": "warn", // Warning 日志
            "background": "#ffcc00", // 黄色背景
            "textDecoration": "underline",
            "foreground": "#000000" // 黑色文字
        },
        {
            "pattern": " W ", // Warning 日志
            "background": "#ffcc00", // 黄色背景
            "textDecoration": "underline",
            "foreground": "#000000" // 黑色文字
        },
        {
            "pattern": " E ", // Error 日志
            "background": "#cc0000", // 红色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": "Error", // Error 日志
            "background": "#cc0000", // 红色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": " F ", // Fatal 日志
            "background": "#9900cc", // 紫色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": "FATAL", // Fatal 日志
            "background": "#9900cc", // 紫色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": "Exception", // 异常信息
            "background": "#ff4500", // 橙红色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": "FileNotFoundException", // 找不到文件异常
            "background": "#ff6347", // 番茄红色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        },
        {
            "pattern": "RuntimeException", // 运行时异常
            "background": "#8b0000", // 深红色背景
            "textDecoration": "underline",
            "foreground": "#ffffff" // 白色文字
        }
    ]
```

