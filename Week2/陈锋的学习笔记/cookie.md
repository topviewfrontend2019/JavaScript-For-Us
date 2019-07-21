## cookie的概念
- cookie 是客户端与服务器端进行通讯使用的一个能够在浏览器本地化存储的技术

- PS：chrome不支持本地文件的cookie读写

## cookie的应用场景
- 七天免登陆
- 7天内访问网站无需输入密码
- 购物车信息
- 添加到购物车后，取到购物车页面，商品信息依然存在
- 商品浏览记录
- 用户每浏览一个商品就会保留商品的浏览记录
## cookie的组成
### cookie由键值对形式的文本组成，完整格式如下：
```
document.cookie = name=value[;expires=date][;path=路径][;domain=域名]
//[]表示该值是可选，代表传入这个cookie的参数，获取cookie是并不会得到（path默认值是当前文件所在的路径）
```
- name=value: 为你要保存的键值对(必选)
    - 利用decodeURI解码中文字符
    - 利用json保存多条信息
- expires=date: 表示cookie的失效时间, 默认是浏览器关闭时失效(可选)
```
//设置7天内生效的cookie
var date = new Date();  
date.setDate(date.getDate() +7); 
document.cookie = "user=laoxie;expires=" + date.toUTCString();
```
- path=路径: 访问路径, 默认为当前文件所在目录(可选)
  - cookie只能在设置的路径及它的子目录下使用(默认下获取cookie，返回的是当前网页及以上目录中能访问的所有cookie，为了使所有页面都能访问到所有cookie可以使用path =/，斜杠代表cookie存在根目录)

- domain=域名: 访问域名, 限制在该域名下访问(可选)
    - 没有设置则默认为当前域名

## cookie的操作
### cookie的获取和设置
```
//设置
document.cookie = 'name=laoxie';

//获取
var cookies = document.cookie;
```
- 一次只能写入一个cookie
- 获取时得到所有cookie，多个cookie之间用分号+空格（’; ‘）来隔开
### cookie的删除
- 利用设置过期时间达到删除的效果。
