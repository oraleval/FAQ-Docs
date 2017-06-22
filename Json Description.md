### 评测返回结果中Json字段说明


| | | |
| ----- | ----- | ----- |
| 名称| 类型 | 说明 |
| version | string | 结果格式版本及版本号 |
| lines | array | 每行输入文本的评测结果 |
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
| text | string | 结果格式版本及版本号 | 词的字符串，使用"sil"表示语音中的静音段 |
| type | int | 类型，共有6种类型，分别是：0 多词；1 漏词；2 正常词；3 错误词；4 静音；5 重复词；8 生词 |
