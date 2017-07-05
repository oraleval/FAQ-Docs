# 开放题型语法编写注意事项

* [置题工具](#tool-introduce)
* [JSGF/枚举语法编写注意事项](#JSGF)
* [口头作文语法编写注意事项](#retell)


### <a name="tool-introduce"></a> 置题工具



> 工具地址：http://101.231.106.182:5000/#/

> 工具帮助文档见工具界面：http://101.231.106.182:5000/#/help

> 半开放题型、口头作文题型的标准答案都可以使用置题工具进行编写，最终生成的语法有枚举类型、JSGF类型和retell类型

> 枚举类型在工具生成的Json结果中含有enumerate 标记，JSGF类型在Json结果中含有JSGF标记，口头作文类型在结果中含有en.exam.retell标记

 
 
### <a name="JSGF"></a> JSGF/枚举语法编写注意事项

> 一般固定答案采用枚举类型的语法，半开放题型采用枚举或是JSGF语法编写答案

#### 1.半开放题型介绍

> 举例，中考中的情景问题就是半开放题型

> 情景提示：李明最喜欢的学科是体育，他认为体育很有趣，下周五他要参加学校举行的篮球比赛

> 问题：What is LiMing's favorite subject?

> 这个问题的答案是有限的，但是有多种说法，所以可以认为是半开放题型


#### 2.语法编写规则

##### 2.1关键词以精简为原则

> 在置题工具中设置关键词时，关键词要求精简，尽量不要含有a、the、an 等常见冠词或量词

##### 2.2检查文本正确性

> 检查英文文本的正确性，文本中不要含有全角或是中文标点

##### 2.3检查语法的覆盖

> 句式覆盖全面能够保证学生回答只要在句式范围内都可以合理打分，如果句式覆盖不全，则可能导致学生说了正确的句式，但是整体打分低

> 句式中注意不要遗漏最简单的句式

> 例如where are you going，答案直接说bookstore的情况，如果答案中没有设定bookstore，学生这么说就会打分很低，实际这么说应该得高分

##### 2.4检查数字

> 语法中不能含有阿拉伯数字

##### 2.5检查关键字

> 句式中所包含的关键词必须跟定义的关键词匹配

> 例如定义的关键字是P E，句式中写的是pe，会导致关键字匹配不上，从而得分低

##### 2.6检查英文简称的写法

> 英文简称建议中间加个空格，可以使评分更加准确

> 例如NLP，可以写成N L P，因为有的缩略词可能是生词，分开写可以评分更加准确，当然一些常见的缩略词如PE确定在引擎词典中，不分开写也是可以的

##### 2.7检查变量和句式的编写

* **注意变量的个数**

>> 一个变量中的个数不宜太多，或者重复的变量不宜太多，否则算法在匹配的时候，可能因为都是同一个单词，在路径查找的时候，在是别的时候容易出现问题，例如：

>> <a> = my mom|my mother|my dad|my father|my uncle|my sister|my brother|my older sister|my younger sister|my older brother|my younger brother|my boyfriend|my girlfriend|my aunt|my cousin|my parents|my grandparents|my grandma|grandmother|granpa|grandfather|tom|mary|kelly|david|peter|john|nancy|lisa|steven|my friends|my friend tom|my friend mary|my friend kelly|my friend david|my friend peter|my friend john|my friend nancy|my friend lisa|my friend steven|classmates|my classmates|my best friend|some of my friends

>> 该变量中都存在my这个词，多了容易识别出错，可以去掉一些不必要的，例如my friend tom|my friend mary|my friend kelly|my friend david|my friend peter|my friend john|my friend nancy|my friend lisa|my friend steven

* **注意变量的有效性**

>> 在一些开放的问答题中，例如你平时的爱好是什么，这种答案不建议包含一些常用的国外的运动。例如<a> = (badminton|football|basketball|volleyball|tennis|table tennis|pingpong|baseball|pool|soccer|american football|golf|hockey
这里的soccer、american football和hockey都不是国内的主流运动，不容易被学生回答到，还增加了句式展开的个数，不建议添加

* **注意变量的常用性**

>> 当一个变量的值比较多时，建议通用类型的说法优先覆盖，减少不通用的说法，例如<b> = (usually|always|often|mostly|normally|in general|most of time，在跟句式结合的时候，normally|in general|most of time并不是最常用的一些说法，被学生说到的几率相对不多，但是多加了会影响整体的评分，建议不加

* **注意句式的简洁性**

>> 部分句式展开前半句基本都是重复的，例如以下句式：

>> <b>

>> <b> competition

>> i would like to <a> the <b>

>> i'd like to <a> the <b>

>> i would like to <a> the <b> at the sports meeting

>> i'd like to <a> the <b> at the sports meeting

>> i would like to <a> the <b> at the school sports meeting

>> i'd like to <a> the <b> at the school sports meeting

>> i would like to <a> the <b> competition

>> i'd like to <a> the <b> competition

>> i would like to <a> the <b> competition at the sports meeting

>> i would like to <a> the <b> competition at the school sports meeting

>> i'd like to <a> the <b> competition at the school sports meeting

>> 其中<a> = take part in|participate in

>> <b> = high jump|shot put|long jump|triple jump|discus throw|javelin|basketball|volleyball|table tennis|ping pong|tennis|football|soccer|swimming|hockey|badminton|running race|race|one hundred meter hurdles|four hundred meter hurdles|one hundred and ten meter hurdles|relay|relay race|four by one hundred meter relay|four by four hundred meter relay|sprint|five thousand meter run|five thousand meter race|one thousand and five hundred meter run|one thousand and five hundred meter race|one hundred meter dash|one hundred meter sprint|two hundred meter sprint|two hundred meter race|four hundred meter race|eight hundred

>> 所有的句式前半部分几乎都是i would like to <a> the <b>或i'd like to <a> the <b>，而展开后<b>这个句式占有的比率会非常低，所以直接说<b>这个句式会存在匹配不上的情况或是被匹配上的概率会非常低，此时建议精简句式，将以上重复的句式都去掉，留几个简洁的主流句式，如果学生多说，并且也是正确的，扣分不会很多，建议将以上句式精简为：

>> <b>

>> <b> <a>

>> <b> competition

>> i would like to <a> the <b>

>> i would like to <a> the <b> competition

>> i 'd like to <a> the <b> match

>> 精简的主要原则：覆盖最常用和最基本的说法，避免啰嗦的说法；这种情况下，如果学生多说了，也不会扣分很明显

* **注意句式的展开条数**

>> 句式展开后的条数不能超过2000条，这个置题工具可以检测。在不超出这个范围的前提下，精简更好

* **注意句式之间的平衡性**

>> 当句式比较多的时候，某个句式展开后非常多，而某些句式展开后会非常少，这样会导致比较少的句式在识别的时候，被识别的概率相对较小，所以建议补充一些无关句式，以使被匹配上的概率相对多一点，前提也是在展开后的条数在2000条以内，例如以下句式：

>> <b>

>> <b> competition

>> i would like to <a> the <b>

>> i would like to <a> the <b> competition

>> i would like to <a> the <b> at the school sports meeting

>> 其中<b>开头的句式会比较少，可以再额外补充一个<b>开头的句式（学生不会用到也没有关系），再精简一下 i 开头的句式，以使被匹配上的概率增加，变成如下：

>> <b>

>> <b> competition

>> <b> <a>

>> i would like to <a> the <b>

>> i would like to <a> the <b> competition



### <a name="retell"></a> 口头作文语法编写注意事项


#### 1.口头作文题型介绍

> 口语考试中的话题简述题型

> 给出几个要点，然后让学生按照要点进行口头描述，例如

> 1.今天是劳动节。早上，我和父母一起去购物

> 2.我和妈妈去服装店，买了一条裙子和一双鞋，爸爸去了超市，买了一些做晚餐要用的菜；

> 3.爸爸做了晚餐；

> 4.我们今天过的非常开心

#### 2.语法编写规则

> 以上4种场景，每种场景可能有好几种表达方式，如下做个列举：

> 场景1表达方式：A1     A2     A3

> 场景2表达方式：B1     B2     B3     B4

> 场景3表达方式：C1     C2

> 场景4表达方式：D1     D2     D3     D4     D5

> 最后的标准答案可以是场景最多的那个个数，标准答案可以列为{A1 B1 C1 D1},{A2 B2 C2 D2},{A3 B3 C1 D3},{A1 B4 C2 D4},{A2 B1 C2 D5}

