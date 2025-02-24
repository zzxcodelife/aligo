# aligo

🚀🔥 简单、易用、可扩展的阿里云盘 API 接口库 👍👍

[wiki 文档](https://github.com/foyoux/aligo/wiki) + [examples](https://github.com/foyoux/aligo/tree/main/examples)

> 文档写得很简单，详情请查看 代码提示 + 文档注释
> 
> 有任何疑问 请 [issue](https://github.com/foyoux/aligo/issues/new?assignees=&labels=&template=bug_report.md&title=)
> 或 加入 **aligo交流反馈群** （群二维码在底部）

[![python version](https://img.shields.io/pypi/pyversions/aligo)](https://pypi.org/project/aligo/)  [![Downloads](https://static.pepy.tech/personalized-badge/aligo?period=total&units=international_system&left_color=black&right_color=orange&left_text=Downloads)](https://pepy.tech/project/aligo)

```bash
pip install --upgrade aligo
```

## 快速入门

```python
"""快速入门"""
from aligo import Aligo

if __name__ == '__main__':
    ali = Aligo()  # 第一次使用，会弹出二维码，供扫描登录
    
    user = ali.get_user()  # 获取用户信息
    print(user.user_name, user.nick_name, user.phone)  # 打印用户信息
    
    ll = ali.get_file_list()  # 获取网盘根目录文件列表
    for file in ll:  # 遍历文件列表
        print(file.file_id, file.name, file.type)  # 打印文件信息
```

https://user-images.githubusercontent.com/35125624/150529002-c2f1b80b-fb11-4e0a-9fd7-6f57f678ccf5.mp4

## 基本功能

- [x] 完全的代码提示
- [x] 福利码兑换
- [x] 文件夹同步
- [x] 在线解压缩
- [x] 支持功能扩展
- [x] 搜索文件/标签
- [x] 获取重复文件列表
- [x] 文件（夹）重命名
- [x] 文件（夹）上传下载
- [x] 文件（夹）移动复制
- [x] 文件（夹）删除恢复
- [x] 文件（夹）分享 保存 收藏
- [x] 持久化登录、多帐户登录
- [x] 文件（夹）自定义分享（无限制）
- [x] 获取帐户、云盘（容量）等基本信息
- [x] 。。。。。。
- [x] ⭐⭐⭐ 欢迎大家发起 [新功能请求](https://github.com/foyoux/aligo/issues/new?assignees=&labels=&template=feature_request.md&title=)

> **温馨提示：**
>   1. 由于秒传链接的失效，自定分享信息的有效期只有4个小时。
>   2. 阿里云盘不同于其他网盘或系统，其定位文件不是基于文件名（路径），而是通过 `file_id`，这才是唯一定位文件的方式，**aligo** 中提供了简便函数 `get_file_by_path`/`get_folder_by_path`，通过网盘路径获取文件对象，通过 其上的 `file_id` 属性即可获取所需文件标识。但不建议频繁使用此方法，因为内部是通过 `get_file_list` 遍历得到的。


## 网页扫码登录

```python

from aligo import Aligo

# 提供 port 参数即可, 之后打开浏览器访问 http://<YOUR_IP>:<port>
ali = Aligo(port=8080)
```


## 发送登录二维码到邮箱（推荐）
**最佳实践**：建议将邮箱绑定到微信，这样能实时收到提醒，登录过期后也可以第一时间收到登录请求。

**安全性问题**：虽然自带公开邮箱，但是他人并不能通过这个获取任何人发送的邮件，所以 防伪字符串 策略是安全的。

```python

from aligo import Aligo


"""
email: 发送扫码登录邮件 ("接收邮件的邮箱地址", "防伪字符串"). 提供此值时，将不再弹出或打印二维码
        关于防伪字符串: 为了方便大家使用, aligo 自带公开邮箱, 省去邮箱配置的麻烦.
        所以收到登录邮件后, 一定要对比确认防伪字符串和你设置一致才可扫码登录, 否则将导致: 包括但不限于云盘文件泄露.
"""

# 提供 email 参数即可
ali = Aligo(email=('xxx@qq.com', '防伪字符串，可任意字符串'))
```

## 如何彻底删除文件？
> 无需先移动文件到回收站

此功能太危险，**aligo** 未直接提供。不过 [这里](https://github.com/foyoux/aligo/wiki/%E8%87%AA%E5%AE%9A%E4%B9%89%E5%8A%9F%E8%83%BD---%E5%BD%BB%E5%BA%95%E5%88%A0%E9%99%A4%E6%96%87%E4%BB%B6) 扩展了该功能，请小心使用！


## 关于扩展功能
这个功能讲得很少，因为觉得没什么好讲的，参考 **彻底删除文件** 章节应该一下子就可以看懂。

一直也没有人反馈或者咨询这个功能，觉得用的人大概很少，所以稍微说下。

一般步骤：

    1. 使用浏览器或其他抓包工具，观察通信过程；
    2. 获取 url/path + 请求体；
    3. 继承 `Aligo`, 使用现有的方法 `self._post` 等，进行发送请求；
    
会自动维护 **token**, 你只需关注如何发送请求即可

[扩展功能举栗🌰 - 配有视频和代码](https://github.com/foyoux/aligo/issues/24)


## 声明

此项目仅供学习交流，若有不妥之处，侵联必删。

此项目仅供学习交流，若有不妥之处，侵联必删。

此项目仅供学习交流，若有不妥之处，侵联必删。

---

<table align="center">
    <thead align="center">
    <tr>
        <td><h2>❤️‍🔥欢迎加入🤝🏼</h2></td>
    </tr>
    </thead>
    <tbody align="center">
    <tr>
        <td><img src="http://110.42.175.98:5512/down/LKPvT9xK2lFx?fname=/aligo/wechat.jpg" alt="aligo反馈交流群"/></td>
    </tr>
    </tbody>
    <tfoot align="center">
    <tr>
        <td>😃 二维码会保持更新 😜</td>
    </tr>
    </tfoot>
</table>