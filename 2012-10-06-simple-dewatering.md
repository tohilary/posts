# 实现一个简单的网页正文提取器
- tags: python, beautifulsoup, readbility

---


##准备工作
首先我们得安装BeautifulSoup4:`sudo pip install beautifulsoup4`


然后。。由于搜索到的内容不一定准确，所以我们需要进行一些“验证”：设定一个最小长度，小于这个长度的内容直接抛弃；同时如果已经搜索到内容，那么在获取新内容的时候先将两者的长度进行比较，如果新内容比之前获取的内容长就替换之（因为正文的内容肯定是网页中最长的一部分）。
我写了一个函数来干这事：
```python
    def _set_content(self, article):
        if len(article) < Dewatering.MIN_LENGTH:
            return False
        if len(article) < len(self.content):
            return False
        self.content = unicode(article)
```

##正式提取
我们得先创建一个BS实例:`soup = BeautifulSoup(html)`

提取正文的第一步，肯定得先删去无用的标签：
```python
        for style in self.soup.find_all('style'):
            style.extract()
        for style in self.soup.find_all('script'):
            style.extract()
        for style in self.soup.find_all('link'):
            style.extract()
```

删掉无用标签之后，首先想到的肯定是提取<article>里面的内容：
```python
        article = self.soup.article
        if article:
            self._set_content(article)
```

如果没有<article>标签。。那么就该根据class/id搜索div了：
```python
        for kls in Dewatering.CONTENT_CLASSES:
            tags = self.soup.find_all("div", {"class": re.compile(kls)})

            for tag in tags:
                self._set_content(tag)
```

于是= =一个~~坑爹的~~网页正文提取器就这么出来了

---

最后的成品：https://github.com/whtsky/dewatering

---

参考：
https://github.com/mitnk/briticle/blob/master/briticle.py
https://github.com/kingwkb/readability/blob/master/readability.py