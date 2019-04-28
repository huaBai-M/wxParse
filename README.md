# wxParse
小程序转html格式的富文本
首先我们在github上下载wxParse
https://github.com/icindy/wxParse
下载完之后我们需要用到目录下的wxParse文件夹，把他拷贝到我们的项目目录下
下面是具体的使用步骤

1.在app.wxss全局样式文件中，需要引入wxParse的样式表

@import "/page/wxParse/wxParse.wxss";


2.在需要加载html内容的页面对应的js文件里引入wxParse

var WxParse = require('../../wxParse/wxParse.js');


3.通过调用WxParse.wxParse方法来设置html内容

/**
* WxParse.wxParse(bindName , type, data, target,imagePadding)
* 1.bindName绑定的数据名(必填)
* 2.type可以为html或者md(必填)
* 3.data为传入的具体数据(必填)
* 4.target为Page对象,一般为this(必填)
* 5.imagePadding为当图片自适应是左右的单一padding(默认为0,可选)
*/

Page({
  data: {
  },
  onLoad: function () {
    var that = this;
    wx.request({
        url: '', 
        method: 'POST',
        data: {
            'id':13
        },
        header: {
            'content-type': 'application/json'
        },
        success: function(res) {
            var article = res.data[0].post;
            WxParse.wxParse('article', 'html', article, that,5);
        }
    })
  }
})


4.在页面中引用模板

<import src="../../wxParse/wxParse.wxml"/>
<template is="wxParse" data="{{wxParseData:article.nodes}}"/>

这样就可以在微信小程序中嵌入html内容了

