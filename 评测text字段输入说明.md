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
在单词评测、句子评测和篇章评测中，只需要学生跟读就可以，这种题型只要传入纯文本即可，例如，nice to meet you, 只需要在接口中传入纯文本 nice to meet you


### 2.text字段传入json
json格式的text通过<a href="http://101.231.106.182:5000">置题工具</a>编写句式，即可生成罗列语法、JSGF语法和复述题语法。语法编写的注意事项参照<a href="https://github.com/oraleval/Grammar-rules">语法编写注意事项</a>

|  |  |  |
| ----- | ----- |----- |
| 语法类型 | 使用场景 | 备注 |
| 罗列语法 | 当答案的个数有限，可以全部罗列出来，传入的text就可以使用该种语法 | 可以用于答案不多的情景问答题型 |
| JSGF语法 | 适用于答案较多的题型，评测原理和罗列语法一致，当在置题工具中使用变量时，只能生成该种语法 |  |
| 复述题语法 | 适用于口头作文和复数题型，需要在置题工具中将口头作文或是复述题可能的答案都罗列出来 | 复述题和口头作文强烈建议使用该语法 |

### 3.text字段开启特定功能

|  |  |  |  |
| ----- | ----- |----- |----- |
| 语法类型 | 功能使用场景 | 功能描述 | 备注 |
