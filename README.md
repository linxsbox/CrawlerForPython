# CrawlerForPython
一个爬虫程序，通过爬取拉钩网站的招聘信息来分析相关的职业技能和要求。

## Jupyter Error 记录
使用 Jupyter 时遇到的一系列问题记录以及解决方法

### 500 : Internal Server Error
- jupyter_contrib_nbextensions 扩展安装遗留问题
- nbconvert 版本未更新。以及相关扩展未更新
- ipython 未更新，主要与 Jupyter 所需版本不一致


### Jupyter kernel error
- 权限问题，未使用管理员权限启动
- 安装路径问题，修改后重启 【Anaconda3\share\jupyter\kernels\python3\kernel.json】

---

## 拉勾网错误
通过首页的职业标签进入列表页后，先搜索公司名称，返回结果后再次搜索公司名称就会触发搜索功能，则浏览器地址会跳转至跟踪链接，进入 debugger 状态然后将页面卡死且无法跳出 debugger 的状态（F12状态下）。
当时我只是想查看搜索请求接口需要的参数，好作为爬取的参数传入。

这里以输入 **腾讯** 和 **阿里** 作为例子。

复现步骤：
1. 首页标签进入列表页 **url：** https://www.lagou.com/zhaopin/webqianduan/?labelWords=label
2. 在输入框中输入“腾讯” **url：** https://www.lagou.com/jobs/list_%E8%85%BE%E8%AE%AF/p-city_215?&cl=false&fromSearch=true&labelWords=sug&suginput=tengxun
3. 返回结果后再次输入“阿里” **url：** https://www.lagou.com/utrack/trackMid.html?f=https%3A%2F%2Fwww.lagou.com%2Fjobs%2Flist%5F%25E9%2598%25BF%25E9%2587%258C%2Fp-city%5F215%3F%26cl%3Dfalse%26fromSearch%3Dtrue%26labelWords%3D%26suginput%3D&t=1570626543&_ti=1

---

## 问题记录
### 2019-10-10 22:45
在爬取数据后对比页面列表数据，发现**数据不一致**。在尝试了多个方式和查看请求信息后发现请求携带的 **cookie** 不一样，爬取代码携带的是认证 **cookie** 而网站上除了认证 **cookie** 之外还携带了多个 **cookie** 的信息。而携带的这些 **cookie** 会影响返回的数据信息，我在尝试去排除非必要信息时发现大部分的 **cookie** 是固定的且与用户相关，有3条 **cookie** 是动态的，每次请求后都会发生变化。

目前如果想实现根据条件请求接口获取所需的数据信息的话，那么就需要先找到生成这3条cookie的请求或接口，以便获取，然后再将固定信息的 cookie 与之合并，在请求时携带应该就可以获取根据条件返回的数据结果了。（待验证）