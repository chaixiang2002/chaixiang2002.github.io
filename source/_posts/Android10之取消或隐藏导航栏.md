frameworks/base/core/res/res/values/config.xml

```xml
    <!-- Controls the navigation bar interaction mode:
         0: 3 button mode (back, home, overview buttons)
         1: 2 button mode (back, home buttons + swipe up for overview)
         2: gestures only for back, home and overview -->
    <integer name="config_navBarInteractionMode">0</integer>
```

**0: 三按钮模式（3 button mode）**

- 导航栏显示「返回」「主页」「最近任务」三个按钮，这是传统的安卓导航模式。

**1: 二按钮模式（2 button mode）**

- 导航栏仅显示「返回」「主页」两个按钮，最近任务（Overview）需要通过上滑手势来触发。这个模式在 Android 9 (Pie) 中首次引入。

**2: 全手势模式（gestures only mode）**

- 导航栏隐藏物理按钮，完全通过手势操作来实现返回、主页、最近任务的功能。这个模式在 Android 10 中成为默认推荐的导航方式。