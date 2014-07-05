jquery-compatibility
====================

jQuery兼容性研究

- 在Blackberry 4.6浏览器中通过`document.getElementById(id)`可能会获取到已经从文档中删除掉的元素，可以通过判断其是否含有parentNode来检测
- 在IE8及之前的浏览器中通过`docuemnt.getElementById(id)`可能会获取到name属性为该id值得元素，可以通过判断元素的id属性来检测
- 在IE8及之前浏览器中，通过innerHTML机制不能序列化标签`<link>`和`<script>`（即不能转换为对应的元素，此时`jQuery.support.htmlSerialize`为`false`），jQuery的解决方案是在这些标签的外层包裹`div<div> ... </div>`
