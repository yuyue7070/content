+++
title = "Selenium"
date = 2024-08-12T22:34:28+08:00
author = "rainbow"
tags = ["python", "Selenium"]
cover = ""
summary = "selenium库的一些基础"
+++


# Selenium

[白月黑羽selenium (byhy.net)](https://www.byhy.net/auto/selenium/01/)



## selenium功能

1. 点击界面按钮
2. 文本框输入文字
3. 在web界面获取信息，然后用程序进行分析处理

浏览器驱动：相当于把写的代码翻译为浏览器能运行的，不同的浏览器它们的驱动不同



## 模块的调用

问题：在控制面版中下载selenium模块后，在pycharm中无法调用该模块

原因：pycharm中使用了虚拟环境

解决办法：Alt+F12打开终端窗口，若前面出现了(venv)，则表面使用了虚拟环境，则在该终端窗口再进行一次模块安装



## webdriver

功能：操控浏览器

### 浏览器的打开

```Python
# get() 方法通常在测试用例的开始处使用，以导航到要测试的页面

# get()方法
# 会等待页面加载完成，但它不会等待 JavaScript 和 Ajax 调用完成。
# 如果页面加载失败，get() 方法将抛出异常。
# 对于跨域请求，get() 方法可能会受到同源策略的限制。
# get() 方法会覆盖当前页面上的任何现有内容。

#替代方法：在某些情况下，可能需要使用 navigate().to() 方法代替 get() 方法。navigate().to()方法不会等待页面加载完成，这在某些情况下可能有用，例如在执行导航后立即需要执行操作时

from selenium import webdriver
from selenium.webdriver.chrome.service import Service	# 理解为特殊形式防止报错

wd=webdriver.Chrome(service=Service(r'E:\tool\chromedriver-win64\chromedriver.exe'))
#	E:\tool\chromedriver-win64\chromedriver.exe	为对应浏览器的驱动地址
	#	若将驱动所在目录加入环境变量Path中，则可以不输入驱动地址，注意：不是浏览器驱动全路		    径， E:\tool\chromedriver-win64\chromedriver.exe而是 浏览器驱动所在目录			 E:\tool或者E:\tool\chromedriver-win64
    	
#	等号右边返回的是 WebDriver 类型的对象，我们可以通过这个对象来操控浏览器，如 打开网址、选择界面元素等


wd.get('')	# 构建一个请求发给浏览器驱动，浏览器驱动然后转发给浏览器
# 括号中为所要打开的网址
```



### 选择元素

要操控元素首先需要定位界面元素

界面按F12打开开发者工具

点击红圈内元素后再点击想要查找的元素

或者直接在要查找的元素位置右键，检查（耗费CPU资源）



#### 通过ID查找

若ID唯一

```python
from selenium import webdriver
from selenium.webdriver.common.by import By	# By是其中的一个类

wd = webdriver.Chrome()
wd.get('https://www.byhy.net/_files/stock1.html')

# 定位元素
element = wd.find_element(By.ID, '')	#ID是By中的一个属性，空处填ID的名称
# 根据id选择元素，返回的就是该元素对应的WebElement对象

# 操作元素
# 通过该WebElement对象，就可以对页面元素进行操作了
element.send_keys('')
element.click()
# click()方法相当于操作鼠标点击
# send_keys()方法相当于在你定位的元素里进行输入
```



