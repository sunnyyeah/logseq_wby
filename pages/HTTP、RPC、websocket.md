- tags: #SSE #http #websocket
-
- ## SSE 请求的 client 和 server 之间的交互是怎样的？
- Server-Sent Events（SSE）的客户端和服务器之间的交互过程主要包括如下步骤：
	- 1. **发起请求**：首先，客户端发起一个 HTTP/HTTPS 请求到服务器。这通常是通过 JavaScript 的 `EventSource` API 来进行的。比如创建一个连接到 SSE 服务器的
	  `EventSource` 实例：
	- ```javascript
	  var source = new
	  EventSource("https://example.com/events")
	  ```
	- 通常，这个请求需要包含一个 `Accept: text/event-stream` 请求头，来告诉服务器客户端希望建立一个 SSE 连接。
-
	- 2. **建立连接**：如果服务器支持 SSE，那么它会处理这个请求，并保持连接打开状态而不是立刻关闭。服务器会返回一个 `Content-Type: text/event-stream` 的响应头，告诉客户端这是一个 SSE 连接。
-
	- 3. **发送消息**：当服务器有数据需要推送到客户端时，它会通过这个打开的连接发送一个或多个 SSE 数据包。每个数据包主要由一行或连续多行的文本组成,结尾有一个空行。
	- 例如，一个基础的 SSE 消息可能如下：
	- ```SSE
	  data: This is a message.
	  ```
	- 在发送多行数据时，可以将 "data:" 重复在每一行的前面：
	- ```SSE
	  data: first line
	  data: second line
	  data: third line
	  ```
	- 当一个数据包（可能包含一个或多个 "data:" 行）被发送出去时, 客户端的
	  "onmessage" 事件会被触发，可以从事件对象中读取这个数据包的信息。
-
	- 4. **监听消息**：客户端每接收到一个数据包，就会触发一个 JavaScript 事件。例如，你可以定义一个函数来处理 `message` 事件：
	- ```javascript
	  source.onmessage = function(event) {
	  	console.log(event.data);
	  }
	  ```
-
	- 5. **断线重连**：如果连接被中断，客户端会自动尝试重新连接到服务器。这个大概有3秒的固定延迟。开发者也可以通过在服务器的消息中带上 `retry:` 来自定义这个重连时间。
-
- 以上就是一个简化版的 SSE 连接过程。在实际应用中，还可能有其他因素需要考虑，比如错误处理、网络问题、授权验证、消息序列化反序列化以及连接存活时间等等。
-
- ## SSE 和 websocket 的区别是什么？
- 服务器发送事件(Server-Sent Events,
  SSE)和WebSockets都是拥有持久连接，并能够实现服务器向客户端主动发送信息的技术。但它们在某些方面有以下几个主要区别：
	- 1. **双向 vs 单向通信**：WebSockets
	  支持全双工通信，这意味着客户端和服务器都可以在任何时候向对方发送数据。相反，
	  SSE 是单向的，只允许服务器向客户端发送数据。
	- 2. **消息类型**：在 WebSockets
	  中，你可以发送任何类型的数据，文本或二进制都可以。SSE 仅支持发送 UTF-8 编码的文本数据。
	- 3. **连接类型**：SSE 在单个 HTTP 连接上重用了
	  HTTP 协议，每次通信的数据被视为一个新的 HTTP 请求的一部分。WebSockets 则不同，它握手的时候启动的是一个 HTTP
	  连接，一旦握手成功，便在相同的 TCP 连接上升级协议，转变为 WebSockets 协议进行通信。
	- 4.** **历史消息和重连处理****：SSE
	  支持自动重连（如果连接断开）、发送事件 ID 来同步和追踪消息。WebSockets 协议比较底层，这些行为需由开发人员自行实现。
	- id:: 656b5a06-a0f0-4a5e-86d2-9bc04a3edbc8
	  5. **传输层需求**：SSE 可以通过 HTTP
	  协议进行传输，与现有的网络协议兼容性较好，可以通过现有的 HTTP 或 HTTPS 端口（80 或 443 端口）进行传输，并且也可以利用现有的 HTTP
	  缓存机制。WebSockets 使用独特的、全双工通信的协议。
- 在选择适合的技术时，需要根据实际的应用需求来做决定。如果需要实现全双向的通信，那么 WebSockets
  可能是更好的选择。如果只需要服务器向客户端推送更新，而且浏览器兼容性（老旧浏览器可能无法支持 WebSockets）和网络环境（企业防火墙等可能限制了WebSockets 连接）是你关心的地方，那么 SSE 可能是更好的选择。
-
-