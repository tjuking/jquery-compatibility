jquery-compatibility
====================

jQuery兼容性研究

- 在Blackberry 4.6浏览器中通过`document.getElementById(id)`可能会获取到已经从文档中删除掉的元素，可以通过判断其是否含有parentNode来检测
- 在IE8-浏览器中通过`docuemnt.getElementById(id)`可能会获取到name属性为该id值得元素，可以通过判断元素的id属性来检测
- 在IE8-浏览器中，通过innerHTML机制不能序列化标签`<link>`和`<script>`（即不能转换为对应的元素，此时`jQuery.support.htmlSerialize`为`false`），jQuery的解决方案是在这些标签的外层包裹`div<div> ... </div>`
- 在IE7-浏览器中通过innerHTML机制，写入空白`<table>`时，会自动生成`<tbody>`元素（需要剔除，此时的`jQuery.support.tbody`为`false`）
- 在IE8-浏览器中通过innerHTML机制，会自动剔除前导空白符（需要通过`createTextNode()`补全，此时的`jQuery.support.leadingWhitespace`为`false`）
- 在IE7-浏览器中通过innerHTML机制将复选框和单选框按钮插入DOM树后，其选中状态checked会丢失（通过赋值`defaultChecked`解决，此时的`jQuery.support.appendChecked`为`false`）
- 在IE8-浏览器中通过`Object.prototype.toString(xxx)`应用到操作DOM的方法或者类似于`alert`这样的方法，将得到`[object Object]`而非`[object Function]`
- 在IE9-浏览器中访问某些浏览器宿主对象例如location的`location.constructor.prototype`会抛出异常，需要`try/catch`
- 在IE7-浏览器中使用`(new Function("return " + data))()`将字符串转换JSON，如果未移除传入字符串开头和结尾的空白符就无法正确的解析
- 在IE8-浏览器中不支持ECMAScript5中指定的JSON对象及其方法
- 在IE8-浏览器中不支持`window.DOMParser`对象解析，可以使用`ActiveXObject`对象来解析XML
- 要想在全局作用域下执行字符串脚本，必须（为了兼容IE、Chrome和Firefox详情可参考[https://weblogs.java.net/blog/driscoll/archive/2009/09/08/eval-javascript-global-context](https://weblogs.java.net/blog/driscoll/archive/2009/09/08/eval-javascript-global-context)，对于Chrome的那个修正现在应该是不需要了）：`(window.execScript || function(data){window["eval"].call(window, data);})(data);`
- 在IE浏览器中连字符样式属性名例如`-ms-transform`对应的style属性是`msTransform`而通常其他浏览器中都是连字符后首字母大写，例如`MozTransform`（在`.camelCase(string)`方法中需要特殊处理一下）
- 在IE8-浏览器中，`\s`不匹配不间断空格`\xA0`（non-breaking space，还需要处理`\uFEFF`--Byte Order Mark），需要为`.trim(str)`方法里的正则特殊处理一下
- 在Blackberry4.7中，正则对象也有length属性
