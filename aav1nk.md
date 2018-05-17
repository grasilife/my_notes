# gzip压缩前端文件

__react项目中利用dva脚手架，roadhog打包工具打包后只生成了一个index.css 和 index.js 。所有的 js文件 都打包在了一个 index.js 文件中，所以这个文件有可能会很大。部署到服务器上，首次访问首页加载的会特别慢，这样会流失很多的用户。__
## <a name="9fy3oo"></a>解决办法:gzip
ZIP编码是一种用来改进WEB应用程序性能的技术。大流量的WEB站点常常使用GZIP压缩技术来让用户感受更快的速度。这一般是指WWW服务器中安装的一个功能，当有人来访问这个服务器中的网站时，服务器中的这个功能就将网页内容压缩后传输到来访的电脑浏览器中显示出来.一般对纯文本内容可压缩到原大小的40%.这样传输就快了，效果就是你点击网址后会很快的显示出来.当然这也会增加服务器的负载. 一般服务器中都安装有这个功能模块的。

gzip可以极大的加速网站.有时压缩比率高达80%，近来测试了一下，最少都有40%以上，还是相当不错的.在Apache2之后的版本，模块名不叫gzip，而叫mod\_deflate。
## <a name="yuuhgk"></a>nginx开启gzip
<span data-type="color" style="color:rgb(79, 79, 79)"><span data-type="background" style="background-color:rgb(255, 255, 255)">在 nginx.conf 中添加以下配置：</span></span>
```bash
gzip on;
gzip_buffers 32 4k;
gzip_comp_level 6;
gzip_min_length 200;
gzip_types text/css text/xml application/javascript;
gzip_vary on;
```
<span data-type="color" style="color:rgb(79, 79, 79)"><span data-type="background" style="background-color:rgb(255, 255, 255)">重启 nginx：</span></span>
```bash
/usr/local/nginx/sbin/nginx -s reload
```
<span data-type="color" style="color:rgb(79, 79, 79)"><span data-type="background" style="background-color:rgb(255, 255, 255)">清除浏览器缓存，重新访问网页，可以发现首次加载速度快了很多。</span></span>

## <a name="d50txg"></a>查看是否开启了gzip
### <a name="r8dbqf"></a>开启gzip的显示如下
#### <a name="g3nrqp"></a>1.firefox


![image.png | left | 827x197](https://cdn.yuque.com/yuque/0/2018/png/111166/1526525181983-1152543e-8eee-40c9-ac1f-991960bb568c.png "")

在调试器中可以看到传输和大小两个值不一样,且在响应头中出现,Content-Encoding: gzip(是在响应头不是请求头)
请求头显示如下


![image.png | left | 551x218](https://cdn.yuque.com/yuque/0/2018/png/111166/1526525315812-3ce33a4e-ed07-456f-ae3c-c66493854ddb.png "")

#### <a name="m3v2ct"></a>2.chrome


![image.png | left | 827x288](https://cdn.yuque.com/yuque/0/2018/png/111166/1526525437530-366c38b4-0b06-4962-93fd-ea99194b83c2.png "")

### <a name="bvddvy"></a>没有开启gzip的显示如下
#### <a name="25s1lg"></a>1.firefox


![image.png | left | 827x208](https://cdn.yuque.com/yuque/0/2018/png/111166/1526525568670-d112729b-6054-4437-bf84-1b96f777fa2b.png "")

响应头中没有Content-Encoding: gzip
请求头如下


![image.png | left | 544x301](https://cdn.yuque.com/yuque/0/2018/png/111166/1526525627472-fde4e401-555e-47c0-ab7a-c260ce8faefe.png "")

在未压缩的情况下,请求头还是存在Content-Encoding: gzip,deflate
#### <a name="4i8trc"></a>2.chrome


![image.png | left | 827x312](https://cdn.yuque.com/yuque/0/2018/png/111166/1526525743246-bc66f3a6-d2e8-49de-9503-d042f42e7238.png "")

响应头中没有Content-Encoding: gzip
