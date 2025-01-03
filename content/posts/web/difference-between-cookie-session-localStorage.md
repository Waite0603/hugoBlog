---
title: "cookie、session和localStorage的区别"
date: 2023-09-22T16:04:23+08:00
categories: ["Web"]
tags: ["Web", "Knowledge"]

showToc: true
TocOpen: true # 是否展开目录
disableHLJS: true # to disable highlightjs
weight:
draft: false
---

## 概念的理解

### webstorage本地存储

1. webstorage是本地存储，存储在客户端，包括localStorage和sessionStorage 
2.  localStorage生命周期是永久，这意味着除非用户显示在浏览器提供的UI上清除localStorage信息，否则这些信息将永远存在。存放数据大小为一般为5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信 
3. sessionStorage仅在当前会话下有效，关闭页面或浏览器后被清除。存放数据大小为一般为5MB,而且它仅在客户端（即浏览器）中保存，不参与和服务器的通信。源生接口可以接受，亦可再次封装来对Object和Array有更好的支持
4. WebStorage的目标 提供一种在cookie之外存储会话数据的路径 提供一种存储大量可以跨会话存在的数据的机制 HTML5的WebStorage提供了两种API：localStorage（本地存储）和sessionStorage（会话存储） 
5. 作用域的不同： 不同浏览器无法共享localStorage或sessionStorage中的信息。相同浏览器的不同页面间可以共享相同的 localStorage（页面属于相同域名和端口），但是不同页面或标签页间无法共享sessionStorage的信息。这里需要注意的是，页面及标 签页仅指顶级窗口，如果一个标签页包含多个iframe标签且他们属于同源页面，那么他们之间是可以共享sessionStorage的 
6. 存储大小： localStorage和sessionStorage的存储数据大小一般都是：5MB 
7. 存储位置： localStorage和sessionStorage都保存在客户端，不与服务器进行交互通信 
8. 存储内容类型： localStorage和sessionStorage只能存储字符串类型，对于复杂的对象可以使用ECMAScript提供的JSON对象的stringify和parse来处理 
9. 获取方式： localStorage：window.localStorage;；sessionStorage：window.sessionStorage; 
10.  应用场景： localStoragese：常用于长期登录（+判断用户是否已登录），适合长期保存在本地的数据，而sessionStorage：敏感账号一次性登录 
11. WebStorage的优点： 存储空间更大：cookie为4KB，而WebStorage是5MB 节省网络流量：WebStorage不会传送到服务器，存储在本地的数据可以直接获取，也不会像cookie一样美词请求都会传送到服务器，所以减少了客户端和服务器端的交互，节省了网络流量 对于那种只需要在用户浏览一组页面期间保存而关闭浏览器后就可以丢弃的数据，sessionStorage会非常方便 快速显示：有的数据存储在WebStorage上，再加上浏览器本身的缓存。获取数据时可以从本地获取会比从服务器端获取快得多，所以速度更快 安全性：WebStorage不会随着HTTP header发送到服务器端，所以安全性相对于cookie来说比较高一些，不会担心截获，但是仍然存在伪造问题 WebStorage提供了一些方法，数据操作比cookie方便 setItem (key, value) —— 保存数据，以键值对的方式储存信息。 getItem (key) —— 获取数据，将键值传入，即可获取到对应的value值。 removeItem (key) —— 删除单个数据，根据键值移除对应的信息。 clear () —— 删除所有的数据 key (index) —— 获取某个索引的key

### cookie

1. HTTP Cookie简称cookie,在HTTP请求发送Set-Cookie HTTP头作为响应的一部分。通过name=value的形式存储 
2. cookie的构成： 名称：name(不区分大小写,但最好认为它是区分的) 值:value(通过URL编码:encodeURIComponent) 域 路径 失效时间:一般默认是浏览器关闭失效,可以自己设置失效时间 安全标志:设置安全标志后只有SSL连接的时候才发送到服务器 
3. cookie的作用:主要用于保存登录信息 
4.  生命期为只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭。 存放数据大小为4K左右 。有个数限制（各浏览器不同），一般不能超过20个。与服务器端通信：每次都会携带在HTTP头中，如果使用cookie保存过多数据会带来性能问题 
5.  cookie的优点：具有极高的扩展性和可用性 通过良好的编程，控制保存在cookie中的session对象的大小 通过加密和安全传输技术，减少cookie被破解的可能性 只有在cookie中存放不敏感的数据，即使被盗取也不会有很大的损失 控制cookie的生命期，使之不会永远有效。这样的话偷盗者很可能拿到的就 是一个过期的cookie 
6. cookie的缺点： cookie的长度和数量的限制。每个domain最多只能有20条cookie，每个cookie长度不能超过4KB，否则会被截掉 安全性问题。如果cookie被人拦掉了，那个人就可以获取到所有session信息。加密的话也不起什么作用 有些状态不可能保存在客户端。例如，为了防止重复提交表单，我们需要在服务端保存一个计数器。若吧计数器保存在客户端，则起不到什么作用

### sessionStorage

1. sessionStorage是Storage类型的一个对象，拥有clear(),getItem(name),key(index),removeItem(name),setItem(name,value)方法
2. sessionStorage对象存储特定于某个会话的数据,也就是该数据只保持到浏览器关闭 
3. 将数据保存在session对象中。所谓session，是指用户在浏览某个网站时，从进入网站到浏览器关闭所经过的这段时间，也就是用户浏览这个网站所花费的时间。session对象可以用来保存在这段时间内所要求保存的任何数据 
4.  sessionStorage为临时保存

### localStorage

1. localStorage也是Storage类型的一个对象 
2.  在HTML5中localStorage作为持久保存在客户端数据的方案取代了globalStorage(globalStorage必须指定域名) 
3. localStorage会永久存储会话数据，除非removeItem,否则会话数据一直存在 
4. 将数据保存在客户端本地的硬件设备(通常指硬盘，也可以是其他硬件设备)中，即使浏览器被关闭了，该数据仍然存在，下次打开浏览器访问网站时仍然可以继续使用 5. localStorage为永久保存

## 区别的比较

### 本地储存localStorage与cookie的区别

1. cookie在浏览器与服务器之间来回传递 sessionStorage和localStorage不会把数据发给服务器，仅在本地保存 
2. 数据有效期不同 cookie只在设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭 sessionStorage：仅在当前浏览器窗口关闭前有效 localStorage 始终有效，长期保存
3. cookie数据还有路径的概念，可以限制cookie只属于某个路径下 存储大小也不同，cookie数据不能超过4k，sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大 
4.  作用域不用 sessionStorage不在不同的浏览器窗口中共享 localStorage在所有同源窗口中都是共享的 cookie也是在所有同源窗口中都是共享的 WebStorage 支持事件通知机制，可以将数据更新的通知发送给监听者。Web Storage 的 api 接口使用更方便

### cookie、session和localStorage的区别

1. cookie的内容主要包括：名字、值、过期时间、路径和域，路径与域一起构成cookie的作用范围。若不设置时间，则表示这个cookie的生命期为浏览器会话期间，关闭浏览器窗口，cookie就会消失，这种生命期为浏览器会话期的cookie被称为会话cookie 
2. 会话cookie一般不存储在硬盘而是保存在内存里，当然这个行为并不是规范规定的。若设置了过期时间，浏览器就会把cookie保存到硬盘上，关闭后再打开浏览器这些cookie仍然有效直到超过设定的过期时间。对于保存在内存里的cookie，不同的浏览器有不同的处理方式session机制。
3. 当程序需要为某个客户端的请求创建一个session时，服务器首先检查这个客户端的请求里是否已包含了一个session标识（称为session id），如果已包含则说明以前已经为此客户端创建过session，服务器就按照session id把这个session检索出来使用（检索不到，会新建一个），如果客户端请求不包含session id，则为客户端创建一个session并且生成一个与此session相关联的session id，session id的值应该是一个既不会重复，又不容易被找到规律以仿造的字符串，这个session id将被在本次响应中返回给客户端保存。保存这个session id的方式可以采用cookie，这样在交互过程中浏览器可以自动的按照规则把这个标识发送给服务器。

### cookie和session的区别

1. cookie数据存放在客户的浏览器上，session数据放在服务器上
2. cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session 
3. session会在一定时间内保存在服务器上，当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie 
4.  单个cookie保存的数*据不能超过4K，很多浏览器都限制一个站点最多保存20个cookie 
5. 建议将登录信息等重要信息存放为session，其他信息如果需要保留，可以放在cookie中 
6. session保存在服务器，客户端不知道其中的信心；cookie保存在客户端，服务器能够知道其中的信息 
7. session中保存的是对象，cookie中保存的是字符串 8. session不能区分路径，同一个用户在访问一个网站期间，所有的session在任何一个地方都可以访问到，而cookie中如果设置了路径参数，那么同一个网站中不同路径下的cookie互相是访问不到的

### web Storage和cookie的区别

1. Web Storage的概念和cookie相似，区别是它是为了更大容量存储设计的，cookie的大小是受限的，并且每次请求一个新的页面的时候cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可跨域调用 
2. web storage拥有setItem,getItem,removeItem,clear等方法，不像cookie需要前端开发者自己封装setCookie，getCookie 
3. 但是cookie也是不可或缺的，cookie的作用是与服务器进行交互，作为http规范的一部分而存在的，而web Storage仅仅是为了在本地“存储”数据而生 sessionStorage、localStorage、cookie都是在浏览器端存储的数据，其中sessionStorage的概念很特别，引入了一个“浏览器窗口”的概念，sessionStorage是在同源的同窗口中，始终存在的数据，也就是说只要这个浏览器窗口没有关闭，即使刷新页面或进入同源另一个页面，数据仍然存在，关闭窗口后，sessionStorage就会被销毁，同时“独立”打开的不同窗口，即使是同一页面，sessionStorage对象也是不同的 
4. Web Storage的好处 减少网络流量：一旦数据保存在本地之后，就可以避免再向服务器请求数据，因此减少不必要的数据请求，减少数据在浏览器和服务器间不必要的来回传递 快速显示数据：性能好，从本地读数据比通过网络从服务器上获得数据快得多，本地数据可以及时获得，再加上网页本身也可以有缓存，因此整个页面和数据都在本地的话，可以立即显示 临时存储：很多时候数据只需要在用户浏览一组页面期间使用，关闭窗口后数据就可以丢弃了，这种情况使用sessionStorage非常方便

### 浏览器本地存储与服务器端存储的区别

1. 数据既可以在浏览器本地存储，也可以在服务器端存储 
2. 浏览器可以保存一些数据，需要的时候直接从本地存取，sessionStorage、localStorage和cookie都是由浏览器存储在本地的数据 
3. 服务器端也可以保存所有用户的所有数据，但需要的时候浏览器要向服务器请求数据 
4.  服务器端可以保存用户的持久数据，如数据库和云存储将用户的大量数据保存在服务器端 ，服务器端也可以保存用户的临时会话数据，服务器端的session机制，如jsp的session对象，数据保存在服务器上
5. 服务器和浏览器之间仅需传递session id即可，服务器根据session id找到对应用户的session对象，会话数据仅在一段时间内有效，这个时间就是server端设置的session有效期 
6. 服务器端保存所有的用户的数据，所以服务器端的开销较大，而浏览器端保存则把不同用户需要的数据分别保存在用户各自的浏览器中，浏览器端一般只用来存储小数据，而非服务可以存储大数据或小数据服务器存储数据安全一些，浏览器只适合存储一般数据

### sessionStorage、localStorage和cookie的区别

1. 相同点是都是保存在浏览器端、且同源的 
2.  cookie数据始终在同源的http请求中携带（即使不需要），即cookie在浏览器和服务器间来回传递，而sessionStorage和localStorage不会自动把数据发送给服务器，仅在本地保存。cookie数据还有路径（path）的概念，可以限制cookie只属于某个路径下 
3. 存储大小限制也不同，cookie数据不能超过4K，同时因为每次http请求都会携带cookie、所以cookie只适合保存很小的数据，如会话标识。sessionStorage和localStorage虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大 
4.  数据有效期不同，sessionStorage：仅在当前浏览器窗口关闭之前有效；localStorage：始终有效，窗口或浏览器关闭也一直保存，因此用作持久数据；cookie：只在设置的cookie过期时间之前有效，即使窗口关闭或浏览器关闭 
5. 作用域不同，sessionStorage不在不同的浏览器窗口中共享，即使是同一个页面；localstorage在所有同源窗口中都是共享的；cookie也是在所有同源窗口中都是共享的 
6. web Storage支持事件通知机制，可以将数据更新的通知发送给监听者 
7. web Storage的api接口使用更方便

### sessionStorage与页面js数据对象的区别

1. 页面中一般的js对象的生存期仅在当前页面有效，因此刷新页面或转到另一页面这样的重新加载页面的情况，数据就不存在了 
2. sessionStorage只要同源的同窗口中，刷新页面或进入同源的不同页面，数据始终存在，也就是说只要浏览器不关闭，数据仍然存在
