### CDN
- CDN称为内容分发系统，即通过最靠近用户的服务器实现更快、更可靠的内容传输
- CDN 常用来托管静态资源（如js、css、html、图片等）；也可用于流媒体场景，例如直播，对流媒体数据进行缓存

### 懒加载
- 概念：懒加载也叫延迟加载、按需加载，即将部分模块、资源进行延迟加载，以达到提升页面性能的目的，譬如长列表场景、首屏等
- 作用
    - 减少非必须的资源提前加载
    - 提升用户体验
    - 避免资源扎堆加载，导致部分资源加载滞后，从而影响页面性能
- 实现原理
    - 通过监听模块进入屏幕可视区域的距离，控制模块的加载时机

### 预加载
- 概念：预加载也叫前置加载，即提升对模块、资源进行加载，以达到提升页面性能的目的，譬如在当前页面进程空闲时提前加载下一个页面的部分资源

### 懒加载、预加载的区别
- 懒加载、预加载都是提升页面性能的手段
- 懒加载会减缓服务端的请求压力
- 预加载会增加服务端的请求压力

### 重绘、回流
- 回流：当页面内元素的几何属性（大小、位置、形状等）发生变化时，导致页面整体或区域进行重新布局则称为页面回流
    - 产生回流的场景 
        - 元素内容变化
        - 字体大小
        - 位置
        - 查询元素
        - 操作DOM
        - 浏览器窗口变化
        - 首次渲染
        - 其他
- 重绘：当页面的样式属性发生变化时，且不影响其他元素的位置发生变化，则称为重绘
- 重绘与回流的关系：
    - 重绘不一定产生回流
    - 回流一定产生重绘
        - 重绘导致回流的属性
            - color、background
            - shadow
            - outline
            - border
- 如何避免重绘、回流
    - 避免频繁操作元素样式，可通过更换样式类名方式实现
    - 对元素操作时对可能产生回流动作的元素进行脱离文档流操作，以尽量减少回流产生的影响
    - 尽量避免大范围的DOM操作

