# 云知声评测接口text字段输入说明
评测服务需要输入文本+音频，才能进行正确的评测。目前评测的text不仅可以传入评测的文本，还可以在text中控制某些功能的开启

## text字段涉及的函数
不同平台涉及的text传入接口函数如下

* Android SDK平台接口： public void setOralText(String oralText)
* ios SDK接口函数：@property (nonatomic, strong) NSString *oralText
* Flash SDK接口函数：public** function**setContent(text:String, serviceType:String = ServiceType.A):void
* H5 SDK接口函数：function start(text, mode)
* http SDK 接口参数：text

## text字段传入文本说明
目前主要有两种格式：纯文本和json格式

### 1.text字段传入纯文本
> 在单词评测、句子评测和篇章评测中，只需要学生跟读就可以，这种题型只要传入纯文本即可，例如，nice to meet you, 只需要在接口中传入纯文本 nice to meet you
|  |  |
| ----- | ----- |
| 说明 | 上传的音频格式 |
| 参数format | 音频格式，可选值为:  mp3 , opus , amrnb |

### 2.text字段传入json

### 3.text字段开启特定功能
