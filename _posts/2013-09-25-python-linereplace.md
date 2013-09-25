---
layout: post
title:  python替换指定行内容
date:   2013-09-25 09:22:11
---

python脚本，正则表达式，替换指定行

### python脚本检查文件内容
这次遇到的问题是工作中需要迁移代码，并把原来的日志系统更新到现在的格式，原来获取log的格式是
{% highlight java %}
AuctionPoolLoggerUtil.getLogger()  
{% endhighlight %}
现在获取log的格式是：
{% highlight java %}
LoggerFactory.getLogger(XXXXX.class)  
{% endhighlight %}
这里的XXXXX需要替换为当前的类名。如果这样的java文件不多还好，可以一个个人肉替换。一旦这样的文件很多，特别是迁移过来大量的文件时，你就会发现简直是一场灾难。其实我们发现上面的工作很多是机械单调的。ide中的替换功能不能做到的是把XXXXX替换成当前的类名。而python很容易处理文本，利用正则表达式可以比较方便的拿到类名，然后替换掉xxxxx就可以了。

{% highlight python %}
import fileinput  
import os  
import re  
  
__author__ = 'ykdsg'  
  
packDir='/Users/ykdsg/svn_workspace/auctionplatform/misc_refactory/auctionplatform/ap-biz/src/main/java/com/yk/misccenter'  
#查找class name  
findClassNameP=re.compile(r"(?<=class\s)\w*")  
findXP=re.compile(r"XXXXX")  
  
  
def processDirectory(args,dirname,filenames):  
    # print 'Directory',dirname  
    for filename in filenames:  
  
        if os.path.splitext(filename)[1]=='.java':  
            # print 'file',filename  
            fullFileUrl=dirname+ "/"+filename  
            fileObj=open(fullFileUrl)  
            className=''  
            # Optional in-place filtering: if the keyword argument inplace=1 is passed to fileinput.input()  or to  
            # the FileInput constructor, the file is moved to a backup file and standard output is directed  to the  
            # input file (if a file of the same name as the backup file already exists, it will be replaced silently)  
            # .  This makes it possible to write a filter that rewrites its input file in place.  If the backup  
            # parameter is given (typically as backup='.<some extension>'), it specifies the extension  for the  
            # backup file, and the backup file remains around; by default, the extension is '.bak' and it is deleted  
            #  when the output file is closed. In-place filtering is disabled when standard input is read.  
            for line in fileinput.input(fullFileUrl, inplace=1):  
                matchClass = findClassNameP.search(line)  
                if matchClass:  
                    className = matchClass.group()  
                matchX=findXP.search(line)  
                if matchX:  
                    #print 后面需要有, 否则会出现多余的空行  
                    print line.replace('XXXXX',className),  
                else:  
                    print line,  
  
  
def search():  
    os.path.walk(packDir,processDirectory,None)  
  
if __name__ == '__main__':  
    search()  
{% endhighlight %}

上面的脚本中大部分是fileinput.input的注释，就是说了inplace=1其实就是把源文件的内容放到缓存区，然后直接将内容写入源文件
findClassNameP 是查找class name的正则表达式，上面的逻辑就是对文件逐行分析，拿到class name。然后再分析当前行是否有xxxxx，有的话就用class name 替换，没有的话就原行输出。

