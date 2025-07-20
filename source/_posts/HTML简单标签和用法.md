---
title: HTML简单标签和用法
date: 2022-01-12 13:08:58
tags:
---

HTML的英文全称是Hyper Text Markup Language,即超文本标记语言,包括一系列标签。通过这些标签可将网络上的文档格式统一下，连城一个逻辑整体。

# 简单HTML标签用法

### Welcom to learn

Study :  [MDN](https://developer.mozilla.org/zh-CN/)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>标题</title>
    <link rel="icon" href="images/icon.png">//换网页的图标
</head>


<!-- 标题标签，标题大小一级比一级大小-->
    <h1>一级标签</h1>
    <h2>二级标签</h2>
    <h3>三级标签</h3>
    <h4>四级标签</h4>
    <h5>五级标签</h5>
    <h6>六级标签</h6>


<!-- <br>  代表换行，<hr>  代表分割线 -->
     1.自己 <br>
     <hr>
     2.内心  <br>


<!-- 修改字体样式、格式、颜色、大小等标签 -->
    <font size="7px" color="blue" face="宋体">宁夏理工学院</font>
    <br>
    <b>加粗</b>&nbsp;&nbsp;
    <u>下划线字体标记</u>
    <br>
    <ins>下划线</ins>
    <br>
    <i>斜字体</i>&nbsp;&nbsp;
    2(文字下标) <sub>3</sub>&nbsp;&nbsp;
    2(文字上标) <sup>3</sup>
    <br>
    <del>删除标签</del>
    <br>
    

<!-- 段落标签 -->
    <p>祝：好兄弟</p> 
    <p>愿你在我看不到的</p>
    <p> 地方继续发胖</p> 
    <p>愿你的冬天</p>  
    <p>永远不缺狗粮</p>  
    <p>愿你的身材 </p> 
    <p>明天依旧乘风破浪</p>  
    <p>愿你的未来</p>  
    <p>依旧找不到对象</p> 
    
    <pre>
            #include &lt;iostream&gt;
        
            using namespace std;

            int main()
            {
                cout &lt;&lt; hello world! &lt;&lt; endl;

                return 0;
            }
    </pre>
    

 <!-- 添加图片,并设置图片长宽高 -->
   <img src="星空.jpg" alt="pic" title="悬停文字" width="20%" height="20%">
   <br>
 <!-- 绝对路径可移植性差 -->
   <img src="D:\作业\数据库上机课\图片" alt="找不到">
   <br>
<!--图像标签-->
<!--
src:图片地址
    相对地址(推荐)    绝对地址（盘符目录）
    ../   代表上一级目录
alt:图片加载失败返回值
title：鼠标悬停的时候显示的
-->

<!-- 音频和视频 
controls；播放选择（进度条）
autoplay:自动播放 -->
<video src="与图片链接相同" controls autoplay></video>
<br>
<audio src="同上" controls autoplay></audio>
<br>


<!-- 特殊符号 -->
    宁夏&nbsp;&nbsp;理工&nbsp;&nbsp;&nbsp;学院 
    <br>
           <!-- 有几个&nbsp;就有几个空格 -->
    &copy;版权归属JHJ
    <br>
    <img src="特殊字符.png" alt="pic" title="特殊符号" width="40%" height="40%"> 
    <br>


<!-- 超链接，target是跳转到新打开的页面 -->
    <a href="http://wwww.baidu.com" target="_blank">点击跳到另一网页</a>
    <br>
    <a href="http://wwww.baidu.com"> 
        <img src="夕阳.jpg" alt="pic" title="嵌套图片地址，使图片可以跳转链接" width="10%" height="5%">
          <!-- 图片做超链接 -->
    </a>
    <br>


<!-- 下载链接：地址链接的文件 .exe或者zip灯压缩报形式 -->
    <a href="#.zip">下载文件</a>


<!-- 锚链接 -->
<!-- 1.先有一个锚标记
2.跳转到锚标记 -->
    <p>
        <a href="#top"> 回到顶部</a>
    </p>
        <!-- <a href="#dibu">到页面底部</a>
        <a name="dibu"></a> -->
    <br>


<!-- 功能性链接 
邮箱链接：mailto: -->
    <a href="mailto:524134609@qq.com">QQ邮箱</a>


<!-- 有序列表标签，可加 type 属性、新的起始数值 value -->
<ol type="A">
    <li>宁夏</li>
    <li>理工</li>
    <li>学院</li>
    <li>计算机</li>
</ol>


<!-- 无序列表 -->
<ul>
    <li>计科</li>
    <li>网工</li>
    <li>大数据</li>
</ul>
    <br>


<!-- 制作表格 -->
    <table width="500px" height="230px" border="1px" align="content" cellspacing="0px">
        <caption>成绩表</caption>
        <tr>
            <th align="content">班级</th>
            <th>姓名</th>
            <th>年龄</th>
            <th>成绩</th>
        </tr>
        <tr align="content" valign="content">
            <td>计类2班</td>
            <td>小五</td>
            <td>19</td>
            <td>80</td>
        </tr>
        <tr align="content" valign="content">
            <td>计类2班</td>
            <td>小航</td>
            <td>19</td>
            <td>93</td>
        </tr>
    </table>


<!-- 自定义列表，dl:标签，dt:列表标题，dd:列表名称 -->
<dl>
    <dt>软件说明：</dt>
    <dd>简单介绍软件新功能及应用</dd>
    <dt>软件界面</dt>
    <dd>用于选择软件外观</dd>
</dl>


<!-- 分区显示标签（盒子） -->
<div>
    <div>宁夏理工学院</div>
    <div>计算机科学与工程学院</div>
</div>
    <br>


<!-- 提交、重置、普通按钮 -->
    <form method="POST">
        账号：<input type="text" name="zhanghao" size="10" maxlength="10">
        <br>
        <br>
        密码：<input type="password" name="mima" size="10">
        <br>
        <br>
        <input type="submit" value="提交">
        <input type="reset" value="重置">
    </form>
        <br>
    <form>
        
        -----------------------------------------------------
        <form action="/Web/TREES/christmas.html">
        <!-- action 有向服务器交互的过程 -->
        <label for="username">用户名</label>
        <input type="text" minlength="3" name="username" id="username">

        <br>
        <label for="password"> 密码</label>
        <input required type="password" maxlength="10" name="password" id="password">
        <!-- required 加在哪里 ，哪里必须填写 -->


        <br>
        <label for="email">邮箱</label>
        <input type="email" name="email" id="email">

        <br>
        <label for="cpp"> cpp</label>
        <input type="radio" name="lang" id="cpp">

        <br>
        <label for="java"> java</label>
        <input type="radio" name="lang" id="java">
        
        <br>
        <label for="c#">c#</label>
        <input type="radio" name="lang" id="c#">
        <br>
        <button>提交</button>
    </form>
        -----------------------------------------------------
 <!-- 单选按钮 -->
        性别:
        <input id="man" type="radio" name="sex" checked="checked">男
        <input id="woman" type="radio" name="sex">女
    </form>
        <br>
<!-- 多行文本域 -->
    <form>
        自我介绍：<br>
        <textarea name="ziwojieshao" cols="30" rows="5">
        </textarea>
    </form>
<!-- 菜单下拉列表域 -->
    <form>
        <label for="jiguan">籍贯</label>
        <select name="jiguan">
            <!-- selected  默认 
            <option selected value="henan">河南</option> -->
            <option value="henan">河南</option>
            <option value="jiangsu">江苏</option>
            <option value="ningxia">宁夏</option>
        </select>
    </form>


<!-- 邮箱验证 -->
    <p>邮箱
        <input type="email" name="email">
    </p>


<!-- 长方形输入框url -->
    <p>url
        <input type="url" name="url">
    </p>


<!-- 数字 -->
    <p>
        <input type="number" name="number" max="100" min="10">
    </p>


<!-- 滑块 -->
    <p>音量
        <input type="range" name="email">
    </p>

    <h3 class="name">我好累啊！</h3>

</body>
</html>
```

