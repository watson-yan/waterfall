# waterfall-瀑布流组件

> 基于Vue.js的瀑布流组件

### Demo地址: [https://huayan.site/waterfall](https://huayan.site/waterfall)

## 瀑布流布局的优点
瀑布流对于图片的展现，是高效而具有吸引力的，用户一眼扫过的快速阅读模式可以在短时间内获得更多的信息量,而瀑布流里懒加载模式又避免了用户鼠标点击的翻页操作，瀑布流的主要特性便是错落有致，定宽而不定高的设计让页面区别于传统的矩阵式图片布局模式，巧妙的利用视觉层级，视线的任意流动又缓解了视觉疲劳，同时给人以不拘一格的感觉，切中年轻一族的个性化心理。国内类Pinterest网站也如雨后春笋般出现，已知网站超40家，类Pinterest网站有四种，一是电商导购，如想去网、蘑菇街和美丽说、好享说、依托于淘宝平台;二是兴趣图谱分享，如知美、花瓣等;三是在细分垂直领域，如针对吃货的零食控、针对家居行业的他部落等。四是服装款式设计资讯平台如看潮网等等。

## 瀑布流的分类：*竖向瀑布流* 和 *横向瀑布流*
* ### 竖向瀑布流
图片列表分为固定列，每个图片或者容器的宽度相同，高度与宽度等比缩放(所以不同的比例图片高度不一样)，如下图所示：

<img src="http://upload-images.jianshu.io/upload_images/3778813-bf24085a98babefc.png"/>

* ### 横向瀑布流：
图片或者容器保持高度相同，每一行的显示的图片宽度之和等于页面的宽度，高度与宽度等比缩放(所以不同的比例图片宽度不一样)，但由于宽度不一定能满足刚好占满一行，所以采取了切割图片的做法， 如下图所示：

<img src="http://upload-images.jianshu.io/upload_images/3778813-a817aefc27d38959.png"/>

## How to use
作为瀑布流的一个尝试，并没有打包发布，组件的源码在 *./src/components/Waterfall.vue*中, 该例子只是作为一个demo，具体可以根据使用场景在此基础上做修改。

## 说明
此示例中需要后端传回的数据包含图片的尺寸数据，如果完全靠前端来计算图片的宽和高，对网络和性能开销比较大，我们项目的实际也是采用了后端传回图片的宽高来计算出在瀑布流中显示的比例，保持图片不变形。

## Props
prop|type|description
---|---|---
list|Array|图片列表
row|Boolean|是否横向排列
column|Number|如果不是横向排列,column代表分为几列（默认4列）
height|Number|如果是横向排列, height为没行应该占得高度（默认225px）


## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
