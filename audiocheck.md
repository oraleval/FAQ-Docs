
#### API

```
{
  "OralConf": {
    "stress": true,
    "subject": "word",
    "point" :4
  },
  
  "AudioCheck": true,
  "DisplayText": "hello world",
  "X-EngineType": "",
  "EngineType":"",
  "ID": ""
}
```


// OralConf:是控制评测引擎的配置参数，其中stress字段，打开重音功能

// AudioCheck:字段， 打开音质检查功能(TODO:正在开发中)

// DisplayText: 送给引擎的文本

// X-EngineType:的值可以是oral.gendu,oral.zuowen

// EngineType是X-EngineType的别名(目前还没有实现)

// ID 内容管理服务需要的ID

#### 选项含义

* stress

值为true，打开重音功能，值false或不填，都不开启重音功能

* subject(TODO)

普通功能: 可以是word(单词),sentence(句子),chapter(篇章)

高级功能: subject:可以是选择题(select), 问答题(qa), 口头作文(composition), 检错纠错, 模仿评测(imitate)

point

分制: 现在支持4或者8分制两种情况

* AudioCheck

设置为true，打开音质检测功能，检测音量高，低，截幅，信噪比。分别是volume-low, volume-high, clipping, noise。
在引擎返回的json会多出audioCheck:"volume-low,noise" 类似字段。如果检测出多种情况，结果会用,号隔开。

#### 使用示例
* 使用point的示例
```
# cat point.json
{
    "OralConf": {
        "point":4
    },
    "DisplayText": "good"
}

http_addr="http://127.0.0.1:4986"
curl -X POST -H "session-id:`uuidgen`" -H "appkey:xxx" \
            -H "Content-Length"  \
            --form mode="a" --form text="`cat point.json`" --form voice=@./good.opus "$http_addr/eval/opus"
```

* 使用stress的示例
```
# cat stress.json
{
    "OralConf": {
        "stress":true
    },
    "DisplayText": "good"
}

curl -X POST -H "session-id:`uuidgen`" -H "appkey:xxx" \
            -H "Content-Length"  \
            --form mode="a" --form text="`cat stress.json`" --form voice=@./good.opus "$http_addr/eval/opus"
```
* 使用audioCheck的示例
```
# cat audiocheck.json 
{
    "AudioCheck":true,
    "DisplayText": "good"
}

curl -X POST -H "session-id:`uuidgen`" -H "appkey:xxx" \
            -H "Content-Length"  \
            --form mode="a" --form text="`cat audiocheck.json`" --form voice=@./good.opus "$http_addr/eval/$format"
            
# 这时候服务端返回的json会多出audioCheck字段,没有检测出异常音频，值为"ok"，也有可能为volume-low, volume-high, clipping, noise的一个或者多个，
# 多个值用 ","号隔开
{
  "lines": [
    {
      
    }
  ],
  "version": "full 1.0",
  "audioCheck": "volume-low"
}

```
