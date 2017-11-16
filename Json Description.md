### 评测返回结果中Json字段说明


| 名称| 类型 | 说明 |
| :----- | :----- | :----- |
| version | string | 结果格式版本及版本号 |
| lines | array | 每行输入文本的评测结果 |
| EvalType | string | 评测类型：general（朗读评测）、askandanswer（情景问答）、composition（作文） |
| sample | string | 输入的标准文本 |
| usertext | string | 用户实际朗读的文本（语音识别结果） |
| begin | double | 开始时间，单位为秒 |
| end | double | 开始时间，单位为秒 |
| volume | double | 音量 |
| score | string | 分值 |
| subwords | double | 单词包含的音标 |
| integrity | double | 录入语音的完整度 |
| pronunciation | double | 录入语音的标准度 |
| fluency | double | 录入语音的流利度 |
| words | array | 每个词的评测结果 |
| text | string | 单词或音素文本 | 词的字符串，使用"sil"表示语音中的静音段 |
| type | int | 类型，共有6种类型，分别是：0 多词；1 漏词；2 正常词；3 错误词；4 静音；5 重复词；8 生词 |
| sentSample | array | 句式标准文本 |
| sentScore | array | 句式总分 |
| sentPronunciation | array | 句式标准度得分 |
| sentFluency | array | 句式流利度得分 |
| sentIntegrity | array | 句式完整度得分 |
| keySample | array | 关键词sample（包括关键词和每个关键词的得分 |
| keysScore | array | 关键词总分 |
| keysPronunciation | array | 关键词标准度得分 |
| keysIntegrity | array | 关键词完整度得分 |
| keysFluency | array | 关键词流利度 |
| standardScore | string | 客户定制，输出的分制，当前含有4分制和8分制 |
| StressOfSent | string | 句子重读，每个单词都输出，0：该单词没有被重读；1：该单词被重读 |
| StressOfWord | string | 单词重音，将用户发音和词典的重音位置做比较，0：该单词重音朗读错误；1：该单词重音朗读正确 |
| tone | array | 输出全部信息，数据可以用于画用户的发音曲线，目前只有内部在使用 |
| audiocheck | array | 音质检测结果。volume：音量过小的置信度；clipping：截幅的置信度；noise：噪音过大的置信度；cut:截断的置信度；too short：是否音频过短；emptyAudio：是否是空音频。<br>备注：置信度的值为0和10，10代表可能存在该项音质问题，0代表该项检测正常 |
