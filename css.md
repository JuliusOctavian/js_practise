工作中很多时候需要对图片背景作处理,比如设置通透性，模糊处理等等![Screenshot from 2020-06-21 23-46-14.png](/img/bVbIC2t)
但是如果对背景图所在标签直接设置这些效果的话，这些样式会被子标签继承。![Screenshot from 2020-06-21 23-51-20.png](/img/bVbIC2X)
*例1: 给背景所在标签设置模糊效果，影响到了子标签内的文字*
```
    <style>
		.parent{
            background: url('./test.jpg') no-repeat center;
			filter: blur(3px)
		}
		.son{
			filter: blur(0);
            /*
            在子标签内设置相同属性也无法覆盖继承来的样式
            */
		}
	</style>

	<div class="parent">
		<p class="son">Hello</p>
	</div>
```
**解决方法：**
为父标签中添加一个标签，令其绝对定位并铺满父标签，将背景 / 样式设置在该标签内。
```
    <style>
		.parent{
			position: relative;
            /*让父标签相对定位，使.middle相对自己定位*/
		}
		.middle{
			background: url('./test.jpg') no-repeat center;
			filter: blur(3px);

			position: absolute;
			height: 100%;
			width: 100%;
			
			z-index: -1;
            /*降低图层高度，防止遮盖其他子元素*/
		}
		.son{
		}
	</style>
    
	<div class="parent">
		<div class="middle"></div>
		<p class="son">Hello</p>
	</div>
```
![Screenshot from 2020-06-22 00-16-15.png](/img/bVbIC5o)
