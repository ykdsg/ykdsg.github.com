---
layout: post
title:  python脚本检查文件内容
date:   2013-09-06 14:55:11
---

python脚本，正则表达式

### python脚本检查文件内容
这个是之前就在学python，欣赏python的小巧但是功能强大，是连电池都自带的语言。平时工作中用java ，觉得python在日常生活中比java用处要大，首先语法没那么复杂，特别是io的操作，java里要写一大坨没关的代码。还有就是不用编译，而且linux系统默认都会自带。  
这次遇到的问题是工作当中想要迁移一个系统中的一个模块，这个时候需要评估模块里的代码有没有对其他代码强依赖，就是有没有import 其他模块的代码。如果通过人肉来坐，少量的文件还好，如果有大量的文件实在是很悲剧。这个时候就想起可以用pytho来检索文件，通过正则表达式分析文件内容，把有问题的文件名打印出来就可以了。

{% highlight python %}
import os
import os.path
import re

packDir='/**/src/main/java/com/hz/yk/auction'
p1=re.compile(r"yk\.((?!auction)\w)+\b")
p2=re.compile(r"yk\.((?!domain)\w)+\b")
p3=re.compile(r"yk\.((?!utils)\w)+\b")

def processDirectory(args,dirname,filenames):
	# print 'Directory',dirname
	for filename in filenames:
		if os.path.splitext(filename)[1]=='.java':
			# print 'file',filename
			fileObj=open(dirname+ "/"+filename)
			hasOther=False
			for line in fileObj:
				if p1.search(line) and p2.search(line) and p3.search(line):
					hasOther=True
					print line

			if hasOther:
				print 'file:',filename


def search():
	os.path.walk(packDir,processDirectory,None)

if __name__ == '__main__':
	search()


{% endhighlight %}
因为希望看到应用其他模块的代码，所以排除掉自己的模块名auction和公共的应用domain，utils 。对剩下的符合条件的打印出import这句和文件名sikuli


