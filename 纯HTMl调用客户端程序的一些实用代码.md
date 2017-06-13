---
title: 纯HTML调用客户端程序的一些实用代码
date: 2017-05-10 16:09:38
tags: 奇淫巧计
---

> 这绝对是值得收藏的纯干货，已加入和将要加入收藏的有QQ聊天，添加QQ好友，加入QQ群，添加微信好友，加入微信群聊，发送邮件，Skype聊天，MSN聊天，MSN添加好友，旺信聊天，百度地图接口，Google地图接口。本页面不提供测试访问，测试某接口的话请确保客户端安装有相应的应用程序。

> 比如说，我想用电脑试试旺信聊天接口代码能否调用。那么我要在电脑上安装阿里旺旺软件，然后将接口调用代码写在HTML文件中，保存再用浏览器打开，点击链接唤醒旺旺软件。默认聊天对象均为博主本人。下面是一些简短的常用代码：

<!-- more -->

```
点击QQ聊天
<a href="tencent://message/?uin=310932019&amp;Site=QQ&amp;Menu=yes" >点击QQ聊天</a>

企业QQ聊天
<a href="http://wpa.qq.com/msgrd?V=1&Uin=310932019&Site=&Menu=yes" target="_blank">咨询QQ：310932019</a>

QQ聊天样式
<img src="http://wpa.qq.com/pa?p=1:21755061:1" border="0" />
<img src="http://wpa.qq.com/pa?p=1:21755061:2" border="0" />
<img src="http://wpa.qq.com/pa?p=1:21755061:3" border="0" />
<img src="http://wpa.qq.com/pa?p=1:21755061:4" border="0" />
<img src="http://wpa.qq.com/pa?p=1:21755061:5" border="0" />

点击进行MSN聊天
<a href="msnim:chat?contact=jinshangdi310@163.com" >点这里MSN聊天</a>

点击链接发送邮件
<a href="mailto:jinshangdi310@163.com?subject=测试主题&body=你好，一个HTML测试。">Email to: jinshangdi310@163.com</a>

<a href="msnim:add?contact=jinshangdi310@163.com">加我为好友MSN</a>

阿里旺旺加好友
<a href="wangwang:SendIM?晋殇帝&uid_t=abcde&suid=******&desc=123456">加我为好友旺旺</a>
<!-- abcde请改为对方的账号，******请改为自己账号，123456是商品名称  -->

点击加好友Skype
<a href="callto://abcde ">点击加好友Skype</a>

Paypay付款
<a href="https://www.paypal.me/erchoc">Paypay付款</a>
```

- 百度地图API(含密钥)：

```
- 头部head引入百度地图API：
<script src="http://api.map.baidu.com/api?v=2.0&ak=e4HVYXyDIAkqODAN7ZREFsRBx8roV2Hj"></script>
- 身体body创建百度地图容器：
<div style="width:700px;height:550px;border:#ccc solid 1px;font-size:12px" id="map"></div>
- js脚本创建动态交互效果：
<script type="text/javascript">
  //创建和初始化地图函数：
  function initMap(){
    createMap();//创建地图
    setMapEvent();//设置地图事件
    addMapControl();//向地图添加控件
    addMapOverlay();//向地图添加覆盖物
  }
  function createMap(){
    map = new BMap.Map("map");
    map.centerAndZoom(new BMap.Point(116.038355,28.686546),15);
  }
  function setMapEvent(){
    map.enableScrollWheelZoom();
    map.enableKeyboard();
    map.enableDragging();
    map.enableDoubleClickZoom()
  }
  function addClickHandler(target,window){
    target.addEventListener("click",function(){
      target.openInfoWindow(window);
    });
  }
  function addMapOverlay(){
    var markers = [
      {content:"电话：6800780<br/>备注：欢迎莅临我校参观指导",title:"江西师范大学",imageOffset: {width:-46,height:-21},position:{lat:28.687116,lng:116.036415}}
    ];
    for(var index = 0; index < markers.length; index++ ){
      var point = new BMap.Point(markers[index].position.lng,markers[index].position.lat);
      var marker = new BMap.Marker(point,{icon:new BMap.Icon("http://api.map.baidu.com/lbsapi/createmap/images/icon.png",new BMap.Size(20,25),{
        imageOffset: new BMap.Size(markers[index].imageOffset.width,markers[index].imageOffset.height)
      })});
      var label = new BMap.Label(markers[index].title,{offset: new BMap.Size(25,5)});
      var opts = {
        width: 200,
        title: markers[index].title,
        enableMessage: false
      };
      var infoWindow = new BMap.InfoWindow(markers[index].content,opts);
      marker.setLabel(label);
      addClickHandler(marker,infoWindow);
      map.addOverlay(marker);
    };
  }
  //向地图添加控件
  function addMapControl(){
    var scaleControl = new BMap.ScaleControl({anchor:BMAP_ANCHOR_BOTTOM_LEFT});
    scaleControl.setUnit(BMAP_UNIT_METRIC);
    map.addControl(scaleControl);
    var navControl = new BMap.NavigationControl({anchor:BMAP_ANCHOR_BOTTOM_RIGHT,type:2});
    map.addControl(navControl);
  }
  var map;
    initMap();
</script>
```