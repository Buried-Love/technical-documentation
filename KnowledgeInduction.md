# 基础知识总结归纳

<hr/>

# HTML

### 根据条件选DOM元素

```js
    var lodingImg = document.querySelector("img[class='loding-svg']");
    console.log(lodingImg);
```



<hr/>

# CSS 

### 解决margin的嵌套崩塌问题

> 1.给父盒子添加border（添加border之后，父子元素就不是真正意义上的贴合）
> 2.给父盒子设置padding-top
> 3.给父盒子添加overflow:hidden
> 4.父盒子：position:fixed;
> 5.父盒子：display:table;


### 英文字母或数字超出盒子

```css
    white-space: pre-wrap; /* CSS3 */
    white-space: -moz-pre-wrap; /* Firefox */
    white-space: -pre-wrap; /* Opera <7 */
    white-space: -o-pre-wrap; /* Opera 7 */
    word-wrap: break-word; /* IE */
```

### 多行文字超出变...

```css
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2; // 行数
    -webkit-box-orient: vertical;
```

### 元素穿透各种JS事件不遮挡

>   pointer-events: none;

### 文字两端对齐

###### PC端

```css
  text-align: justify;
  text-align-last: justify;
```

###### 移动端
>  移动端 直接设置并不生效 需要让文字超出两行 这里选择使用伪元素

```css
.text {
text-align: justify;
text-align-last: justify;
&:after {
     display: inline-block;
     width: 70px;
     height: 20px;
     text-align: justify;
     overflow: hidden;
     content: "";
  }
}

```
<hr/>

# NPM

### 淘宝镜像

> npm install cnpm -g --registry=https://registry.npm.taobao.org

<hr/>

# JS

###   打印插件

> print.js (这款插件只是在原生的基础上做了优化)


### 检测浏览器内核版本

>  我只需要webkit内核 所以下面是以这个为基准

```JS
 (function (w) {
            "use strict";
            var n = w.navigator,
                d = w.document;
            var r = [];
            r.isIE = ("number" == typeof d.documentMode) ? d.documentMode :
                false; //Trident    
            r.isWebkit = ("undefined" != typeof n.productSub && "20030107" == n.productSub);
            r.isChrome = ("object" == typeof w.chrome || (r.isWebkit && "string" == typeof n.vendor && /Google/
                .test(n.vendor)));
            r.isBlink = (r.isChrome || r.isOpera) && !!w.CSS;
            w.browsecore = r;
            document.writeln(r.isWebkit)
        })("undefined" != typeof window ? window : this);
```

### 检测浏览器名称 (只定义主流需要可以再加判断)

```JS

var webkit = document.getElementById("webkit");
var ifBrowser = document.getElementById("if-browser")
function getBrowserInfo() {
    var ua = navigator.userAgent.toLocaleLowerCase();
    var browserType = null;
    if (ua.match(/msie/) != null || ua.match(/trident/) != null) {
        webkit.style.display = "block"
        browserType = "IE";
        browserVersion = ua.match(/msie ([\d.]+)/) != null ? ua.match(/msie ([\d.]+)/)[1] : ua.match(/rv:([\d.]+)/)[1];
    } else if (ua.match(/firefox/) != null) {
        webkit.style.display = "block"
        browserType = "火狐";
    } else if (ua.match(/ubrowser/) != null) {
        webkit.style.display = "block"
        browserType = "UC";
    } else if (ua.match(/opera/) != null) {
        webkit.style.display = "block"
        browserType = "欧朋";
    } else if (ua.match(/bidubrowser/) != null) {
        webkit.style.display = "block"
        browserType = "百度";
    } else if (ua.match(/metasr/) != null) {
        webkit.style.display = "block"
        browserType = "搜狗";
    } else if (ua.match(/tencenttraveler/) != null || ua.match(/qqbrowse/) != null) {
        if (ua.match(/qbcore/) !== null) {
            browserType = "微信";
        } else {
            browserType = "QQ";
        }
        webkit.style.display = "block"
    } else if (ua.match(/maxthon/) != null) {
        webkit.style.display = "block"
        browserType = "遨游";
    } else if (ua.match(/lbbrowser/) !== null) {
        browserType = '猎豹';
        webkit.style.display = "block"
    } else if (ua.match(/chrome/) != null) {
        var true360 = 360;
        var mimeTypes = navigator.mimeTypes;
        if (mimeTypes.length > 20) {
            true360 = 360;
        } else {
            if (ua.match(/edg/) != null) {
                true360 = 1;
            } else {
                true360 = 2;
            }
        }
        if (true360 == 360) {
            browserType = '360';
            webkit.style.display = "block"
        } else if (true360 == 2) {
            browserType = '谷歌';
        } else {
            browserType = 'Edge';
            webkit.style.display = "block"
        }
    } else if (ua.match(/safari/) != null) {
        browserType = "Safari";
        webkit.style.display = "block"
    }
    ifBrowser.innerHTML = "";
    ifBrowser.innerHTML += browserType + "浏览器，";
}

getBrowserInfo()

```

### 检测浏览器是否加载flash

```JS
//  检测 浏览器是否加载flash
function hasUsableFlash() {
  var flashObj;
  if (typeof window.ActiveXObject != "undefined") {
    flashObj = new ActiveXObject("ShockwaveFlash.ShockwaveFlash");
  } else {
    flashObj = navigator.plugins['Shockwave Flash'];
  }
  return flashObj ? true : false;
}
```

### 定义浏览器从兼容模式到极速模式

``` HTML
 <meta name="renderer" content="webkit" />
    <meta name="force-rendering" content="webkit" />
    <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1" />
```


### 取URL

```JS
import Qs from 'qs' const query = Qs.parse(location.hash.substring(3));

let channel = query.channel let user = query.user

```


### 获取声音分贝

```JS 
        // 再谷歌上需要 用户执行 才可以获取
        function decibel() {
            if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
                let AudioContext = window.AudioContext || window.webkitAudioContext;
                var audioContext = new AudioContext();
                // 获取用户的 media 信息
                navigator.mediaDevices.getUserMedia({
                    audio: true
                }).then((stream) => {
                    // 将麦克风的声音输入这个对象 
                    mediaStreamSource = audioContext.createMediaStreamSource(stream);
                    // 创建一个音频分析对象，采样的缓冲区大小为4096，输入和输出都是单声道
                    var scriptProcessor = audioContext.createScriptProcessor(4096, 1, 1);
                    // 将该分析对象与麦克风音频进行连接
                    mediaStreamSource.connect(scriptProcessor);
                    // 此举无甚效果，仅仅是因为解决 Chrome 自身的 bug
                    scriptProcessor.connect(audioContext.destination);
                    // 开始处理音频
                    scriptProcessor.onaudioprocess = function (e) {
                        // 获得缓冲区的输入音频，转换为包含了PCM通道数据的32位浮点数组
                        let buffer = e.inputBuffer.getChannelData(0);
                        // 获取缓冲区中最大的音量值
                        let maxVal = Math.max.apply(Math, buffer);
                        // 显示音量值
                        box.style.height = Math.round(maxVal * 1000) * 4 + "px";
                    };
                }).catch((error) => {
                    console.log('获取音频时好像出了点问题' + error)
                });
            } else {
                alert('不支持获取媒体接口');
            }
        }
```

### 获取当前时间到X天之前的时间 (这里是近30天)

```JS
function getRaday() {
     var date = new Date();
    var year = date.getFullYear();
    var month = date.getMonth() + 1;
    var day = date.getDate();
    if (month < 10) {
        month = "0" + month;
    }
    if (day < 10) {
        day = "0" + day;
    }
    var nowData = year + "-" + month + "-" + day;
    var Date2 = new Date();
    Date2.setDate(Date2.getDate() - 29);
    var weekYear = Date2.getFullYear();
    var weekMonth = Date2.getMonth() + 1 > 10 ? Date2.getMonth() + 1 : '0' + (Date2.getMonth() + 1);
    var weekDate = Date2.getDate() > 10 ? Date2.getDate() : '0' + Date2.getDate();
    if (weekDate.length >= 3) {
        weekDate = Date2.getDate() > 10 ? Date2.getDate() : Date2.getDate();
    } else {
        weekDate = Date2.getDate() > 10 ? Date2.getDate() : '0' + Date2.getDate();
    }
    var oldData = weekYear + "-" + weekMonth + "-" + weekDate;
    return {
        startTime: nowData,
        endTime: oldData
    }

}

```
### 两个时间相减 返回值是结果

> 注意: ios上 不能使用 -  只能使用 / 所以用正则判断了一下

```JS
//  获取使用时间
function timesFun(startDate, endDate) {
    if (endDate == null) {
        endDate = "1988-01-01";
    };
    var startDateRep = startDate.replace(/\-/g, '/');
    var endDateRep = endDate.replace(/\-/g, '/');
    var date1 = startDateRep; //开始时间;;
    var date2 = endDateRep; //结束时间
    var date3 = new Date(date2).getTime() - new Date(date1).getTime(); //时间差的毫秒数    
    //计算出相差天数
    var days = Math.floor(date3 / (24 * 3600 * 1000))
    //计算出小时数
    var leave1 = date3 % (24 * 3600 * 1000) //计算天数后剩余的毫秒数
    var hours = Math.floor(leave1 / (3600 * 1000))
    //计算相差分钟数
    var leave2 = leave1 % (3600 * 1000) //计算小时数后剩余的毫秒数
    // console.log(leave2 / (60 * 1000)) round
    var minutes = Math.ceil(leave2 / (60 * 1000));
    var timesString = '';
    var timesStringCard = '';
    // 判断卡片时间
    if (days >= 1) {
        var daysNum = (days * 24 + hours) / 24;
        timesStringCard = daysNum.toFixed(1) + "天";
        timesString = days + "天 " + hours + "小时";
    } else if (hours == 0) {
        timesStringCard = minutes + "分钟";
        timesString = minutes + "分钟";
    } else {
        var hoursNum = (hours * 60 + minutes) / 60;
        timesStringCard = hoursNum.toFixed(1) + "小时";
        timesString = hours + "小时" + minutes + "分钟";
    }
    if (timesString.slice(0, 1) == "-") {
        timesString = "--"
    }
    return {
        timesStringCard: timesStringCard,
        timesString: timesString
    }
}
```

### 去除IOS 300ms 延迟 

```JS
$(function () {
    FastClick.attach(document.body);
});
```

<hr/>


# VUE 

###  VUE 页面离开时 函数钩子

```JS
 destroyed: function() {
  },
```


### VUE 动态更改title

###### 1、在项目目录下安装vue-wechat-title
   
 ```js
 cnpm i vue-wechat-title --save
 ```

###### 2、在main.js中使用vue-wechat-title

```js
    import VueWechatTitle from 'vue-wechat-title'  //引入

    Vue.use(VueWechatTitle)    //注册组件
```
###### 3、在router.js的配置中设置
```js
meta:{
       title:'登录',
       requireAuth:true
      }
```
###### 4、在每个vue页面中加入
```html
  <div v-wechat-title='$route.meta.title'></div>
```

> 如果不是 vue 使用 document.title = '标题'; (原生属性)


### 上级页面缓存
> 主要用于 我浏览页面到底部 我查看商品详情 再返回列表的时候 重新进入页面导致刷新 用户体验不好
> 列表页 ====>点击跳转到列表详情页面 ======> 返回列表页(希望页面不重新加载 且保留原来浏览的位置)

###### 两个用于区分 缓存与不缓存
```js
  <transition :name="transitionName" mode="out-in">
      <keep-alive>
        <router-view v-if="$route.meta.keepAlive" />
      </keep-alive>
    </transition>
    <transition :name="transitionName" mode="out-in">
      <router-view v-if="!$route.meta.keepAlive" />
    </transition>
```
###### router.js 内更改状态

>  $\color{#FF0000}{注意: 配置路由一定要使用 懒加载 ; component}$ 

```JS
  {
    path: "/home",
    name: "home",
    component: () => import("../views/home/index.vue"),  
    meta: {
      requireAuth: true,
      adminShow: false,
      isShow: true,
      keepAlive: true, // 开启 缓存
      isBack: false
    }
  },
```


### 利用canvas 绘制 移动端与PC端手写签名

```HTML
<template>
  <section class="signature">
    <div class="signatureBox">
      <div class="canvasBox" ref="canvasHW">
        <canvas
          id="exitImg"
          ref="canvasF"
          v-if="!imgShow"
          @touchstart="touchStart"
          @touchmove="touchMove"
          @touchend="touchEnd"
          @mousedown="mouseDown"
          @mousemove="mouseMove"
          @mouseup="mouseUp"
        ></canvas>
        <div class="imgShowPng" v-if="imgShow">
          <img class="imgCanvas" :src="dataUrl" />
          <div class="my-sig-icon">我的签名</div>
        </div>
        <div class="btnBox">
          <div class="overwriteBtn" v-if="!imgShow" @click="overwrite">重写</div>
          <div class="commitBtn" v-if="!imgShow" @click="commit">提交</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { Toast } from "vant";
import axios from "axios";
import addSignApi from "../api/addSignApi/index";
export default {
  components: {
    [Toast.name]: Toast
  },
  data() {
    return {
      dataUrl: "",
      stageInfo: "",
      client: {},
      points: [],
      canvasTxt: null,
      startX: 0,
      startY: 0,
      moveY: 0,
      moveX: 0,
      endY: 0,
      endX: 0,
      w: null,
      h: null,
      isDown: false,
      isViewAutograph: this.$route.query.isViews > 0,
      contractSuccess: this.$route.query.contractSuccess,
      isCanvasX: null,
      isCanvasY: null,
      imgShow: false
    };
  },

  mounted() {
    this.$nextTick(() => {
      setTimeout(() => {
        var staffSignChird = localStorage.getItem("staffSign");
        if (staffSignChird == "null" || staffSignChird == null) {
          this.dataUrl = "";
          this.imgShow = false;
        } else {
          this.dataUrl = staffSignChird;
          this.imgShow = true;
        }
        // let canvas = this.$refs.canvasF;
        let canvas = document.querySelector("#exitImg");
        var canWidth =
          this.$refs.canvasHW.offsetWidth -
          this.$refs.canvasHW.offsetWidth * 0.925333;
        canvas.width = this.$refs.canvasHW.offsetWidth - canWidth;
        // 计算高度
        canvas.height = this.$refs.canvasHW.offsetHeight * 0.75 - 10;
        this.canvasTxt = canvas.getContext("2d");
        // 设置字体
        this.canvasTxt.font = "80px bold";
        // 设置颜色
        this.canvasTxt.fillStyle = "rgba(146,159,185,0.5)";
        // 设置水平对齐方式
        this.canvasTxt.textAlign = "center";
        // 设置垂直对齐方式
        this.canvasTxt.textBaseline = "middle";
        // 绘制文字（参数：要写的字，x坐标，y坐标）
        this.isCanvasX = canvas.width / 2;
        this.isCanvasY = canvas.height / 2;
        this.canvasTxt.fillText(
          "签 名 区",
          canvas.width / 2,
          canvas.height / 2
        );
        this.stageInfo = canvas.getBoundingClientRect();
      }, 800);
    });
    // 监听滚动 并获取 canvas信息
    window.addEventListener(
      "scroll",
      res => {
        let canvas = document.querySelector("#exitImg");
        if (canvas !== null) {
          this.stageInfo = canvas.getBoundingClientRect();
        }
      },
      false
    );
  },

  methods: {
    //mobile
    touchStart(ev) {
      ev = ev || event;
      ev.preventDefault();
      if (this.points.length === 0) {
        this.canvasTxt.clearRect(0, 0, this.isCanvasX * 2, this.isCanvasY * 2);
      }
      if (ev.touches.length == 1) {
        let obj = {
          x: ev.targetTouches[0].clienX,
          y: ev.targetTouches[0].clientY
        };
        this.startX = obj.x;
        this.startY = obj.y;
        this.canvasTxt.beginPath();

        this.canvasTxt.moveTo(this.startX, this.startY);
        this.canvasTxt.lineTo(obj.x, obj.y);
        this.canvasTxt.stroke();
        this.canvasTxt.lineWidth = "3";
        this.canvasTxt.closePath();
        this.points.push(obj);
      }
    },
    touchMove(ev) {
      ev = ev || event;
      ev.preventDefault();
      if (ev.touches.length == 1) {
        let obj = {
          x: ev.targetTouches[0].clientX - this.stageInfo.left,
          y: ev.targetTouches[0].clientY - this.stageInfo.top
        };
        this.moveY = obj.y;
        this.moveX = obj.x;
        this.canvasTxt.beginPath();
        this.canvasTxt.moveTo(this.startX, this.startY);
        this.canvasTxt.lineTo(obj.x, obj.y);
        this.canvasTxt.stroke();
        this.canvasTxt.lineWidth = "3";
        this.canvasTxt.closePath();
        this.startY = obj.y;
        this.startX = obj.x;
        this.points.push(obj);
      }
    },
    touchEnd(ev) {
      ev = ev || event;
      ev.preventDefault();
      if (ev.touches.length == 1) {
        let obj = {
          x: ev.targetTouches[0].clientX - this.stageInfo.left,
          y: ev.targetTouches[0].clientY - this.stageInfo.top
        };
        this.canvasTxt.beginPath();
        this.canvasTxt.moveTo(this.startX, this.startY);
        this.canvasTxt.lineTo(obj.x, obj.y);
        this.canvasTxt.stroke();
        this.canvasTxt.lineWidth = "3";
        this.canvasTxt.closePath();
        this.points.push(obj);
      }
    },
    //pc
    mouseDown(ev) {
      ev = ev || event;
      ev.preventDefault();
      if (1) {
        let obj = {
          x: ev.offsetX,
          y: ev.offsetY
        };
        this.startX = obj.x;
        this.startY = obj.y;
        this.canvasTxt.beginPath();
        this.canvasTxt.moveTo(this.startX, this.startY);
        this.canvasTxt.lineTo(obj.x, obj.y);
        this.canvasTxt.stroke();
        this.canvasTxt.lineWidth = "3";
        this.canvasTxt.closePath();
        this.points.push(obj);
        this.isDown = true;
      }
    },
    mouseMove(ev) {
      ev = ev || event;
      ev.preventDefault();
      if (this.isDown) {
        let obj = {
          x: ev.offsetX,
          y: ev.offsetY
        };
        this.moveY = obj.y;
        this.moveX = obj.x;
        this.canvasTxt.beginPath();
        this.canvasTxt.moveTo(this.startX, this.startY);
        this.canvasTxt.lineTo(obj.x, obj.y);
        this.canvasTxt.stroke();
        this.canvasTxt.lineWidth = "3";
        this.canvasTxt.closePath();
        this.startY = obj.y;
        this.startX = obj.x;
        this.points.push(obj);
      }
    },
    mouseUp(ev) {
      ev = ev || event;
      ev.preventDefault();
      if (1) {
        let obj = {
          x: ev.offsetX,
          y: ev.offsetY
        };
        this.canvasTxt.beginPath();
        this.canvasTxt.moveTo(this.startX, this.startY);
        this.canvasTxt.lineTo(obj.x, obj.y);
        this.canvasTxt.stroke();
        this.canvasTxt.lineWidth = "3";
        this.canvasTxt.closePath();
        this.points.push(obj);
        this.points.push({ x: -1, y: -1 });
        this.isDown = false;
      }
    },
    //重写
    overwrite() {
      if (this.points.length === 0) {
        // Toast("请签名 !");
        return;
      } else {
        this.canvasTxt.clearRect(
          0,
          0,
          this.$refs.canvasF.width,
          this.$refs.canvasF.height
        );
        this.points = [];
      }
    },
    //提交签名
    commit() {
      if (this.points.length === 0) {
        Toast("请签名后再提交 !");
        return;
      }
      this.imgUrl = this.$refs.canvasF.toDataURL();
      // console.log(this.$refs.canvasF.toDataURL()); //签名img回传后台
      var base641 = this.$refs.canvasF.toDataURL();
      var fileDate = this.base64ToFile(base641, "logo.png");
      let formData = new FormData();
      // 通过append()方法追加数据
      formData.append("file", fileDate);
      formData.append("category", 1);
      axios({
        method: "post",
        //服务器上传地址
        url: `http://b.***********`,
        data: formData,
        headers: {
          // 修改请求头
          "Content-Type": "multipart/form-data"
        }
      }).then(res => {
        this.dataUrl = res.data.url;
        this.imgShow = true;
        addSignApi
          .addSign({
            knowledgeId: localStorage.getItem(
              "knowledgeId",
              this.$route.params.knowledgeId
            ),
            picUrl: this.dataUrl,
            title: localStorage.getItem("listTitle")
          })
          .then(res => {
            Toast.success("签名成功");
          });
      });
    },
    base64ToFile(urlData, fileName) {
      let arr = urlData.split(",");
      let mime = arr[0].match(/:(.*?);/)[1];
      let bytes = atob(arr[1]); // 解码base64
      let n = bytes.length;
      let ia = new Uint8Array(n);
      while (n--) {
        ia[n] = bytes.charCodeAt(n);
      }
      return new File([ia], fileName, { type: mime });
    }
  }
};
</script>

<style  lang="scss" scoped>
.signatureBox {
  width: 100%;
  // height: calc(100% - 50px);
  height: 220px;
  box-sizing: border-box;
  overflow: hidden;
  background: #fff;
  z-index: 100;
  display: flex;
  flex-direction: column;
}
.canvasBox {
  box-sizing: border-box;
  height: 320px;
  flex: 1;
  .imgShowPng {
    position: relative;
    width: 92.5333%;
    height: 160px;
    margin: 0 auto;
    background-color: #f2f2f2;
    border: 1px solid rgba($color: #000000, $alpha: 0.1);
    border-radius: 4px;
    .imgCanvas {
      width: 100%;
      height: 160px;
    }
    .my-sig-icon {
      position: absolute;
      left: 0;
      top: 0;
      width: 60px;
      height: 20px;
      font-size: 12px;
      line-height: 20px;
      text-align: center;
      color: rgba(255, 255, 255, 1);
      background: rgba(146, 159, 185, 1);
      border-radius: 3px 0px 0px 0px;
    }
  }
}
canvas {
  background-color: #f2f2f2;
  border: 1px solid rgba($color: #000000, $alpha: 0.1);
  border-radius: 4px;
}
.btnBox {
  display: flex;
  justify-content: space-between;
  width: 150px;
  height: 32px;
  text-align: center;
  line-height: 32px;
  margin: 0 auto;
  margin-top: 10px;
  margin-bottom: 18px;
  .overwriteBtn {
    width: 70px;
    height: 32px;
    font-size: 14px;
    color: rgba(64, 158, 255, 1);
    background: rgba(255, 255, 255, 1);
    border: 1px solid rgba(64, 158, 255, 1);
    border-radius: 197px;
  }
  .commitBtn {
    width: 70px;
    height: 32px;
    font-size: 14px;
    color: rgba(255, 255, 255, 1);
    background: rgba(64, 158, 255, 1);
    border-radius: 197px;
  }
}
</style>
```


### 封装全局可调用 组件

###### 新建 JS 文件

```JS
import Vue from 'vue';
//  引入当前组件
import warning from './warning.vue'
const warningBox = Vue.extend(warning)
warning.install = function (data) {
  let instance = new warningBox({
    data
  }).$mount()
  document.body.appendChild(instance.$el)
  Vue.nextTick(() => {
    instance.show = true
  })
}

export default warning

```

###### main.js 里面 引入

```JS
//  全局预警通知弹窗组件
import warning from './layout/components/warning/warning.js';
Vue.prototype.$warning = warning.install;
```
###### 调用

```js
  this.$warning(); 
```

### 利用vuex 不相干的组件 全局更改数据


###### vuex内获取数据

```js

const store = new Vuex.Store({
  state: {
    comingCount: "",
    unreadNumCount: ""
  },
  mutations: {
    getComingCounts() {
      navbarApi.getComingCount().then(res => {
        if (res.errorCode == 0) {
          if (res.todoCount.length !== 0 && res.todoCount !== null) {
            this.state.comingCount = res.todoCount;
          } else {
            this.state.comingCount = false;
          }
        }
      });
    },
    // 获取预警数量
    getWarningCounts() {
      navbarApi.getWarningCount().then(res => {
        if (res.errorCode == 0) {
          if (res.unreadNum.length !== 0 && res.unreadNum !== null) {
            this.state.unreadNumCount = res.unreadNum;
          } else {
            this.state.unreadNumCount = false;
          }
        }
      });
    }
  },
  modules: {
    app,
    settings,
    user
  },
  getters
})


```

###### 需要更改数据的组件内 计算属性计算

```js
  computed: {
    numberFn() {
      return this.$store.state.comingCount;
    },
    numberFnTwo() {
      return this.$store.state.unreadNumCount;
    }
  },

```

######  调用方法 更改状态

```JS
    this.$store.commit("getComingCounts");
    this.$store.commit("getWarningCounts");
```

### 移动端input输入框 关闭后 页面底部留白

```JS
   //失焦后强制让页面归位
    changeCount() {
      window.scroll(0, this.scrollTop);
    },
    scroll() {
      let scrollTop =
        window.pageYOffset ||
        document.documentElement.scrollTop ||
        document.body.scrollTop;
      this.scrollTop = scrollTop;
    }
   // 首先获取 当前 offsetop
  created() {
    window.addEventListener("scroll", this.scroll);
  }

```

### 前台input框表格实时搜索

```html
  <!-- 输入框 -->
<el-input placeholder="请输入搜索内容" suffix-icon="el-icon-search" v-model="inputAll"></el-input>
  <!-- 表格内容  :data = "搜索结果" -->
<el-table :data="tables" style="width: 100%" height="625px"></el-table>
```

```js
computed: {
  tables() {
      if (this.inputAll !== "") {
        return this.tableData.filter(data => {
          // some() 方法用于检测数组中的元素是否满足指定条件;
          // some() 方法会依次执行数组的每个元素：
          // 如果有一个元素满足条件，则表达式返回true , 剩余的元素不会再执行检测;
          // 如果没有满足条件的元素，则返回false。
          // 注意： some() 不会对空数组进行检测。
          // 注意： some() 不会改变原始数组。
          // 该方法对大小写敏感！所以之前需要toLowerCase()方法将所有查询到内容变为小写。
          return Object.keys(data).some(key => {
            return (
              String(data[key])
                .toLowerCase()
                .indexOf(this.inputAll) > -1
            );
          });
        });
      } else {
        return this.tableData;
      }
  }
}
```

<hr/>

# Element 

### 后台使用 Panjiachen 模板
> 需要使用以下打包命令
###### Build

```bash
# build for test environment
npm run build:stage

# build for production environment
npm run build:prod
```
######  关闭 语法规范 或修改语法规范 避免报错

```js
module.exports = {
  root: true,
  parserOptions: {
    parser: 'babel-eslint',
    sourceType: 'module'
  },
  env: {
    browser: true,
    node: true,
    es6: true,
  },
  extends: ['plugin:vue/recommended', 'eslint:recommended'],
}

```

### 提取element 的img方法 使用图片查看器

######  引入img的dom
```html
    <el-image ref="preview" style="width: 0; height: 0" :src="url" :preview-src-list="urlList"></el-image>
    
```
###### 查看图片 点击事件

```js
   openPhotos(picUrl) {
      if (picUrl !== null && picUrl !== "") {
        // 获取图片
        this.urlList = picUrl.split(",");
        this.url = this.urlList[0];
        this.$refs.preview.clickHandler();
      }
    },
```
### element 通知弹框 只显示一次
###### element的通知框 可以无限被点击 造成叠加
```JS
    // 先清除上一次
    this.$message.closeAll();
    this.$message({})
```
### element 分页器

> DOM 部分

```html
   <!-- 表格数据格式 -->
    <el-table
      :data="pageData"
      style="width: 100%"
      tooltip-effect="dark"
      cell-class-name="table-style"
      v-loading="answerLoading"
      :height="tableHeight"
      :row-class-name="tableRowClassName"
      :row-key="(row)=>{ return row.fodId}"
      @selection-change="selChange"
    >
      <el-table-column type="selection" fixed="left" width="42" :reserve-selection="true"></el-table-column>
      <el-table-column type="index" fixed="left" label="序号" :index="typeIndex" width="60"></el-table-column>
    </el-table>


  <!-- 分页器 -->
    <el-pagination
      class="pagination"
      layout="prev, pager, next"
      ref="pagination"
      :page-size="pageSize"   // 每页显示条目个数
      :total="total"  // 总条目数
      :page-count="Math.ceil(total / pageSize)"  // 总页数，total和page-count设置任意一个就可以达到显示页码的功能如果要支持 page-sizes 的更改，则需要使用 total 属性
      :background="true"  // 背景色
      :current-page="currpage"  // 当前页数
      hide-on-single-page  // 只有一页时是否隐藏
      @current-change="currentPage"
    ></el-pagination>

```
> JS部分

```js
  data() {
    return {
      currpage: 1, // 当前页
      tableData: [], // 当前总数据
      selIds:"",
      tableHeight:undefined,
      }
  }
  // 计算属性 计算
  computed: {
    total() {
      return this.tableData.length;
    },
    pageSize() {
      return (this.tableHeight - 40) / 40 - 1;
    },
    pageData() {
      if (this.tableData.length > 0) {
        return this.tableData.slice(
          (this.currpage - 1) * this.pageSize,
          this.currpage * this.pageSize
        );
      } else {
        return [];
      }
    }
  },
  methods: {
      // 切换分页器
    currentPage(value) {
      this.currpage = value;
    },
      // 跳转
    getParams() {
      // 是否跳转过来
      if (this.$route.query.fodId === undefined) {
        this.isFromUpcomming = false;
      } else {
        this.isFromUpcomming = true;
        this.paramsId = this.$route.query.fodId;
      }
    },
     // 表格序号
    typeIndex(index) {
      return index + (this.currpage - 1) * this.pageSize + 1;
    },
     // 选项切换change事件
    selChange(val) {
      this.selIds = val;
    },
    init(){
      api.then(res=>{
            // 重置分页器当前页数
          this.currpage = 1;
          // 判断 如果是 跳转来的 修改分页器  isFromUpcomming 判断是否是跳转来的
          if (this.isFromUpcomming === true) {
            this.tableData.forEach((ele, index) => {
              if (ele.fodId === this.paramsId) {
                var count =
                  parseInt(index / ((this.tableHeight - 40) / 40 - 1)) + 1;
                this.currentPage(count);
                this.$refs.pagination.currentPage = count;
              }
            });
            this.isFromUpcomming === false;
          }
      })
    }
  }
  // 获取 表格高度 自适应
  mounted() {
    this.tableHeight =
      parseInt((document.documentElement.clientHeight - 220) / 40) * 40; //获取浏览器可视区域高度
    window.onresize = () => {
      this.tableHeight =
        parseInt((document.documentElement.clientHeight - 220) / 40) * 40;
    };
  },

```


<hr/>

# Vant

### 选择器 三级联动 (效果:省市区选择器;结果:数据自定义)
```html
     <van-action-sheet v-model="branchShow" :round="false" class="linkage" :lock-scroll="false">
        <van-picker
          show-toolbar
          :loading="depLoading"
          :item-height="80"
          :visible-item-count="5"
          :columns="depColumns"
          @confirm="depConfirm"
          @change="depChange"
          @cancel="branchShow = false"
          title="选择**"
        />
      </van-action-sheet>
```
###### Data return 内的数据

```js
  data() {
    return {
      // 部门选择器picker数据数组
      depColumns: [
        {
          values: [],
          className: "column1"
        },
        {
          values: [],
          className: "column2"
        },
        {
          values: [],
          className: "column3"
        }
      ],
      // 选择器名字
      branchName: "",
      // 选择器loding
      depLoading: false,
      // 选择器二级选择器id,如果改变,获取三级id
      depTwoId: "99999999999999999999999",
      // 初始选择器信息
      initDep: {}
    };
  },
```

######  获取并添加数据

```JS
    // 选择器确定事件
    depConfirm(value) {
      var id = "";
      if (value[2] == undefined && value[1] == undefined) {
        id = value[0].id;
        this.branchName = value[0].text;
      } else if (value[2] == undefined) {
        id = value[1].id;
        this.branchName = value[1].text;
      } else {
        id = value[2].id;
      }
      infoApi.setInfo({ "dep.depId": id }).then(res => {
        if (res.errorCode === 0) {
          this.$toast.success("修改成功");
        }
        this.branchShow = false;
        this.branchName = value[2].text;
      });
    },
    // 选择器更改选项事件
    depChange(val, val2) {
      // 第二列选中行的下标
      var valIndex = val.children[1].currentIndex;
      // 第二列数组
      var valArr = val.children[1].options;
      // 拿到第二列选中行的id,用来获取第三列数据
      var depTwoId = valArr[valIndex].id;
      if (depTwoId !== this.depTwoId) {
        this.depLoading = true;
        var that = this;
        infoApi
          .depList({
            superiorId: depTwoId
          })
          .then(res => {
            var arr = res.depList;
            var values3 = [];
            arr.forEach((ele3, index3) => {
              var obj3 = {
                id: ele3.depId,
                text: ele3.depName
              };
              values3.push(obj3);
            });

            this.depLoading = false;
            val.setColumnValues(2, values3 || []);
          });
      }
      this.depTwoId = depTwoId;
    },
```

<hr/>

# ECharts
> 留坑 后面更

<hr/>


# 微信

### 微信获取 Code

```JS
        var WXCode;
        function getCode() { // 非静默授权，第一次有弹框
            WXCode = '';
            WXCode = getUrlCode().code // 截取code
            // 如果没有 去获取
            if (!WXCode) {
                window.location.href = " ";
            }
            if (WXCode == null || WXCode === '') { // 如果没有code，则去请求
                // 这个地址就是 你请求后的 data.url 的地址
                window.location.href ="";
            } else {
                // 你自己的业务逻辑
            }
        }
        function getUrlCode() { // 截取url中的code方法
            var url = location.search;
            var theRequest = new Object();
            if (url.indexOf("?") != -1) {
                var str = url.substr(1);
                var strs = str.split("&");
                for (var i = 0; i < strs.length; i++) {
                    theRequest[strs[i].split("=")[0]] = (strs[i].split("=")[1])
                }
            }
            return theRequest
        }
        getCode()
```

### 禁止用户字体自定义缩小放大

```JS
 function resizePage() {
    if (typeof WeixinJSBridge == "object" && typeof WeixinJSBridge.invoke == "function") {
      handleFontSize();
    } else {
      if (document.addEventListener) {
        document.addEventListener("WeixinJSBridgeReady", handleFontSize, false);
      } else if (document.attachEvent) {
        document.attachEvent("WeixinJSBridgeReady", handleFontSize);
        document.attachEvent("onWeixinJSBridgeReady", handleFontSize);
      }
    }

    function handleFontSize() {
      // 设置网页字体为默认大小
      WeixinJSBridge.invoke('setFontSizeCallback', {
        'fontSize': 0
      });
      // 重写设置网页字体大小的事件
      WeixinJSBridge.on('menu:setfont', function () {
        WeixinJSBridge.invoke('setFontSizeCallback', {
          'fontSize': 0
        });
      });
    }
  };

```

### 微信分享 未注册用户 进入分享链接限制查看

###### 分享方法 在链接后面拼接参数
```JS
    var href = window.location.href.split("#")[0];
        axios.defaults.headers.post["Content-Type"] =
          "application/x-www-form-urlencoded";
        var params = new URLSearchParams();
        params.append("signUrl", href);
        axios({
          method: "post",
          url: "http://b.matr******ign",
          withCredentials: true,
          data: params
        }).then(function(resData) {
          wx.config({
            debug: false, // 开启调试模式,调用的所有api的返回值会在客户端alert出来，若要查看传入的参数，可以在pc端打开，参数信息会通过log打出，仅在pc端时才会打印。
            appId: resData.data.appid, // 必填，公众号的唯一标识
            timestamp: resData.data.timestamp, // 必填，生成签名的时间戳
            nonceStr: resData.data.nonceStr, // 必填，生成签名的随机串
            signature: resData.data.signature, // 必填，签名，见附录1
            jsApiList: [
              "onMenuShareTimeline", // 朋友圈
              "onMenuShareAppMessage" // 好友
              //此处列表，用到哪些方法，必须要在此提前声明，我当时要用到hideMenuItems，但是因为没有在此出声明，一直不起作用，
            ]
          });
          var showImga = "";
          if (res.knowledge.titlePic == "" || res.knowledge.titlePic == null) {
            showImga = "http://b.m*****x_logo.png";
          } else {
            showImga = res.knowledge.titlePic;
          }
          var isContentId = res.knowledge.knowledgeId;
          var isCategory = res.knowledge.category;
          var isTitle = res.knowledge.title;
          wx.ready(function() {
            wx.onMenuShareTimeline({
              title: res.knowledge.title, // 分享标题
              desc:
                res.knowledge.subTitle == null
                  ? "******"
                  : res.knowledge.subTitle, // 分享描述
              link: `http://b.matr*****tent&state=${res.knowledge.knowledgeId}`, // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
              imgUrl: showImga, // 分享图标
              success: function(res) {
                contentApi
                  .wxShare({
                    contentId: isContentId,
                    category: isCategory,
                    title: isTitle
                  })
                  .then(res => {
                    console.log(res);
                  });
              },
              cancel: function() {
                // 用户取消分享后执行的回调函数
              }
            });
            wx.onMenuShareAppMessage({
              title: res.knowledge.title, // 分享标题
              desc:
                res.knowledge.subTitle == null
                  ? "******"
                  : res.knowledge.subTitle, // 分享描述
              link: `http://b******nt&state=${res.knowledge.knowledgeId}`, // 分享链接，该链接域名或路径必须与当前页面对应的公众号JS安全域名一致
              imgUrl: showImga, // 分享图标
              success: function(res) {
                contentApi
                  .wxShare({
                    contentId: isContentId,
                    category: isCategory,
                    title: isTitle
                  })
                  .then(res => {
                    console.log(res);
                  });
              },
              cancel: function() {
                // 用户取消分享后执行的回调函数
              }
            });
          });
```
###### 判断是否是从分享链接过来的

```js
 // 判断是分享页面进来的
    if (
      window.location.href.split("?")[1] == "" ||
      window.location.href.split("?")[1] == undefined ||
      window.location.href.split("?")[1] == null
    ) {
      mainBack.style.display = "none";
      });
```
<hr/>

# GIS

### 去除百度地图文字.logo

```css
 /* 去除百度地图文字 */
    .BMap_cpyCtrl {
      display: none;
    }

    /* 去除百度地图logo */
    .anchorBL {
      display: none;
    }
```

### 测距

```JS
  myDis = new BMapLib.DistanceTool(bMap);
  myDis.open(); //开启鼠标测距
```


### H5 获取位置

```JS
// 获取位置 HTTPS  协议
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition);
    } else {
        // HTTPS  协议
    }
}
function showPosition(position) {
    latitude = position.coords.latitude; // 纬度，
    longitude = position.coords.longitude; // 经度，
    initPoint(longitude, latitude);
}
getLocation();
```

### GIS 实时定位 移动动画

```JS
var bMap;
var geolocation;
var gc;
var g_sta = [];
function initMap(g_id, mapTypeSta) {
    // 我需要转换地图类型 所以 把变量 改为BMAP_NORMAL_MAP 即可,或者直接删除;
    bMap = new BMap.Map(g_id, {
        mapType: mapTypeSta,
    });
    // var g_centerPoint = new BMap.Point(116.331398, 39.897445);
    var g_centerPoint = new BMap.Point(114.701341, 38.287799);
    // 创建点坐标
    bMap.centerAndZoom(g_centerPoint, 16); // 中心点位置和默认放大
    bMap.setMinZoom(16);
    bMap.setMaxZoom(19);
    bMap.enableScrollWheelZoom(true); //启用滚轮放大缩小
    bMap.enableContinuousZoom(true); //启用地图惯性拖拽

    // 此处采用WX定位 舍弃 百度地图定位 与 H5 定位 H5定位需要建立在HTTPS协议上 
    // 百度地图定位 如果想要更精准 需要HTTPS协议 与开启SDK辅助定位
    // 以下百度地图 创建地理编码器注释
    // geolocation = new BMap.Geolocation();
    // gc = new BMap.Geocoder(); //创建地理编码器
}

var posStartEndList = []; // 移动的点位
var myMarkerLists = null; // 清除上个点位
var count = 1; // 首次定位
var _startPoint; // 开始点
var _endPoint; // 结束点
var newMyPoint; // 当前最新中心点

function initPoint(lng, lat) {
    var WGSPoint = new BMap.Point(lng, lat);
    var WGSPointArr = [];
    WGSPointArr.push(WGSPoint);
    posStartEndList.push(WGSPoint);
    // 删除第一个
    if (posStartEndList.length > 2) {
        posStartEndList.shift();
    }
    var convertor = new BMap.Convertor();
    // 查阅文档: 声明以下注释;
    // from	源坐标类型：
    //      1：GPS设备获取的角度坐标，WGS84坐标;
    //      2：GPS获取的米制坐标、sogou地图所用坐标;
    //      3：google地图、soso地图、aliyun地图、mapabc地图和amap地图所用坐标，国测局（GCJ02）坐标;
    //      4：3中列表地图坐标对应的米制坐标;
    //      5：百度地图采用的经纬度坐标;
    //      6：百度地图采用的米制坐标;
    // to目标坐标类型：
    //      5：bd09ll(百度经纬度坐标);
    //      6：bd09mc(百度米制经纬度坐标);
    convertor.translate(WGSPointArr, 1, 5, function (data) {
        if (data.status === 0) {
            var myIcon = new BMap.Icon(
                `../imgs/myIcon.svg`,
                new BMap.Size(60, 60), {
                    imageSize: new BMap.Size(60, 60),
                    offset: new BMap.Size(0, -15),
                }
            );
            var myMarkers = new BMap.Marker(data.points[0], {
                icon: myIcon,
            }); // 创建标注
            if (count === 1) {
                bMap.setCenter(data.points[0]);
            }
            count = 2;
        }
        convertor.translate(posStartEndList, 1, 5, function (data) {
            _startPoint = bMap.getMapType().getProjection().lngLatToPoint(data.points[0]);
            if (data.points.length == 1) {
                _endPoint = bMap.getMapType().getProjection().lngLatToPoint(data.points[0]);
                newMyPoint = data.points[0];
            } else {
                _endPoint = bMap.getMapType().getProjection().lngLatToPoint(data.points[1]);
                newMyPoint = data.points[1];
            }
            if (_startPoint !== undefined) {
                movepoint(_startPoint, _endPoint, myMarkers, 10, 60);
            }
        })
    });

}

//xoy1  x1 或者y1,  xoy2 x2或者y2 ,num 分割多少个点，m 第几个点
function getpointitem(xoy1, xoy2, num, m) {
    return (xoy2 - xoy1) / num * m + xoy1
}
// statpoint,开始点
// endpoint,结束点
// marker, 移动的marker
// timer, 间隔时间
// count  计数点
function movepoint(statpoint, endpoint, marker, timer, count) {
    var currentCount = 0;
    //两点之间匀速移动
    var intervalFlag = setInterval(function () {
        //两点之间当前帧数大于总帧数的时候，则说明已经完成移动
        if (currentCount >= count) {
            clearInterval(intervalFlag);
        } else {
            //动画移动
            currentCount++; //计数
            var x = getpointitem(statpoint.x, endpoint.x, count, currentCount);
            var y = getpointitem(statpoint.y, endpoint.y, count, currentCount);
            //根据平面坐标转化为球面坐标
            var pos = bMap.getMapType().getProjection().pointToLngLat(new BMap.Pixel(x, y));
            //更新坐标点
            marker.setPosition(pos);
            // 画点到地图上
            if (myMarkerLists !== null) {
                bMap.removeOverlay(myMarkerLists);
            }
            marker.disableMassClear();
            bMap.addOverlay(marker);
            myMarkerLists = marker;
        }
    }, timer);
}

```

### 获取行政区 并描画

```html
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no" />
    <style type="text/css">
        body,
        html {
            width: 100%;
            height: 100%;
            margin: 0;
        }
        #g-map {
            width: 100%;
            height: 100%;
        }
    </style>
    <script type="text/javascript" src="https://api.map.baidu.com/api?v=2.0&ak=wSylPL9dkhvYGjKCtsTzz7dGQdP47Rtz">

    </script>
    <script src="./Jisyan.js"></script>
    <title></title>
</head>

<body>
    <div id="g-map"></div>
</body>

</html>
<script>
    // 百度地图API功能
    var map = new BMap.Map("g-map");
    map.centerAndZoom(new BMap.Point(118.907632, 32.079094), 10);
    map.enableScrollWheelZoom();
    var bdary = new BMap.Boundary();
    var asdwad = [];
    bdary.get("南京", function (rs) { //获取行政区域
        var count = rs.boundaries.length; //行政区域的点有多少个
        asdwad = rs.boundaries[2]
        for (var i = 0; i < count; i++) {
            var ply = new BMap.Polygon(rs.boundaries[i], {
                strokeColor: "#f09",
                fillColor: "#f09",
                strokeWeight: 2,
                strokeOpacity: 1,
                fillOpacity: 0.01,
                strokeStyle: "solid",
            }); //建立多边形覆盖物
            map.addOverlay(ply); //添加覆盖物
        }
    });
</script>
```
<hr/>


# 百度地图 基础使用流程

#### 1.
        百度地图官方文档地址(3.0):http://lbsyun.baidu.com/index.php?title=jspopular3.0
        
        使用百度地图流程: 注册百度账号 ==> 成为百度开发者 ==> 获取服务密匙(AK) ==> 使用百度地图

        获取AK流程: 登录百度账号 ==> 打开控制台 ==> 应用管理 ==> 我的应用 ==> 创建应用
        
        创建地图:  
                1. head里面引入 百度的api || ak="你的密匙" 输入你的AK值   我当前输入的是我 创建的AK wSylPL9dkhvYGjKCtsTzz7dGQdP47Rtz
                2. 写入一个div 并命名一个ID  我在这命名 "myMap" 并设置 宽高 100% 100%
#### 2.

```js
        var map = new BMap.Map("myMap"); // 创建地图实例 输入你盒子的id 用于存放地图
        var point = new BMap.Point(116.404, 39.915); // 创建点坐标  116.404就是Lng 也就是 经度 39.915 就是维度 经纬度确定一个点
        map.centerAndZoom(point, 15); // 初始化地图，设置中心点坐标point就是你通过经纬度确定的点 把这个点 当做中心点
        //  15 是 地图缩放级别(你一进来你能看到的地图范围)
        map.enableScrollWheelZoom(true); //开启鼠标滚轮缩放
```
#### 3. 
                        WGS-84坐标系 :
                            全称: World Geodetic System一1984 Coordinate System(世界大地测量系统一1984坐标系);

                            简介:
                            一种国际上采用的地心坐标系。坐标原点为地球质心，其地心空间直角坐标系的Z轴指向
                            BIH （国际时间服务机构）1984.0定义的协议地球极（CTP)方向， X轴指向BIH 
                           1984.0的零子午面和CTP赤道的交点，Y轴与Z轴、X轴垂直构成右手坐标系，称为1984年世界大地坐标系统。

                           意义: 建立WGS-84世界大地坐标系的一个重要目的，是在世界上建立一个统一的地心坐标系

                    // 百度地图 坐标转换 详情见 官方文档 : http://lbsyun.baidu.com/index.php?title=jspopular3.0/guide/coorinfo
                        BD09坐标系 :

                            首先了解WEB地图常用的坐标系有哪些，主要是三种WGS84、GCJ02和BD09，其中GCJ02[见下面] 和 BD09只是在国内使用。

                            简介:
                            BD09为百度坐标系，在GCJ02坐标系基础上再次加密 其中BD09LL表示百度经纬度坐标 BD09MC表示百度墨卡托米制坐标
                            BD09分为BD09LL和BD09MC 其中，BD09LL是在标准经纬度的基础上进行GCJ-02加偏之后，再加上百度自身的加偏算法，
                            也就是在标准经纬度的基础之上进行了两次加偏，该坐标系的坐标值为经纬度格式，单位为度

                        GCJ02坐标系 :又称火星坐标系，是由中国国家测绘局制定的地理坐标系统，是由WGS84加密后得到的坐标系

                    //  注意 这里获取的 是 WGS84 坐标 所以用在百度地图上 需要 转为BD09坐标 ===> BD09:百度坐标系
                    // openLocation 另一种Gis开发技术 不必了解
                    type: 'wgs84', // 默认为wgs84的gps坐标，如果要返回直接给openLocation用的火星坐标，可传入'GCJ02'
                    type: 'wgs84', // 默认为wgs84的gps坐标，如果要返回直接给openLocation用的火星坐标，可传入'GCJ02'

# 正则

### 判断class名称

```JS
e.target.className.split(/\s+/)[0]="className" 
```

### 手机号
```JS
 /^1[3456789]\d{9}$/
```

### 提取中文字符

```JS
/^\D+(?=\d)/.exec(String);
```

### 提取字符串中的数字

```JS
String.replace(/[^0-9]/ig, "");
```

<hr/>


# Axios

### Axios 二次封装

> 封装 request.js 文件

```js
import axios from "axios";
import qs from "qs";
// 创建一个axios实例
const service = axios.create({
  baseURL: "http://**********/", // 配置总地址 /setUser/3
  timeout: 5000, // 设置超时时间
  withCredentials: true // 允许携带cookie code
});
service.interceptors.request.use(
  config => {
    return config;
  },
  error => {
    console.log(error); // for debug
    return Promise.reject(error);
  }
);
service.interceptors.response.use(
  response => {
    const res = response.data;
    return res;
  },
  error => {
    console.log("err" + error); // for debug
    return Promise.reject(error);
  }
);

// post 请求和 set 请求 axios对两种请求方式是不同的
function http(config) {
  // toLowerCase 将字符串转换成小写
  if (config.method.toLowerCase() === "post") {
    config.data = qs.stringify(config.data, {
      arrayFormat: "repeat",
      allowDots: true
    });
  } else {
    config.params = config.data;
  }
  return service(config);
}

export default http;

```

> 模块化 请求接口

```js
import request from "../request";
// 接口
function addXXXX(data) {
    return request({
        url: "/add", // 地址
        method: "POST", // 请求方式
        data: data
    });
}
export default {
    addXXXX
};
```
> 调用接口

```js
import api from "../../api/api/learn";
api.addXXXX({ searchKey: this.searchValue }).then(res => {})
```

<hr/>

#  flexible  postcss-px2rem

### npm

> npm install lib-flexible --save  
> npm install postcss-px2rem --save

### 删除 \<meta name='viewport' > 标签
>flexible会为页面根据屏幕自动添加<meta name='viewport' >标签，动态控制initial-scale，maximum-scale，minimum-scale等属性的值

### 引入lib-flexible
main.js里
>import 'lib-flexible'

### 配置postcss-px2rem
```js
module.exports = {
    css: {
        loaderOptions: {
          css: {},
  postcssOptions: {
          postcss: {
            plugins: [
              require('postcss-px2rem')({
                remUnit: 37.5
              })
            ]
          }
        }
}
    },
}

```


# Xgplayer (视频)


```html
<template>
  <div>
    <div id="mse"></div>
    <input type="text" class="input" v-model="searchText" @keyup="debounce" placeholder="防抖" />
    <div @click="throttle">节流</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      searchText: "",
      lastTime: ""
    };
  },
  created() {},
  mounted() {
    this.init();
  },
  methods: {
    init() {
      new Player({
        el: document.querySelector("#mse"),
        url:
          "//s1.pstatp.com/cdn/expire-1-M/byted-player-videos/1.0.0/xgplayer-demo.mp4",
        fluid: true,
        // fitVideoSize: "auto",
        volume: 0.6, // 音量
        autoplay: false, // 自动播放
        loop: true, // 循环播放
        poster:
          "http://n1.itc.cn/img8/wb/recom/2016/05/04/146234627755814871.JPEG", // 视频封面
        playbackRate: [0.5, 0.75, 1, 1.5, 2], // 倍速播放的值
        defaultPlaybackRate: 1, // 倍速播放的默认值
        download: true,
        danmu: {
          comments: [
            //弹幕数组
            {
              duration: 15000, //弹幕持续显示时间,毫秒(最低为5000毫秒)
              id: "1", //弹幕id，需唯一
              start: 3000, //弹幕出现时间，毫秒
              prior: true, //该条弹幕优先显示，默认false
              color: true, //该条弹幕为彩色弹幕，默认false
              txt: "我是弹幕,我是弹幕,我是弹幕", //弹幕文字内容
              style: {
                //弹幕自定义样式
                color: "#ff9500",
                fontSize: "16px",
                borderRadius: "50px",
                padding: "5px 11px",
                backgroundColor: "rgba(255, 255, 255, 0.1)"
              },
              mode: "top" //显示模式，top顶部居中，bottom底部居中，scroll滚动，默认为scroll
              // el: DOM //直接传入一个自定义的DOM元素作为弹幕，使用该项的话会忽略所提供的txt和style
            }
          ],
          area: {
            //弹幕显示区域
            start: 0, //区域顶部到播放器顶部所占播放器高度的比例
            end: 1 //区域底部到播放器顶部所占播放器高度的比例
          },
          closeDefaultBtn: false, //开启此项后不使用默认提供的弹幕开关，默认使用西瓜播放器提供的开关
          defaultOff: false //开启此项后弹幕不会初始化，默认初始化弹幕
        }
        // textTrack: [
        //   {
        //     src: "./textTrack-1.vtt",
        //     kind: "subtitles",
        //     label: "字幕1",
        //     srclang: "zh",
        //     default: true
        //   },
        // textTrackActive: "click"
      });
    },
    debounce() {
      //定时器中的变量定义，会在每次执行函数的时候重复定义变量，产生严重的内存泄漏
      if (timer) {
        //timer在全局中定义
        clearTimeout(timer);
      }
      var timer = setTimeout(function() {
        timer = undefined;
      }, 200);
    },
    throttle() {
      let that = this;
      let now = + new Date();
      if (this.lastTime && this.lastTime - now < 2000) {
        //lastTime跟timer在全局定义
        clearTimeout(timer);
      }
      var timer = setTimeout(function() {
        console.log("点击");
        this.lastTime = +new Date();
      }, 200);
    }
  }
};
</script>

```


<hr/>


# 基础爬虫相关 

> 两种简单爬虫方式 

### python 抓取网页手机号

```py
from phone import Phone
import urllib.request
import re

def get_html(url):
    page = urllib.request.urlopen(url)
    html = page.read().decode('utf-8')
    return html

reg = r'1[3|4|5|7|8]\d{9}'  # 正则表达式
# print(reg)
# print(nodeUrl)
reg_img = re.compile(reg) 
nodeUrl = input('请输入网址:')
imglist = reg_img.findall(get_html(nodeUrl))  # 进行匹配
for img in imglist:
    # print(img)
    if __name__ == "__main__":
        phoneNum = img
    info = Phone().find(phoneNum)
    if info['city'] == "苏州":
        print(img, info['province'],"省", info['city'],"市",info['phone_type'])
```

### Node 抓取并下载图片

```js
const request = require('request');
const fs = require('fs');
const cheerio = require('cheerio');
request('https://www.zcool.com.cn/', function (error, response, body) {
    //获取爬取网站的页面信息
    const $ = cheerio.load(body)
    //目标网站图片链接地址数组
    let imgs = []
    // 用正则判断数组中的路径是否存在https
    var _z = /(http[s]?|ftp)/;
    // 遍历所有
    $('img').each((i, e) => { 
        var src = $(e).attr('alt');
        if (!_z.test(src)) {
            src = src.replace(/\/{2}/, 'https://') //因为有些图片不可下载 所以用正则判断一下
        }
        imgs.push(src)
    })
    // 下载数组里的图片
    for (let index = 0; index < imgs.length; index++) {
        if (imgs[index].indexOf('http') !== -1) {
            request(imgs[index]).pipe(fs.createWriteStream(`./qiantuImg/${index}.png`)) //这里为了省事 就直接用下标命名了
        }
    }
});
```
