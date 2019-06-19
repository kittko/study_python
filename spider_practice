import requests
from bs4 import BeautifulSoup

# 获取章节页面
def get_url(url):
	headers = {'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.90 Safari/537.36'}
	response = requests.get(url, headers = headers)
	response = response.text
	soup = BeautifulSoup(response, 'lxml')
	text = soup.dl.children
	return text

# 获取章节内容
def get_html(text):
	for child in text:
		try:
			html = "https://www.biquge.com.cn" + child.a.get('href')
			get_novel(html)
		except AttributeError:
			pass

#下载各章节内容
def get_novel(url):
	headers = {'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/75.0.3770.90 Safari/537.36'}
	response = requests.get(url, headers)
	response = response.text.encode('ISO-8859-1')
	soup = BeautifulSoup(response, 'lxml')
	name = soup.h1.string#获取章节标题
	text = soup.find('div', id="content")#获取小说内容
	with open('%s.txt' % name,'w',encoding='utf-8') as f:
		f.write(text.text)

url = "https://www.biquge.com.cn/book/15517/"
text = get_url(url)
get_html(text)
