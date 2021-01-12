# 吉大自动打卡程序
本项目由voidtaoist开源，供吉大学子使用。
一切只为解放生产力！
本项目基于TechCiel/jlu-health-reporter[链接](https://github.com/TechCiel/jlu-health-reporter)进行修改

为吉林大学本科生每日打卡所作的自动机器人。（一测温一点名版）

## 免责声明

本自动程序适用于吉林大学本科生每日健康打卡（一测温一点名），不保证按时更新。研究生打卡是否适用未经测试。

**使用本程序自动提交打卡，你必须实际完成一日一测温，在指定时间回到寝室，并在身体状况出现异常时立刻联系校医院和辅导员。**

__**如运行本程序，您理解并认可，本自动程序的一切操作均视为您本人进行、或由您授权的操作。本程序作者对您因使用此程序可能受到的损失、处罚以及造成的法律后果不负任何责任。**__

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# 使用说明

需要 Python 3 ，先 `pip3 install requests` 。

运行之前**先登录平台提交一次打卡**，务必确保信息准确。

参照 example-config.json 建立配置文件 config.json ，填入登录信息和对应表单项（目前校区、公寓楼、寝室号和部分同学的班级需要程序每次指定）的值（注意均使用字符串值）。

**请一定要正确配置config文件，因为没有正确配置造成的一切后果与程序作者无关**

校区id和公寓楼id也可以在上传的json里查找

目前尚未适配校外居住 请见谅

- 1.获取抓包文件

>进入健康申报后按下f12(推荐使用谷歌浏览器)，将信息按照个人情况填入，之后不要点击提交
  点击保存后，在f12打开的界面中找到_Network_ ，选择开头有_progerss_ 的一项，
  复制里面的全部信息

- 2.配置config文件

>在[JSON在线解析及格式化验证 - JSON.cn]https://www.json.cn/ 输入抓包后的全部信息
之后ctrl+f 搜索个人特征信息，只要其中_fieldS_开头的信息，但是其中有一项日期是_fieldSQrq_
请不要加入config文件。

- 3.为多人打卡请这样添加

```
{
	"transaction": "BKSMRDK",
	"fields": {
		"fieldZtw": "1"
	},
	"conditions": {
		"fieldZtw": "(int(time()%86400/3600)+8)%24 in range(6,12)"
	},
	"tasks": [
		{
			"username": "xxx"
			"password": "x",
			"fields": {	
				"fieldSQxq": "x",
				"fieldSQgyl": "x",
				"fieldSQqsh": "x",
				"fieldSQnj": "xx",
				"fieldSQbj": "xxxx"
			}
		},
		{
			"username": "xxxx",
			"password": "xxxx",
			"fields": {
				"fieldSQxq": "xxxx",
				"fieldSQgyl": "xxxx",
				"fieldSQqsh": "xxxx",
				"fieldSQnj": "xxxxxxxx",
				"fieldSQbj": "xxxx"
			}
		},
		{
			"username": "xxxx",
			"password": "xxxxx",
			"fields": {
				"fieldSQxq": "xxxxxxxxxxxx",
				"fieldSQgyl": "xxxxxxxx",
				"fieldSQqsh": "xxxx",
				"fieldSQnj": "xxxx",
				"fieldSQbj": "xxxx"
			}
		}
	]
}
```
