# 版本管理

## <a name="wfm4sx"></a>nvm
### <a name="fel6qx"></a>nvm是什么
在windows上按照执行exe文件的方式安装node没法在本地开发过程中切换版本,当一个项目依赖比如说6.9.5版本,而另一个项目依赖8.11.2版本的时候,当切换到不同的项目运行时,需要重新安装node,非常麻烦,而nvm解决了这个问题.
### <a name="ysoduf"></a>安装nvm   
nvm网址:[https://github.com/creationix/nvm](https://github.com/creationix/nvm)
widows版nvm下载地址:[https://github.com/coreybutler/nvm-windows/releases](https://github.com/coreybutler/nvm-windows/releases)
安装时需要几下下面的路径,下面要用到


![image.png | left | 509x388](https://cdn.yuque.com/yuque/0/2018/png/111166/1527752328731-bd769db5-1194-4702-8985-b5ce13c45cfb.png "")

安装完以后命令行执行:
```powershell
nvm
```



![image.png | left | 827x366](https://cdn.yuque.com/yuque/0/2018/png/111166/1527751822393-f48c0623-4ae4-4a87-9ddc-bb13b8abc03b.png "")

出现上面的画面说明安装成功
```powershell
nvm list //本地node版本查看
```


![image.png | left | 490x409](https://cdn.yuque.com/yuque/0/2018/png/111166/1527751915855-15f3b18d-b13b-4d46-aedd-9820b8a63891.png "")

安装node
```powershell
nvm install 8.11.2 
```

为了加快安装速度我们配置下淘宝镜像
这步要用到上面的路径D:\develop\nvm了
执行路径下install.cmd,已管理员权限运行,要不然可能会失败


![image.png | left | 677x441](https://cdn.yuque.com/yuque/0/2018/png/111166/1527752482587-3521a6ea-61de-419e-b0a6-93da2a386db3.png "")


在后面输入D:\develop\nvm,就是你nvm的存放路径,或者直接按回车,这时候弹出下面窗口



![image.png | left | 827x522](https://cdn.yuque.com/yuque/0/2018/png/111166/1527752795237-0f308436-8903-45ae-b87b-c7e6bc0a2ffb.png "")

* root ： nvm的存放地址
* path ： 存放指向node版本的快捷方式，使用nvm的过程中会自动生成。一般写的时候与nvm同级。
* arch ： 电脑系统是64位就写64,32位就写32
* proxy ： 代理
我们在里面加点东西
```plain
root: D:\develop\nvm 
path: C:\Program Files\nodejs 
arch: 64 
proxy: none
node_mirror: http://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/

```
我们使用了淘宝镜像加快了安装速度
### <a name="6ia6gh"></a>安装node
<span data-type="color" style="color:rgb(199, 37, 78)"><span data-type="background" style="background-color:rgb(246, 246, 246)">nvm install [版本号]</span></span>

```plain
nvm install 8.11.2
```

然后可以查看版本



![image.png | left | 620x166](https://cdn.yuque.com/yuque/0/2018/png/111166/1527753310530-1f110432-3426-476b-b23f-d603de62f466.png "")


我们用 <span data-type="color" style="color:rgb(199, 37, 78)"><span data-type="background" style="background-color:rgb(246, 246, 246)">nvm use [版本号]</span></span>可以切换使用哪个node版本

### <a name="rrovmt"></a>nvm高级使用
待更新....

