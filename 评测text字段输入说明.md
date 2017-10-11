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
当使用韵律评测的时候，json需要自己拼

* **普通评测的json**

>| text类型 | 使用场景 | 备注 |
>| :--- | :--- | :--- |
>| 罗列语法 | 当答案的个数有限，可以全部罗列出来，传入的text就可以使用该种语法 | 可以用于答案不多的情景问答题型 |
>| JSGF语法 | 适用于答案较多的题型，评测原理和罗列语法一致，当在置题工具中使用变量时，只能生成该种语法 |  |
>| 复述题语法 | 适用于口头作文和复数题型，需要在置题工具中将口头作文或是复述题可能的答案都罗列出来 | 复述题和口头作文强烈建议使用该语法 |

* **韵律评测json**

韵律评测的json中需要标注音标的开始位置，结束位置和字节长度，如下：
```
> {"Version":1,"DisplayText":"ɪntər ɪntər næʃ nəl","Markers":[{"Type":"phone","Position":{"Start":0,"Length":5},"Value":["ɪ·n·t·ə·r"]},{"Type":"phone","Position":{"Start":6,"Length":5},"Value":["ɪ·n·t·ə·r"]},{"Type":"phone","Position":{"Start":12,"Length":3},"Value":["n·æ·ʃ"]},{"Type":"phone","Position":{"Start":16,"Length":3},"Value":["n·ə·l"]}]}

```


### 3.text字段开启特定功能

```
"OralConf": {
        "stress": true,
        "subject": "word",
        "point" :4,
        "phone":true
    },
     "AudioCheck": true,
    "DisplayText": "hello world
```


>| 字段名称 | 功能使用场景 | 描述 | 备注 | 返回结果字段 |
>| :---: | :--- | :--- | :--- | :--- |
>| stress | 句子重音，可以输出句子中的每个单词是否重读 | 值为true则开启 |  | StressOfSent |
>| subject | 该字段可以区分题型 | subject设置为指定的值，即可区分题型：word(单词)，sentence(句子)，chapter(篇章)，选择题(select)，问答题(qa)， 口头作文(composition)， 检错纠错(evalcheck)， 模仿评测(imitate) | 该功能主要用于数据统计，不影响评测 | 无 |
>| point | 定制的打分制，当前默认输出是百分制 | point当前可选值为4和8，即可以按照4分制和8分制输出打分 | 默认不使用 | standardScore |
>| phone | 输出tone信息，可用于画用户发音曲线 | 值为true则开启 | 默认不开启 | tone |
>| AudioCheck | 音质检测，检测用户录音环境是否符合评测的要求 | 检测项：音量过小、截幅、截断、噪音，返回结果中的值带便置信度，即可信程度，值范围0-10，数值越大的那项，最可能有问题 | 建议将置信度最高的那个问题返回给客户，提示用户改正姿势重读 | audioCheck |
>| DisplayText | 必填项 | 评测文本 |  |  |

各个功能返回的字段请参考<a href="https://github.com/oraleval/FAQ-Docs/blob/master/Json%20Description.md">评测结果json字段说明</a>

