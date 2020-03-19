
### 复制功能
---
```
<input class="input" type="text" readonly="readonly" value=">
<button data-clipboard-action="copy" data-clipboard-target=".input"></button>
<script src="/static/js/clipboard.min.js"></script>
<script>
    let text='复制的内容',$('.input').val(text);
    $('button').on('click',function(){
        let clipboard=new ClipboardJS('button');
        clipboard.on('success',function(e){
        e.clearSelection();
    })
})
</script>
```
### 判断是安卓还是pc端
---
```
if (/Android|webOS|iPhone|iPod|BlackBerry/i.test(navigator.userAgent)) {
    // 移动端
}else{
    //pc端
}
```
### 获取地址栏参数
---
```
function GetUrlByParamName(name) {
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    var URL = decodeURI(window.location.search);
    var r = URL.substr(1).match(reg);
    if (r != null) {
        return decodeURI(r[2]);
    }
    return null;
}
//引用
GetUrlByParamName('id')
```
### 生成随机数(从minNum到maxNum)
```
function randomNum(minNum, maxNum) {
    switch (arguments.length) {
        case 1:
            return parseInt(Math.random() * minNum + 1, 10);
            break;
        case 2:
            return parseInt(Math.random() * (maxNum - minNum + 1) + minNum, 10);
            break;
        default:
            return 0;
            break;
    }
}
```
### 分割数组(按个数分割数组)
```
sliceArr: function (a, x) {
    var arr = [];
    for (var i = 0; i < a.length; i += x) {
        arr.push(a.slice(i, i + x))
    }
    return arr
},
```
* 使用方式
```
sliceArr([1,2,3,4,5,6,7,8,9],2)
```
* 结果
```
[[1,2],[3,4],[5,6],[7,8],[9]]
```
### vue代码模板闪现
---
```
<div v-cloak></div>
[v-cloak]{
    display:none
}
```
### vue select的默认值设置
---
```
https://blog.csdn.net/weixin_41056945/article/details/92382436
```
### vue 绑定多个class类名
---
```
https://www.cnblogs.com/zjh-study/p/10654941.html
```
### 计算顺子 豹子 对子 半顺 杂六
```
号码1：<input type="number" value="5" id="num1" /><br />
号码2：<input type="number" value="6" id="num2" /><br />
号码3：<input type="number" value="1" id="num3" /><br />
<button onclick="calc()">计算</button>
<span style="color:red;margin-left:50px;">计算结果：
    <b id="result" style="color:blue"></b>
</span>
<script>
    function calc() {
        var numberArray = new Array(3);
        for (var i = 0; i < 3; i++) {
            numberArray[i] = document.getElementById("num" + (i + 1)).value;
        }
        var resultArray = calcGamePlayResult(numberArray);
        var value = '';
        if (resultArray[0] == 1) {
            value = "对子";
        } else if (resultArray[0] == 2) {
            value = "豹子";
        } else if (resultArray[1] == 1) {
            value = "半顺";
        } else if (resultArray[1] == 2) {
            value = "顺子";
        } else {
            value = "杂六";
        }
        document.getElementById("result").innerHTML = value;
    }
    function calcGamePlayResult(array) {
        array = Arrays.toNumArray(array);
        array = Arrays.sortAsc(array);
        //存储计算结果
        var resultArray = new Array(2);
        //计算豹子、对子
        resultArray[0] = array[2] - array[1] == 0 ? 1 : 0;
        resultArray[0] = array[1] - array[0] == 0 ? ++resultArray[0] : resultArray[0];
        //计算顺子、半顺、杂六
        resultArray[1] = array[2] - array[1] == 1 ? 1 : 0;
        resultArray[1] = array[1] - array[0] == 1 ? ++resultArray[1] : resultArray[1];
        return resultArray;
    }
    Arrays.sortAsc = function (array) {
        for (var i = 0; i < array.length; i++) {
            for (var x = i; x < array.length; x++) {
                if (array[i] > array[x]) {
                    var temp = array[x];
                    array[x] = array[i];
                    array[i] = temp;
                }
            }
        }
        return array;
    }
    Arrays.toNumArray = function (strArray) {
        var numArray = new Array(strArray.length);
        for (var i = 0; i < strArray.length; i++) {
            numArray[i] = Number(strArray[i]);
        }
        return numArray;
    }
```