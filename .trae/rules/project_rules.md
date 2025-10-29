# Memory Bank

你熟悉 uni-app x框架，擅长编写跨平台且高性能的代码。
uni-app x项目使用UTS语言编写script。 UTS是一种跨平台的强类型语言， 类似TS语言但类型要求更加严格。

## Code Style and Structure
    - 简洁易懂，复杂的代码配上中文注释。
    - 严格类型匹配，不使用隐式转换。
    - 不使用变量和函数的声明提升，严格的在清晰的范围内使用变量和函数。
    - 当生成某个平台专用代码时，应使用条件编译进行平台约束，避免干扰其他平台。

## project
    - 遵循uni-app x的项目结构，在正确的目录中放置生成的文件。
    
## page
    - 使用uvue作为页面后缀名，uvue与vue基本类似，但有少量细节差异。
    - 生成的uvue页面放置在项目的pages目录下，生成的页面需要在pages.json中注册。
    - 可滚动内容必须在scroll-view、list-view、waterflow等滚动容器中。 如果页面需要滚动，则在页面template的一级子节点放置滚动容器，例如` <scroll-view style="flex:1">`。此时应在 App 上使用条件编译，例如：`<!-- #ifdef APP --><scroll-view class="container"><!-- #endif -->`。
    - 生成uvue页面时，页面内容需符合uts.mdc、uvue.mdc、ucss.mdc、api.mdc约定的规范。

# API
    - 可以使用uts的api，但注意版本和平台的兼容性。
    - 可以使用uni-app x的api，但注意版本和平台的兼容性。
    - 可以使用vue3的api，但注意版本和平台的兼容性。
    - 可以使用操作系统的api，但注意版本和平台的兼容性。尽量在uts插件中调用系统原生API，而不是在uvue页面中直接调用系统原生API。
    - 特定平台或特定版本以上才能使用的代码，需使用条件编译包围这些代码，或者放置在平台专用的目录文件中。
    - 通过mcp工具查询项目下可用的插件。
    - 跨页面通信优先使用eventbus。


# uvue rules

## vue support
    - 仅使用vue3语法，避免使用vue2。
    - 新页面尽量使用组合式API。
    - 组件尽量使用easycom规范。
    - 非easycom的自定义vue组件，调用组件方法时需使用组件实例的`$callMethod`方式调用。
    - 不使用 pinia、vuex、i18n 等uni-app x不支持的vue插件。
    - 使用vue语法时需注意uni-app x官网的平台和版本兼容性，平台特殊代码需包裹在条件编译中。

    ## component
    - 组件可使用uni-app x内置组件，以及项目下的自定义组件。通过mcp工具查询项目下可用的easycom插件。
    - 项目可使用vuejs组件规范，对应的文件扩展名为uvue。
    - 符合easycom规范的组件无需import和注册，可直接在template中使用。
    - 使用内置组件时需注意uni-app x官网的平台和版本兼容性，平台特殊代码需包裹在条件编译中。

# conditional compilation

## core syntax
    ```
    // Platform basic judgment
    #ifdef APP || MP
    //Mini programs/APP common code
    #ifdef APP-ANDROID
        // Android-specific logic
    #endif
    #ifdef APP-IOS
        // IOS-specific logic
    #endif
    #endif
    ```

## Core Platform Identifier
    uniVersion is used to distinguish the version of the compiler Details HBuilderX 3.9.0 
    APP App
    APP-ANDROID App Android Platform Details
    APP-IOS App iOS Platform Details
    APP-HARMONY App HarmonyOS Next platform
    WEB web (same as H5) HBuilderX 3.6.3 
    MP-WEIXIN WeChat Mini Program
    MP-ALIPAY APPLET
    MP-BAIDU BAIDU MINI PROGRAM
    MP-TUTIAO TIKTOK MINI PROGRAM
    MP-KUAISHOU Kuaishou Mini Program
    MP-JD JD Mini Program
    MP-HARMONY Harmony Atom Service HBuilderX 4.34 
    MP-XHS Xiaohongshu Mini Program
    MP WeChat Mini Program/Alipay Mini Program/Baidu Mini Program/Douyin Mini Program/Feishu Mini Program/QQ Mini Program/360 Mini Program/Hongmeng atom Service

# UTS Rules
    - 生成的脚本代码使用跨平台的UTS语言。
    - UTS语言类似ts，但为了跨平台编译为kotlin、swift等强类型语言，进行了约束。
    - UTS是强类型语言，类型要求严格，不能动态转换类型。 与kotlin等强类型语言一样。
    - 不能使用类型隐式转换。 尤其是条件语句(if、while、do-while、三元运算符、for 循环的条件部分)必须使用布尔类型作为条件。 当判断变量a是否为空时，不能写成 `if (a)`，或`if (!a)` 要写成 `if (a!=null)`。
    - 可为null和不可为null的类型需要严格区分，使用 `|null` 或 `?` 来定义可为空。
    - 可为null的数据类型在使用其属性或方法时，需要判断不为null，或者使用`?.`安全调用。 谨慎使用 `!.` 断言。
    - any类型的变量在使用其属性或方法时，需要as为正确的相容类型。
    - 不支持object类型，使用UTSJSONObject类型替代。
    - 不支持undefined，变量使用前必须赋值。
    - 对象类型定义使用type而不是interface。interface是接口，不用于对象类型定义。
    - 变量和常量定义使用let和const，不使用var。
    - 不使用 JSX 表达式。
    - 不使用 with 语句。
    - 不使用ts的结构化类型系统。 使用名义类型系统， 强调类型名称和继承关系以确保类型安全。
    - 不使用 is 运算符。 使用 instanceof 和 as 进行类型保护。
    - 尽量不使用any。
    - 尽量不使用 === 和!==， 使用 == 和!= 替代。
    - 不使用js的原型链特性。
    - 严格遵守“先定义后使用”的规则。使用代码在定义代码之前。
    - 更多参考：[uts与ts的差异](https://doc.dcloud.net.cn/uni-app-x/uts/uts_diff_ts.html)
    
# css rules
    ucss是css的子集，但可以跨平台使用。除了浏览器之外，还支持App原生平台。

    ## 布局规范
    - 禁用浮动、网格等布局，仅使用flex布局或绝对定位。
    - flex布局默认方向为垂直(通过 flex-direction:column 实现)。

    ## 选择器规则
    - 仅支持基本的类选择器 (.class)，禁止使用其他选择器。
    - 类名必须符合 [A-Za-z0-9_-]+ 规范，禁止使用特殊字符(例如 @class)。

    ## 文字样式规则
    - 文字内容需放置在组件 <text> 或 <button> 中。 文字类样式(color、font-size)只能设置在 <text> 或 <button> 组件上。 其他组件（如<view>）禁止设置文本相关样式。
    - 文字样式不继承。
    - 禁用继承相关关键字，例如 inherit 和 unset。

    ## 层级控制
    - z-index 仅对同级兄弟节点生效。
    - absolute 固定位与文档流分离，不支持分层覆盖。

    ## 长度单位
    - 仅支持px、rpx、百分比。 字体的line-height支持em。 不能使用其他单位，如vh。
    - 除非width需要根据屏幕宽度而变化才使用rpx单位。 其他场景不使用rpx单位。
    - 除非长度单位需要根据父容器大小而变化才使用百分比单位。 其他场景不使用rpx单位。

    ## at-rules
    - 仅支持`@font-face`、`@import`，不使用其他at-rules。
    - 如需使用`@media` 适配不同屏幕，改用 uts 代码实现，先通过API `uni.getWindowInfo`获取屏幕宽度，再通过代码进行适配。
    - 如需使用`@media` 适配暗黑模式，改用 uts 代码 和 css变量 实现。
    - 如需使用`@keyframes`，改为通过UniElement对象的animate方法实现相同逻辑。

    ## css function
    - 仅支持 url()、rgb()、rgba()、var()、env()，不使用其他css方法。

    ## 样式作用范围规则
    - 不使用css scoped。

