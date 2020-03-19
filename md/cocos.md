### 节点显示隐藏
---

``` 
node.active=true;
node.active=false;
```
### 动态获取资源
---
1. 图片资源获取
* 在assets下新建resources，资源需放在这个文件夹下

``` 
cc.loader.loadResDir('header', cc.SpriteFrame,  (err, spriteframe, urls)=> {
    this.GameRes.imgs = this.sortArray(spriteframe, urls);
})
```
* 按照  ASCLL码表 对获取的数据进行排序(保证获取的数据是按上传时候排序的)
```
sortArray: function (assets, names) {
    var name_indexs = {};
    var array = new Array();
    for (var i = 0; i < names.length; i++) {
        array.push(names[i]);
        name_indexs[names[i]] = i;
    }
    array = array.sort();
    var tmp_assets = [];
    for (var i = 0; i < array.length; i++) {
        var index = name_indexs[array[i]];
        tmp_assets[i] = assets[index];
    }
    return tmp_assets;
},
```
### 进度条加载
---
```
cc.director.preloadScene('main', this.onProgress.bind(this),  () =>{
    cc.director.loadScene('main');
})
onProgress: function (completedCount, totalCount, item) {
    this.progressBar.progress = completedCount / totalCount;
    //进度条长度的百分比
    this.label.string = Math.floor(completedCount / totalCount * 100) + "%";
}
```
### 节点操作
---
* 查找节点
```
cc.find("Canvas/main/imgBgBetPool_png/num")
```
* 获取转换为label
```
getComponent(cc.Label)
```
* 销毁节点
```
node.destroy()
```
* 销毁所有子节点
```
node.destroyAllChildren()
```
* 更改节点的图片
```
node.getComponent(cc.Sprite).spriteFrame=this.GameRes.imgs[i]
```
* 新建图片节点
```
var node = new cc.Node('Sprite');
var sp = node.addComponent(cc.Sprite);
sp.spriteFrame = pokerSpriteFrame[res.pokers[0]]; //资源
node.name = pokerSpriteFrame[res.pokers[0]].name; 
node.parent = this.park_arr;
```
* 新建label节点
```
var node=new cc.Node();
var label=node.addComponent(cc.Label);
label.string=10;
label.fontSize=25;
node.parent=blackBg;
```
* 节点自定义属性
```
node.attr({
    'index':1
})
```
* 节点更改颜色
```
node.color={r:red,g:green,b:blue,a:255}
```
### 动作
---
* 动作创建和赋值
```
var action = cc.moveTo(0.6, 360, -3);
node.runAction(action);
```
### 组件使用
---
1. 新建组件,文件名GameRes
```
module.exports = {
    imgs:[]
}
```
2. 使用组件
```
this.GameRes=require('GameRes');
this.GameRes.imgs
```
### 使用动画
---
```
 properties: {
     animshow: cc.Animation
 }
 this.animshow.play('clown_alert');
```
### 预制键 prefab
---
1. 获取
```
item_prefab: cc.Prefab,
```
2. 使用
```
var item = cc.instantiate(this.item_prefab);
item.parent = this.list;
```
### 滚动键
---
```
day_scroll_view: function (scrollView) {
    var _this = this;
    var scorll_y = scrollView.content.y;
},
```
### 发送请求
---
1. 发送请求
```
ajax: function (options) {
    /**
     * 传入方式默认为对象
     * */
    options = options || {};
    /**
     * 默认为GET请求
     * */
    options.type = (options.type || "GET").toUpperCase();
    /**
     * 返回值类型默认为json
     * */
    options.dataType = options.dataType || 'json';
    /**
     * 默认为异步请求
     * */
    options.async = options.async || true;
    /**
     * 对需要传入的参数的处理
     * */
    var params = this.getParams(options.data);
    var xhr;
    /**
     * 创建一个 ajax请求
     * W3C标准和IE标准
     */
    if (window.XMLHttpRequest) {
        /**
         * W3C标准
         * */
        xhr = new XMLHttpRequest();
    } else {
        /**
         * IE标准
         * @type {ActiveXObject}
         */
        xhr = new ActiveXObject('Microsoft.XMLHTTP')
    }
    xhr.onreadystatechange = function () {
        if (xhr.readyState == 4) {
            var status = xhr.status;
            if (status >= 200 && status < 300) {
                options.success && options.success(xhr.responseText, xhr.responseXML);
            } else {
                options.fail && options.fail(status);
            }
        }
    };
    if (options.type == 'GET') {
        xhr.open("GET", options.url + '?' + params, options.async);
        xhr.send(null)
    } else if (options.type == 'POST') {
        /**
         *打开请求
         * */
        xhr.open('POST', options.url, options.async);
        /**
         * POST请求设置请求头
         * */
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        /**
         * 发送请求参数
         */
        xhr.send(params);
    }
},
```
2. 使用请求
```
ajax({
    url: URL + '/web_api/game_hall', //请求地址
    type: 'POST',   //请求方式
    data: { token: token }, //请求参数
    dataType: "json",     // 返回值类型的设定
    async: false,   //是否异步
    success: function (response, xml) {
        // console.log(response);   //   此处执行请求成功后的代码
        // response;
    },
    fail: function (status) {
        console.log('状态码为' + status);   // 此处为执行成功后的代码
    }
});
```
### 绑定点击事件
1. 使用方法
```
this.buttonClick.node.on( cc.Node.EventType.TOUCH_END, this.header_callback,this);
header_callback: function (event, customEventData) {
    console.log(event)
}
```
2. 事件
```
cc.Node.EventType.TOUCH_START 当手按下时触发
cc.Node.EventType.TOUCH_END 当手抬起时候
cc.Node.EventType.TOUCH_MOVE 当手按下滑动时
cc.Node.EventType.TOUCH_CANCEL 当手按下滑动后 抬起时
```
### 解绑点击事件
```
this.buttonClick.node.off( cc.Node.EventType.TOUCH_END, this.header_callback,this);
```
### 音频
###### 预加载音频
> assets/sound/backGroundMusic(backGroundMusic是MP3文件)
```
cc.loader.loadResDir("Sound/backGroundMusic", cc.AudioClip, (err, audioClip) => {
    console.log(audioClip);
});
```
###### 使用AudioSource组件播放
1. 在层级管理器上创建一个空节点
2. 选中空节点，在属性检查器最下方点击添加组件->其他组件->AudioSource来添加AudioSource
3. 将资源管理器中所需要的音频资源拖拽到AudioSource组件Clip中，可以通过参数控制播放
* 通过脚本控制AudioSource组件
```
cc.Class({
    extends: cc.Component,

    properties: {
        audioSource: {
            type: cc.AudioSource,
            default: null
        },
    },

    play: function () {
        this.audioSource.play();
    },

    pause: function () {
        this.audioSource.pause();
    },
});
```
###### 使用AudioEngine播放
* AudioEngine与AudioSource都能播放音频，区别在于AudioSource是组件，可以添加到场景由编辑器设置。而AudioEngine是引擎提供的纯API，只能在脚本中调用
1. 在脚本的properties中定义一个AudioClip资源对象
2. 直接使用 cc.audioEngine.play(audio,loop,volume)
```
cc.Class({
    extends: cc.Component,

    properties: {
        audio: {
            default: null,
            type: cc.AudioClip
        }
    },

    onLoad: function () {
        this.current = cc.audioEngine.play(this.audio, false, 1);
    },

    onDestroy: function () {
        cc.audioEngine.stop(this.current);
    }
});
```
###### audioengine类型
- play 播放音频
- setLoop 设置音频是否循环
- isLoop 获取音频循环状态
- setVolume 设置音量（0.0~1.0）
- getVoluem 获取音量（0.0~1.0）
- setCurrentTime 设置当前的音频时间
- getCurrentTime 获取当前的音频播放时间
- getDuration 获取音频总时长
- getState 获取音频总时长
- setFinishCallback 设置一个音频结束后的回调
- pause 暂停正在播放音频
- pauseAll 暂停现在正在播放的所有音频
- resume 恢复播放指定的音频
- resumeAll 恢复播放所有之前暂停的所有音频
- stop 停止播放指定音频
- stopAll 停止正在播放的所有音频
- setMaxAudioInstance 设置一个音频可以设置几个实例
- getMaxAudioInstance 获取一个音频可以设置几个实例
- uncache 卸载预加载的音频
- uncacheAll 卸载所有音频
- preload 预加载一个音频
- setMaxWebAudioSize 设置一个以 KB 为单位的尺寸，大于这个尺寸的音频在加载的时候会强制使用 dom 方式加载
- playMusic 播放背景音乐
- stopMusic 停止播放背景音乐
- pauseMusic 暂停播放背景音乐
- resumeMusic 恢复播放背景音乐
- getMusicVolume 获取音量（0.0 ~ 1.0）
- setMusicVolume 设置背景音乐音量（0.0 ~ 1.0）
- isMusicPlaying 背景音乐是否正在播放
- playEffect 播放音效
- setEffectsVolume 设置音效音量（0.0 ~ 1.0）
- getEffectsVolume 获取音效音量（0.0 ~ 1.0）
- pauseEffect 暂停播放音效
- pauseAllEffects 暂停播放所有音效
- resumeEffect 恢复播放音效音频
- resumeAllEffects 恢复播放所有之前暂停的音效
- stopEffect 停止播放音效
- stopAllEffects 停止播放所有音效
### 循环（类似for）
```
properties: {
    daojishi:12
},
start(){
    node.string = this.daojishi;//  场景文本框为 显示12
    if (this.daojishi >= 0) {
        this.schedule(this.DoSomething, 1);// 计时器将每隔 1s 执行一次。
    }
},
DoSomething: function () {// 倒计时算法
    if (this.daojishi >= 1) {
        this.daojishi = this.daojishi - 1;
        node.string = this.daojishi;    //场景中文本框显示
    }
    if (this.daojishi <= 0) {
        this.unschedule(this.DoSomething);//取消定时器
    }
}
```