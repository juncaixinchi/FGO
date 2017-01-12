# FGO

自己写的一个自定FGO英灵的小程序(￣▽￣)~[]

作为学习HTML5的联系作品

链接：https://juncaixinchi.github.io/FGO/fgo.html


#Notes
1、主要利用HTML5的Canvas制作，通过content.drawImage()组合图片，但遇到了图片消失的情况，解决方案是利用onload，然后把其他的画图放入function内，不过似乎因为内部有多个content.drawImage()，所以可能还是会有刷不出图片的情况\~\~(>_<)\~\~
```html
img.onload = function()
  {
  content.drawImage();
  ......
  }
```

2、需要将生成的图片在手机保存，即保存canvas内容，考虑转化为图片，由于画布内有图片，导致
```
Tainted canvases may not be exported
```
而不能直接使用toDataURL()，后利用修改CROS解决
```html
img_bg.crossOrigin = '';
```

不过重要的一点是，这个需要服务器的配合，否则比如直接打开该html的话会如下报错
```
Access to Image at 'file:///D:/Juncaixinchi/img/fgo/fgo_bg.png' from origin 'null' has been blocked by CORS policy: Invalid response. Origin 'null' is therefore not allowed access.
```
最后利用canvas.toDataURL()获得canvas的url然后赋予显示的图片
```html
dataURL=canvas.toDataURL();
document.getElementById('pic_show').src = dataURL;
```
