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

