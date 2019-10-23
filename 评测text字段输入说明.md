
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
目前主要有两种格式：纯文本和json格式。如果是半开放题型，即有多种答案的题型，必须输入json格式
文本中部分特殊字符不能直接支持评测，需要将特殊字符转换为对应的英文单词，才可以准确评测，主要罗列如下：
>  支持的：序数词，例如1st，sec，月份缩写，星期几缩写；100以内的数字按照数值评分

>  不支持：需要按照字符串读的数字、￥、或是$等币种符号，km、m等物理符号；

>  文本含有换行时，多个文本中间不能有特殊符号，例如

>>  nice to meet you

>>  #nice to meet you

>>  #nice to meet you

> 文本之间的换行符不能有多个

评测文本是作为评测的标准文本，作为判分的依据，文本注意写法规范，例如：

>> 自然拼读 a a apple，不要写成 aa apple.  评测引擎以空格和标点对单词进行区分，a a apple 是作为3个单词进行评测，aa apple 是作为两个单词进行评测。其中写成aa也不是规范的单词，如果碰巧词库中有该词，需要按照词库的发音才能高分，否则会低分；如果不在词库中，aa会被当做生词，生词的评分原则是，如果发音和生词的第一个音素发音相似，则不打低分，否则可能会低分。

>> 评测文本，需要用户完全按照文本读，才会高分，文本不可多写，例如文本是a a，用户只读一个a,则完整度只有50%，整体不会高分；

>> 评测文本不要写看着都不知道怎么读的文本，不是字母也不是单词，例如pl，这类文本学生不知道该怎么读，除非客户端显示音标，同时传评测也标记该文本的音标，否则很难高分；

>> 对于不确定是否是生词的单词，建议业务层在上线文本的时候，评测校验一次，如果确定是正常的单词，可以通过词库加词解决http://101.231.106.182:7777/


### 1.text字段传入纯文本
在单词评测、句子评测和篇章评测中，只需要学生跟读就可以，这种题型只要传入纯文本即可，例如，nice to meet you, 只需要在接口中传入纯文本 nice to meet you


### 2.text字段传入json
json格式的text通过<a href="http://101.231.106.182:5000">置题工具</a>编写句式，即可生成罗列语法、JSGF语法和复述题语法。语法编写的注意事项参照<a href="https://github.com/oraleval/Grammar-rules">语法编写注意事项</a>。半开放题型除了复述题语法，其他可以设置关键字，如果设置了关键字，关键字评测和句式各占总分的50%，即句式中如果只答对关键字，基本可以得到一半的分
当使用韵律评测的时候，json需要自己拼。


* **1）罗列语法**
> 答案的个数有限，可以全部罗列出来，可以用于答案不多的情景问答题型

* **2）JSGF语法**
>  适用于答案较多的题型，评测原理和罗列语法一致<br>当在置题工具中使用变量时，只能生成该种语法

* **3）复述题语法**
>  适用于口头作文和复数题型<br>需要在置题工具中将口头作文或是复述题可能的答案都罗列出来，复述题和口头作文强烈建议使用该语法

* **4）音标评测标记**

韵律评测的json中需要标注音标的开始位置，结束位置和字节长度，如下：
```
{"Version":1,"DisplayText":"inter inter nation nal","Markers":[
{"Type":"phone","Position":{"Start":0,"Length":5},"Value":["ɪ·n·t·ə·r"]},
{"Type":"phone","Position":{"Start":6,"Length":5},"Value":["ɪ·n·t·ə·r"]},
{"Type":"phone","Position":{"Start":12,"Length":6},"Value":["n·æ·ʃ"]},
{"Type":"phone","Position":{"Start":19,"Length":3},"Value":["n·ə·l"]}]}

```

* **5）连读标记**
```
原有标记方式：
{"Grammar": "", "GrammarWeight": "", "Version": 1, "DisplayText": "Far away from home", "Markers": [{"Position": {"Start": 0, "Length": 8}, "Type": "Linking"}]}
简化标记方式：
Far[c:]away from home
```

* **6）重读标记**
```
原有标记方式：
{"Grammar": "", "GrammarWeight": "", "Version": 1, "DisplayText": "you are late", "Markers": [{"Position": {"Start": 8, "Length": 4}, "Type": "SentenceStress"}]}
简化标记方式：
you are late[s:]
```

* **7）升降调标记**
```
原有标记方式：
{"Grammar": "", "GrammarWeight": "", "DisplayText": "Well I'm only supposed to use it for official business", "Markers": [{"Position": {"Start": 46, "Length": 8}, "Type": "Tone", "Value": 1}], "Versions": 1}
简化标记方式：
Well I'm only supposed to use it for official business[t:r]
```

| | |
| ----- | ----- |
| 字段名称 | 含义 |
| Grammar | 固定字段 |
| GrammarWeight | 固定字段 |
| DisplayText | 评测文本 |
| Markers | Position：位置信息；Start：连读开始位置，序号从0开始；Length：连读文本的长度 |
| Type | Linking，连读标记;<br>Tone，升降调标记，输出json中有senTone，0代表调错误，1代表正确<br>SentenceStress，重读标记，用于标记句子中哪些单词是重读；返回json含有StressOfSent，0代表重读错误，1代表重读正确；<br>phone，音标标记 |
| Value | 在Type内容为phone和Tone时生效，Type为phone时，值为IPA88格式音标的数组，；Type为Tone时，值为1（升调）,2（平调）,3（降调） |
|----- | ------ |
简化标记 说明
| 重读[s:] | 需要重读的单词后加标记重读标记，适用用范围为单词或句子中的一个或多个单词 |
| 连读[c] | 需要连读的两个或多个词之间加标记[c:]，适用范围为两个词或是句子中的两个词或是多个词 |
| 升降调[t:r] 和[t:f] | 适用范围为句子，需要升调的句子末尾加标记[t:r]，需要降调的句子末尾加标记[t:f] |
### 3.text字段开启特定功能

```
以下各个功能字段需要时才传入，除了"DisplayText"项，其他均为可选项
{"OralConf": {
        "stress": true,
        "subject": "word",
        "point" :4,
        "phone":true
    },
     "AudioCheckShow": 60,
    "DisplayText": "hello world"
 }
```
* **stress**
> 功能使用场景：句子重音，可以输出句子中的每个单词是否重读

> 描述：值为true则开启

> 返回结果字段：StressOfSent

* **subject**
> 功能使用场景：该字段可以区分题型

> 描述：subject设置为指定的值，即可区分题型：<br>word(单词)，sentence(句子)，chapter(篇章)，选择题(select)，问答题(qa)， 口头作文(composition)， 检错纠错(evalcheck)， 模仿评测(imitate) ，该功能主要用于数据统计，不影响评测

> 返回结果字段：无

* **point**
> 功能使用场景：定制的打分制，当前默认输出是百分制

> 描述：point当前可选值为4和8，即可以按照4分制和8分制输出打分

> 返回结果字段：standardScore

* **phone**
> 功能使用场景：输出tone信息，可用于画用户发音曲线

> 描述：值为true则开启，默认不开启

> 返回结果字段：tone

* **AudioCheck**
> 功能使用场景：音质检测，检测用户录音环境是否符合评测的要求 

> 描述：
>> 检测项：音量过小、截幅、截断、噪音<br>返回结果中的值代表置信度，即可信程度，当音质检测的结果存在不止一种问题时，**服务端会将最可能存在的音质问题的那项结果输出，输出的置信度是10，其他项目输出0**，客户端可以根据10分的音质问题，提示用户改正姿势重读

>> 返回结果字段：audioCheck

>> 字典类型，包含volume（音量过小）、clipping（截幅）、noise（噪音较大）、cut（截断）,tooShort（音频过短）,emptyAudio（空音频），如果emptyAudio的值为true，则说明音频为空，可以直接提示用户未检测到录音等；如果tooShort为true,则提示用户重新录音

>> **默认情况下，引擎默认设置的60分阈值，超出60分，不输出音质检测的结果**

>> 客户端可以通过设置参数，去控制设置在多少分输出音质检测结果，例如：

```
{
    "AudioCheckShow":70,
    "DisplayText": "good"
}

```
>> 则表示70分以上不返回音质检测结果，70分以下返回音质检测结果

>> **建议：** 当打分较高时，不取音质检测的结果，例如当分数>80时，可以忽略音质检测结果，这样可以有效降低一部分误检数据导致的用户体验问题。音质检测主要作为评测的辅助功能，将打分低的一部分音频检测出来，但需要减少因为误检导致的用户体验问题

* **DisplayText**
> 功能使用场景：必填项

> 描述：评测文本

> 返回结果字段：sample


**各个功能返回的json字段请参考<a href="https://github.com/oraleval/FAQ-Docs/blob/master/Json%20Description.md">评测结果json字段说明</a>**

