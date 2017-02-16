>embedSWF: function(swfUrlStr, replaceElemIdStr, widthStr, heightStr, swfVersionStr, xiSwfUrlStr, flashvarsObj, parObj, attObj, callbackFn)

swfUrlStr：（String，必须的）flash地址url,

replaceElemIdStr,：（String，必须的）替换元素的id

widthStr：（String，必须的）flash宽度，类型为字符串

heightStr：（String，必须的）flash高度

swfVersionStr：（String，必须的）指定你发布的SWF对应的Flash Player版本（格式为：major.minor.release）

xiSwfUrlStr：（String，可选的）指定express install SWF的URL并激活Adobe express install

flashvarsObj：（Object，可选的）用name:value对指定你的flashvars

parObj：（Object，可选的）用name:value对指定你的嵌套object元素的params

attObj：（Object，可选的）用name:value对指定object的属性

callbackFn：（Function，可选的）flash加载完成的回调函数，2.2才支持。

callbackFn参数：{success:true/false,id:"object id",ref:DOM Element}

success, Boolean to indicate whether the embedding of a SWF was success or not
id, String indicating the ID used in swfobject.registerObject
ref, HTML object element reference (returns undefined when success=false)

>function load(){
  var swfVersionStr = "10.0.0";
  var params = {};
  params.quality = "high";  
  params.allowfullscreen = "false";
  params.allowscriptaccess = "always"; 
  //params.wmode = "transparent";
  swfobject.embedSWF("flash/MainPage.swf", "FlashID", "597", "416", swfVersionStr,params);
 }
 //调用flash中的方法，"swfId"为html页中swf的id
 function setValue(o) {
   
  thisMovie("FlashID").getIds(o);
 }
  
 //搭建js与flash互通的环境
 function thisMovie(movieName) {
  if (navigator.appName.indexOf("Microsoft") != -1) {
    
   return window[movieName];
  } else {
    
   return document[movieName];
  }
 }

以上为引用
