jquery-compatibility
====================

jQuery兼容性研究

- 在Blackberry 4.6浏览器中通过`document.getElementById(id)`可能会获取到已经从文档中删除掉的元素，可以通过判断其是否含有parentNode来检测
- 在IE8及之前的浏览器中通过`docuemnt.getElementById(id)`可能会获取到name属性为该id值得元素，可以通过判断元素的id属性来检测
