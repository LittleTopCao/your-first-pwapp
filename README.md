# Your first Progressive Web App Code Lab

These are the resource files needed for the [Your first Progressive Web App](https://codelabs.developers.google.com/codelabs/your-first-pwapp/)
code lab from Google.

This is a work in progress, if you find a mistake, please [file an issue](https://github.com/googlecodelabs/your-first-pwapp/issues). Thanks!

## What you’ll learn
* How to design and construct an app using the “app shell” method
* How to make your app work offline
* How to store data for use offline later

## What you’ll need
* Chrome 52 or above, though any browser that supports service workers and `cache.addAll()` will work
* [Web Server for Chrome](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb), or use your own web server of choice.
* The [sample code](https://github.com/googlecodelabs/your-first-pwapp/archive/master.zip)
* A text editor
* Basic knowledge of HTML, CSS and JavaScript
* (Optional) Node is required in the last step to deploy to Firebase


## App Shell
    就是类似 Android App 的代码，App Shell 架构将核心应用程序基础架构和 UI 与 数据 分开。通过缓存 App Shell 来提升启动速度。
    就是把 应用的代码 下载到本地了，还提供更新机制，然后可以分布加载，启动时 第二个页面 的 UI 可以稍后加载，但是也会提供缓存。
    我的理解 这就是 渐进式 的来源，慢慢下载，用到哪个 页面 下载那个页面。
    总结: App Shell 就是应用代码，需要缓存。一部分 立即加载，另一部分 可以延迟加载。

## LocalStorage
    LocalStorage 是一个同步 API，用来存储字符串键值对，性能问题，不应该用于生产服务器。应该选择 IDB 或 SimpleDb。

## WebWorker
    web多线程支持，html5 引入，以前都是单线程操作 UI。

## ServiceWorker
    长期运行线程，并能拦截浏览器请求。还有一些其他关于硬件 API 可以调用。
    我们要判断是否支持 serviceWorker，在不支持 serviceWorker 的时候可以和普通 web 页面一样。

    生命周期，install active 

## CacheStorage
    就是缓存用的，和 serviceWorker 标准的一部分
    caches 是一个全局的 CacheStorage 实例
    caches.open(cacheName)  返回一个 Promise 对象，then 拿到一个 Cache 实例

## Promise
    承诺，在 javascript 中表示异步的代码，这段代码我承诺执行。EC6 引入
    new Promise(function(resolve, reject){

    }).then(function(){

    }).catch(function(){

    });
    其中 then 方法的函数参数会传递给 resolve 作为实参
    catch 方法的函数参数会传递给 reject 作为实参
    这个传来传去 好复杂，没弄清什么时候执行，
    我的理解是 你这个 Promise 包装了一些代码，这些代码的最终目的是获得一个异步执行的结果，在框架中这个代码封装好了，但是这个结果最终怎么用 要你自己决定，所以留了一个接口 然你通过函数 传递 代码过去 来应用这个结果。

## manifest.json
    添加这个文件才表明你是一个 Application。才可以实现 图标 全屏 控制方向 
    