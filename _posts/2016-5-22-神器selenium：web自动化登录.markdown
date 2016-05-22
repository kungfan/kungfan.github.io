---
layout: post
location: Huang Gang
---


最近发现了一个好东西：[selenium](docs.seleniumhq.org),一个用于Web应用程序测试的工具,利用selenium，我们可以让它模拟我们操作浏览器，就像是我们自己在操作浏览器一样，比如我们可以让它自动登录微博，自动发送微博，我们也可以用它来做爬虫，自动爬取网络中需要的内容，我们还可以用它来投票刷票，甚至我们还可以利用它做暴力破解，破解别人空间或邮箱密码。selenium功能十分强大，能让我们浏览操作网页的行为完全自动化，它能做到的事情完全取决于我们的想象力。

Selenium 可以在 Windows、Linux 和 Macintosh上的 Internet Explorer、Mozilla 和 Firefox 以及chrome中运行，你可以在firefox中直接用SeleniumIDE插件直接录制脚本，自动化完成任务，也可以利用自己熟悉的语言（我比较喜欢python）来编写脚本，执行自动化，selenium官方文档比较详细，大家可以仔细看看，下面就介绍下利用selenium自动登陆微信.


####安装selenium

安装selenium非常简单，只需打开cmd 输入：`pip install -U selenium` 即可完成安装。我个人是在windows 10 平台下，已经安装了python2.7和pip，若没有pip，可以到官网或[github下载源码](https://github.com/SeleniumHQ/selenium), 解压后利用 `python setup.py install`手动安装. 安装完成后，我们再在python下 import selenium，看看是否报错，若没报错则表示selenium包安装成功。python 的selenium包默认只支持firefox，要想让它支持win 10 的Edge，还要安装一个驱动：[MicrosoftWebDriver](https://www.microsoft.com/en-us/download/details.aspx?id=48212),MicrosoftWebDriver安装完成后还要将MicrosoftWebDriver.exe的路径加入系统默认路径，这样就可以用selenium驱动 Edge了。

####自动登录代码

在完成selenium安装工作后，基本的准备工作就完成了。我们再来编写一个小实例，让selenium完成启动Edge浏览器，打开指定网页，自动填写登录框用户名和密码，然后模拟鼠标点击登录按钮，完成登录过程。整个过程完全自动化，不需要人为干预。

{% highlight python lineanchors %}

    # -*- coding: utf-8 -*-

    ```
    version = '0.0.1'
    author = 'kongfan'
    Created on Sat May 22 
    利用selenium模拟操作浏览器，完成自动登录微信
    
    ```

    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys


    def autologin(id="",pw=""):    
    
    	```
	    autologin 是自动登录微信公众号函数，id是你的用户名，pw是你的密码

    	```
        driver = webdriver.Edge()
        driver.get("https://mp.weixin.qq.com/");
    
       
        elem_pwd = driver.find_element_by_id("account")
        elem_pwd.send_keys(id)
        elem_pwd = driver.find_element_by_id("pwd")
        elem_pwd.send_keys(pw)
        elem_pwd.send_keys(Keys.RETURN)
        
        print "登录微信成功！"

    autologin(id="你的用户名",pw="你的密码") 

{% endhighlight %}

运行上面代码，就可以自动登录微信公众号，更进一步我们可以将其他程序产生的结果自动推送给公众号订阅用户，比如我可以将爬虫爬到的数据经过加工后推送给用户，将实验室检测结果定向推送，将量化策略筛选的股票代码定向推送等。selenium可以解放我们的双手，极大提供生产效率，有兴趣的同学可以好好研究一下。

<p></P>

**P.S** ：最近碰到单位同事参与系统内评优评先，评比方式以网络投票和局内综合评审相结合，其中网络投票是一个比较重要的一环，得票数的多少直接关系到是否能被评上。本人看了下投票系统非常简单，就一个form 将序号ID，和评价 直接post给服务器，服务器端再做人工审核，没有验证码，没有做js前端控制，非常容易刷票，以上代码非常容易就可以改成刷票器，再通过动态ip代理，突破IP限制，完全可以刷票。









