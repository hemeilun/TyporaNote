# typora利用PicGo+Github上传图片

<br/>

上传到github是为了在所有地方均可以直接访问到图片

<br/>

## 1.Github创建仓库并产生token

<br/>

（1）注册一个github 的账号

（2）点击 **头像 -> Your Profile  -> Pepositories -> new**  进行创建仓库
<br/>
<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo6.png" alt="Picgo6" style="zoom:80%;" />



<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo7.png" alt="Picgo7" style="zoom:80%;" />


<br/><br/><br/>
（3）填完信息后进行创建
<br/>
   仅需填写仓库名和描述即可
<br/>

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo8.png" alt="Picgo8" style="zoom: 80%;" />


<br/><br/><br/><br/>
（4）获取 token（token只会展示一次，请注意保存，不过忘记了可以直接重新创建一个）
<br/>
<1> 点击  **头像 -> Settings** ，进入设置

<2>点击 **developer Settings** ，进入此界面



<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo9.png" alt="Picgo9" style="zoom:80%;" />

<br/>
<br/><br/>

<3>点击 **Personal access tokens** ,进入

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo10.png" alt="Picgo10" style="zoom:80%;" />



<br/><br/><br/>
<4>点击 **generate new token**  ，创建 token

<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo11.png" alt="Picgo11" style="zoom:80%;" />



<br/><br/><br/>

<5>填入 描述 ，设置 此token的期限(Expiration) ,将底部直接全部勾选，进行创建

<6>创建成功后跳转回上一个界面，底部生成的码即为 token（记得保存，一会要用的）



<br/><br/><br/><br/><br/><br/><br/><br/>

## 2.下载PicGo

<br/>

（1）点击  typora左上角的 **文件 ->  偏好设置   ->   图像**    到达

![PicGo1](https://cdn.jsdelivr.net/gh/hemeilun/picture/PicGo1.png)

<br/><br/><br/>

（2）找到左下角的 **上传服务**   再点击**下载PicGo** 即可跳转到  PicGo的下载界面  

         点击免费下载，跳转到 Github中 的下载界面 ，向下滑动 到此处
    
      其中  **dmg 为 Mac** 的版本  ，**x64 为 Windows** 的版本，点击即可下载



<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo2.png" alt="Picgo2" style="zoom:80%;" />






<br/><br/><br/>
（3）下载后为中文界面，直接傻瓜式一步安装

（4）安装成功后到安装路径下找到 **PicGo.exe** 点击后运行（**点击运行后并不会直接出现界面，需要在任务栏点击后出现界面**）



![Picgo3](https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo3.png)

![Picgo5](https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo5.png)



<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo13.png" alt="Picgo13" style="zoom:80%;" />


<br/><br/><br/>
（5）点击 **图床设置** ，选择 **Github图床** 进行设置



设定仓库名为：github的用户名/刚才创建的仓库名

                       比如：我的用户名为 admin    仓库名为 ：bbb     那就是  admin/bbb

设定分支名为：master（我设置为main不知道为什么出现了错误）

设定token为： 刚才保存的 token 值


<br/><br/>
### 这个加速很重要

（这一点非常重要，可以在不翻墙的情况下访问到你的图片）

**设定自定义域名为：https://cdn.jsdelivr.net/gh/  +  用户名 + / + 仓库名**

                          **比如：https://cdn.jsdelivr.net/gh/admin/bbb**


<br/><br/>
点击确定，配置完成
<br/>
<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo14.png" alt="Picgo14" style="zoom:80%;" />

<br/><br/><br/><br/><br/><br/><br/><br/>

## 3.返回Ttpora进行配置


<br/>
（1）左上角 **文件 ->  偏好设置   ->   图像**    

![PicGo1](https://cdn.jsdelivr.net/gh/hemeilun/picture/PicGo1.png)
<br/><br/><br/>
（2）配置 **PicGo的路径**，选择 安装的**PicGo.exe** ,完成后进行 下方的 **验证图片上传选项**



<img src="https://cdn.jsdelivr.net/gh/hemeilun/picture/Picgo15.png" alt="Picgo15" style="zoom:80%;" />

<br/><br/><br/>
（3）测试成功即可上传图片到 github 的仓库中