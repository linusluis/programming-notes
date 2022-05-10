## 1、git本地push到github仓库失败问题汇总

```shell
error: failed to push some refs to 'https://github.com/linusluis/programming-notes.git' 
```    

![git本地push到github仓库失败问题](https://github-img.oss-cn-beijing.aliyuncs.com/programming_notes/git%26github/git%E6%9C%AC%E5%9C%B0push%E5%88%B0github%E4%BB%93%E5%BA%93%E5%A4%B1%E8%B4%A5%E9%97%AE%E9%A2%98.png?Expires=1651330235&OSSAccessKeyId=TMP.3Kj5gz4KoLrm9uZSjSNuErW6xzWaRyxg6Rh1DZXMd1VBCvAyHKUvqNh3JTogJYy6kZuLmdrCQ7ufd3Lxp8rGhXpRygSx8N&Signature=CjsHBGC%2Ban7XCQiNlSuIs6QCanU%3D&versionId=CAEQHRiBgIDmkPnqgxgiIGFiZjMyYzUzZTExNTQ2YzA4NDc1OWMzOTViMjczMjM5)

问题剖析：  
  
们在创建仓库的时候，都会勾选“使用Readme文件初始化这个仓库”这个操作初识了一个README文件并配置添加了忽略文件。当点击创建仓库时，它会帮我们做一次初始提交。于是我们的仓库就有了README.md和.gitignore文件，然后我们把本地项目关联到这个仓库，并把项目推送到仓库时，我们在关联本地与远程时，两端都是有内容的，但是这两份内容并没有联系，当我们推送到远程或者从远程拉取内容时，都会有没有被跟踪的内容，于是你看git报的详细错误中总是会让你先拉取再推送，但是拉取总是失败。  
  
    
解决方法：
1. 使用这个命令：`git pull --rebase 仓库地址 main`
2. 再进行push：`git push -u 仓库地址 master`
