# dy_trans_tool
> _马哥原创：用python开发的抖音转换工具，目前支持3种功能的转换。_

> _本软件工具仅限于学术交流使用，严格遵循相关法律法规，符合平台内容合法合规性，禁止用于任何商业用途！_

# 一、背景分析
## 1.1 开发背景与功能介绍
<img width="1015" height="184" alt="抖音slogon" src="https://github.com/user-attachments/assets/e7df16d3-8b68-41ce-a8c0-efc1ddb41c88" />

我是[@马哥python说](https://github.com/mashukui)，一枚10年+程序猿，现全职独立开发。

曾经和很多用户聊过，他们希望有一个小工具，可以把抖音个人主页链接（或者sec_uid）转换成抖音号，或者反之（把抖音号转成主页链接/sec_uid），为了满足这类需求，我特意用python开发了这款工具：**dy_trans_tool**

软件支持以下3个功能：

功能1、把个人主页链接批量转换成抖音号：
![主页链接转抖音号](https://files.mdnice.com/user/32110/20c07aa5-6e74-4f59-88ab-836c2e10d831.png)

主页链接转抖音号的结果csv文件：
![抖音转换1.csv](https://files.mdnice.com/user/32110/c9a604f6-fbb6-4b05-abf7-4afb7f84a261.png)

功能2、把抖音号批量转换成主页链接：
![抖音号转主页链接](https://files.mdnice.com/user/32110/f1f8094e-2964-4479-9bbb-3210e15c58e6.png)

抖音号转主页链接的结果csv文件：
![抖音转换2.csv](https://files.mdnice.com/user/32110/abc45922-9d85-4a27-90b8-baa2cd1df1a0.png)

功能3、把app端作品链接批量转换成pc端作品链接：
![image](https://files.mdnice.com/user/32110/3f6fb685-97f8-4a97-ba81-e415b26c7c5f.png)

app端链接转pc端链接的结果csv文件：
![抖音转换3.csv](https://files.mdnice.com/user/32110/996c704f-6827-40a1-8983-50f3edf3662c.png)

以上。

## 1.2 软件说明

几点重要说明，请详读了解：
```
1. Windows系统、Mac系统均可直接运行，对文科生非常友好！
2. 软件通过接口协议爬取，并非通过模拟浏览器等RPA类工具，稳定性较高！
3. 软件目前支持3个功能：主页链接和抖音号互转、app端作品链接转为pc端作品链接
5. 软件运行完成后，会在当前文件夹（即，软件所在文件夹）生成csv结果文件
6. 爬取过程中，每爬一条，存一次csv。并非爬完最后一次性保存！防止因异常中断导致丢失前面的数据（每条间隔1~2s）
7. 爬取过程中，有log文件详细记录运行过程，方便回溯
```
# 二、主要技术
## 2.1 模块介绍

软件全部模块采用python语言开发，主要分工如下：
```python
tkinter：GUI软件界面
requests：爬虫请求
json：解析响应数据
time：间隔等待，防止反爬
csv：保存csv结果
logging：日志记录
```
出于版权考虑，暂不公开完整源码，仅向用户提供软件使用。

## 2.2 部分源码
软件界面：
```python
# 创建主窗口
root = tk.Tk()
root.title('抖音转换工具v1.0 | 马哥python说')
# 设置窗口大小
root.minsize(width=850, height=660)
```
爬虫请求：
```python
# 发送请求
r = requests.post(url, headers=h1, data=json_data)
# 接收响应数据
json_data = r.json()
```
保存数据：
```python
# 存入csv文件
with open(ins.result_file, 'a+', encoding='utf_8_sig', newline='') as f:
	writer = csv.writer(f)
	writer.writerow([url, redId])
```
日志记录：
```python
def get_logger(self):
	self.logger = logging.getLogger(__name__)
	# 日志格式
	formatter = '[%(asctime)s-%(filename)s][%(funcName)s-%(lineno)d]--%(message)s'
	# 日志级别
	self.logger.setLevel(logging.DEBUG)
	# 控制台日志
	sh = logging.StreamHandler()
	log_formatter = logging.Formatter(formatter, datefmt='%Y-%m-%d %H:%M:%S')
	# info日志文件名
	info_file_name = time.strftime("%Y-%m-%d") + '.log'
	# 将其保存到特定目录
	case_dir = r'./logs/'
	info_handler = TimedRotatingFileHandler(filename=case_dir + info_file_name,
											when='MIDNIGHT',
											interval=1,
											backupCount=7,
											encoding='utf-8')
	self.logger.addHandler(sh)
	sh.setFormatter(log_formatter)
	self.logger.addHandler(info_handler)
	info_handler.setFormatter(log_formatter)
	return self.logger
```

# 三、演示视频
软件使用过程演示视频：[【软件演示】抖音批量转换工具，主页链接和抖音号互转！](https://mp.weixin.qq.com/s/kywWBlAEePTVNVy_fw_H3Q)

# 四、付费说明
## 4.1 卡密说明
费用详情：
```python
日卡：使用期限1天，19元。日卡仅能购买一次。适合试用等临时需求
月卡：使用期限1个月，119元。月卡可多次购买。适合短期采集需求
季卡：使用期限3个月，299元。季卡可多次购买。适合中期采集需求
年卡：使用期限1年，599元。年卡可多次购买。适合长期采集需求
```
付费方式：<img width="1528" height="918" alt="收款码v2" src="https://github.com/user-attachments/assets/ec8e8a5f-9d0c-4edd-8498-324c571cb2c3" />

付费后，加我v（493882434）自动掉落登录卡密。

## 4.2 一机一码
软件采用一机一码机制，一个卡密只能在一台电脑运行、不可多电脑运行。

## 4.3 软件多开
一台电脑仅允许运行一个软件，不支持软件多开。

# 五、软件获取
"**抖音转换工具**"首发于公众号"**老男孩的平凡之路**"，欢迎交流！
![二维码-公众号放底部](https://github.com/user-attachments/assets/b98aa9f5-aff2-450f-995d-b5df0172da08)
