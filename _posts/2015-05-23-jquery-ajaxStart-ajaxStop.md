---
layout: post
category: "javascript"
title: "ajaxStart和ajaxStop在1.8+的jquery版本中不执行"
tags: ["javascript","jquery"]
---
今天看到一个网友提问的问题,ajaxStart和ajaxStop不执行

```javascript
$(function(){
    $("#btn").click(function(){
        var $content=$("#div1").html()+$("#message").val();
        if($content!=""){
            $.ajax({
                url:"",
                data:$content,
                success:function(data){
                    $("#div1").html($content);
                    $("#message").val("");
                }
            })
        }
        $("#div3").ajaxStart(function(){
            $(this).show().html("留言发送中..");
        })
        $("#div3").ajaxStop(function(){
            $(this).show().html("留言成功!");
        })
    })    
})
```

看了半天没发现问题, 后来google了一会才发现有很多出现这个问题的, 原来时在jquery的1.8+版本中，它的使用对象更改为固定的`document`对象，不可以使用其他的操作对象，原来如此！