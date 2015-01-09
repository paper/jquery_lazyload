## Changelog

### Version: 1.9.4 (by paper)

#####帮助文档（资料）：http://www.appelsiini.net/projects/lazyload

我和作者的讨论在这里：https://github.com/tuupola/jquery_lazyload/issues/237

	默认 failure_limit 为 0  
	也就是说，当elements循环时，一发现有图片在可视区域下面（假设其中一个叫A），  
	++counter 就会大于 0，return false; each 循环停止 。  
	这会导致有些图片虽然在可视区域，但DOM节点处在A下面，就不会加载了。  
	
	虽然可以设置 failure_limit 的数量，但是每个页面的需求不同，
	而且页面的高度可以随时变化，这个值是很难设置，所以意义不大

围绕的主要问题就是：虽然 `failure_limit` 可以提高性能，但其实并不实用。  
（请查看帮助文档： **When Images Are Not Sequential**）

作者在他的帮助文档的 **"How to Use?"** 这样说的：

	$(function() {
	    $("img.lazy").lazyload();
	});

	This causes all images of class lazy to be lazy loaded. See the basic options demo

但是看这个失败的例子：https://paper.github.io/lab/lazyload-test/faile/lazyload-test.html  
所以我觉得这虽然不能说是一个 "bug"，但体验真的不太好

作者也给出了解决方案：

	$("#left img").lazyload(...);
	$("#right img").lazyload(...);	

但当页面很多，页面的dom千变万化的时候，这个代码耦合太高，我们的公共代码只要关心 `img.lazy` 标签即可。

然后 作者又给出：

	$("img.lazy").lazyload({
	    failure_limit  :  99999999999
	});

是不是很囧~ Orz


**故修改后的版本就是：**   
`failure_limit` 默认不使用，如果你想使用，可以设置任何大于0的整数

