
## <a name=head></a> FAQ文档

* [评测服务支持哪些平台](#platform)
* [私有协议和HTTP协议调用评测的区别](#protocol-differences)
* [提供纯离线SDK吗](#provide-offline)
* [纯在线和离在线混合SDK的区别是什么](#online-diff-offline)
* [在线SDK的备份机制是什么](#backup)


#### <a name=platform></a> 评测服务支持哪些平台

* 按照操作系统划分
> 支持Android、iOS、Windows、linux

* 按照协议划分
> 支持基于socket的私有协议和HTTP/HTTPS两种协议。私有协议包含Android平台SDK，iOS平台SDK, flash 平台SDK，其他web端或是后端调用多数是使用http,支持微信小程序、微信公众号

* 按照支持的语言进行划分
> Android和ios源码；java；H5、PHP、JS等前端语言

* 还有哪些可以支持
> 除了私有协议只支持Android、iOS和flash外，其他平台或语言只要能够使用HTTP协议，都可以访问评测服务，例如基于unity或Windows平台开发的软件

#### <a name=protocol-differences></a> 私有协议和HTTP协议调用评测的区别

> 私有协议支持流式，实现时传时评，HTTP/HTTPS以文件方式上传评测

> 后端引擎处理一样，打分一样，就是服务前端的差异


#### <a name=provide-offline></a> 提供纯离线SDK吗？

> 我们提供离在线混合模式，不支持纯离线模式。离线的语音识别和口语评测在准确性、生词支持、算法更新上等有很多弱点，只是作为在线的补充。优先使用在线识别/评测，如果断网或者网络信号不好的情况下，给出离线识别/评测的结果。一般在线1s没有返回评测结果，就会给出离线评分


#### <a name=online-diff-offline></a> 纯在线和离在线混合SDK的区别是什么？

> 纯在线享受云端最新的评测服务，离在线混合SDK的在线也同样享受最新的评测服务

> 纯在线支持单词、句子、段落（16000字符）、选择题、半开放题型和口头作文等各种题型的评测；离线只支持单词、句子和段落的评测，不支持json格式的文本。

> 纯在线SDK有备份机制，离在线混合SDK没有备份机制


#### <a name=backup></a> 在线SDK的备份机制是什么？

> 目前SDK的备份流程有3层，每一层走不通时，都会向下一层去尝试网络连接以保证连接成功率

> 第一层：socket + 域名

> 第二层：socket + ip

> 第三层：http + ip
