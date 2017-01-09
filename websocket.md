首先实例化WS对象：
```
var socket = new WebSocket('ws://echo.websocket.org/');
```
这里的参数必须是ws://或者wss://协议开头的绝对地址
当实例化结束后浏览器就会马上尝试创建连接，WS对象和XHR对象类似也有一个表示当前状态的readyState属性，不过含义有所不同：

```
0:正在建立连接。
1:已经建立连接。
2:正在关闭连接。
3:已经关闭连接。
```
如果想要关闭WS连接可以在任何时候调用close()方法:

```
socket.close();
```
当WS打开之后就可以通过连接发送以及接受数据了，要向服务器发送数据，使用send()方法并传入任意字符串
```
socket.send('HELLO WORLD!')
```
对于复杂的数据文本建议JSON.stringify后再发送。

当服务器返回消息的时候，WS对象就会触发message事件，类似于XHR对象的rponseText，返回的消息存放在event参数的data里。

```
socket.onmessage = function(event) {
	var data = event.data;
	// TODO
}
```
其他事件与注意事项：
```
- open: 在成功建立连接时触发。
- error: 在发生错误时候触发，连接不能持续。
- close: 在连接关闭时触发。
```
WS对象只能使用DOM0语法分别定义每个事件的处理程序：
 ```
 socket.onopen = function(){
 	//TODO
 }
 
 socket.onerror = function(){
 	//TODO
 }
 
 socket.onclose = function(){
 	//TODO
 }
```
在上述事件中只有close事件的event对象有额外信息:wasClean,code,reason.
wasClean:布尔类型，表示是否已经明确的关闭。
code:服务器返回的状态吗。
reason:字符串，包含服务器发回的消息，可以添加到日志中用以分析。
