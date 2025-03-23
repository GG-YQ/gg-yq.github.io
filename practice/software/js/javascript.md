- js四种异步解决方案:回调函数、Promise、Generator、async/await
    - 场景1定时任务：setTimeout、setInterval; 
    - 场景2网络请求：[ajax异步请求](https://www.cnblogs.com/ryelqy/p/12201827.html)、基于promise的htttp客户端axios、动态创建img标签的加载; 
    - 场景3事件监听器：addEventListener。

typescript官网handbook，我还推荐typescript deep dive。里面讲到了一些typescript tricky的用法。

使用 Object.keys 然后获取它的属性，直接在 TypeScript 里这么做也会造成问题

学习 JavaScript 和 类型系统的区别。也要去学习如何能搜索的正确的写法。TypeScript 的语法，比如把函数的参数起好名字。用 objects 当作参数。

# 常见问题
## 获取变量名称
https://docs.pingcode.com/baike/2322310
> js没有直接的方法
- [x] 对象属性：将变量作为对象的属性存储。需要提前知道变量名称并将其存储在对象中，无法直接获取单个变量的名称。
    - `const variableName = Object.keys(obj)[0];`: Object.keys()方法可以返回一个由给定对象的自身可枚举属性组成的数组，但它不能直接作用于变量本身，而是作用于包含该变量的对象。
- [ ] 通过函数参数获取变量名称：通过传递变量作为函数参数，并在函数内部解析参数名称，获取到的名称是函数参数的名称，而不是变量的真实名称。
- [ ] 使用Proxy对象：Proxy对象是ES6中引入的一种新特性，可以拦截和自定义对象的基本操作。通过Proxy对象，可以实现对对象属性的动态管理，并获取变量名称。
- [ ] 使用反射（Reflect）：Reflect是ES6中引入的一个内置对象，提供了一些拦截JavaScript操作的方法。通过Reflect对象，可以实现对对象属性的反射操作，并获取变量名称。
- [ ] 解析代码字符串
- [x] 专门的项目管理系统：研发项目管理系统PingCode、通用项目协作软件Worktile