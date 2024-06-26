# 极简阅读

**我们强烈建议用户仅在法律允许范围内和在相关权利人的明确授权下使用。 任何未经授权或超出法律许可范围的行为，由用户自行承担法律责任。**

极简阅读是一款去中心化的工具，支持苹果IOS和安卓。\
下载地址：<https://freenovel123.github.io/novel/html/index.html>

## 源制作文档

### 1、源参数说明

| 参数          | 名称        | 参数类型        | 是否必填 | 示例值                                   | 描述                    |
| :---------- | :-------- | :---------- | :--- | :------------------------------------ | :-------------------- |
| version     | 版本号       | Number      | 是    | 1                                     | 版本更新标记                |
| siteName    | 站点名称      | String      | 是    | 笔趣阁                                   | 站点的名称                 |
| baseUrl     | 站点根地址     | String      | 是    | <https://www.biqige.com/>             | url地址的末尾必须以/结尾        |
| author      | 作者        | String      | 否    | 张三                                    | 作者的名称                 |
| contact     | 作者联系方式    | String      | 否    | <123@qq.com>                          | 作者联系方式                |
| enable      | 启用状态      | Boolean     | 是    | true                                  | 是否使用该源                |
| tools       | 支持的工具     | Array       | 否    | \["vpn","more"]                       | 给源标记必须要使用的工具取值范围`vpn` |
| header      | 请求头       | JSON        | 否    | `{"Content-Type":"application/json"}` | 请求头                   |
| cookies     | 请求Cookies | JSON        | 否    | `{"token":"111222333"}`               | 请求的Cookies            |
| remarks     | 备注信息      | String      | 否    | 这是一个很好的源                              |                       |
| ruleSearch  | 搜索规则      | RuleSearch  | 是    | `{...}`                               | 具体查看1.1搜索规则说明         |
| ruleChapter | 章节列表规则    | RuleChapter | 是    | `{...}`                               | 具体查看1.2章节列表规则说明       |
| ruleContent | 正文规则      | RuleContent | 是    | `{...}`                               | 具体查看1.3正文规则说明         |

### 1.1、搜索规则说明

| 参数          | 名称     | 参数类型   | 是否必填 | 示例值                               | 描述                                                              |
| :---------- | :----- | :----- | :--- | :-------------------------------- | :-------------------------------------------------------------- |
| engine      | 解析引擎   | String | 是    | xpath                             | 取值范围`xpath,jsonpath`                                            |
| preRequests | 前置请求   | Array  | 否    | `[{...},{...}]`                   | 前置请求，具体参考1.5和2.8                                                |
| request     | 请求信息   | String | 否    | @js: return config;               | 在请求URL之前可以处理一些参数，比如添加请求头，替换请求url等。具体可以查看2.1.1                   |
| response    | 响应处理   | String | 否    | @js: return html;                 | 在请求完成以后，会将请求到的html返回到这里，可以根据需求处理。具体可以查看2.2                      |
| url         | 搜索地址   | String | 是    | <https://www.a.com/search/>       | 站点的搜索地址                                                         |
| method      | 请求方式   | String | 是    | GET                               | 取值范围`GET,POST`                                                  |
| params      | 请求参数   | JSON   | 是    | `{"name":"{keyword}","type":"0"}` | 参数中的{keyword}是搜索中的关键字，比如搜索”三国演义“，那么在实际请求中"{keyword}"会被替换成"三国演义" |
| encode      | 编码方式   | String | 是    | utf-8                             | 取值范围`utf-8,gbk,gb2312`，默认认为utf-8                                |
| bookList    | 搜索列表规则 | String | 是    | //\*\[@class\='list']             | 规则代码                                                            |
| bookName    | 书籍名称规则 | String | 是    | .//a/text()                       | 这里的取值方式是获取bookList中的Dom或者JSON                                   |
| bookUrl     | 书籍地址规则 | String | 是    | .//a/@href                        | 同上                                                              |
| bookAuthor  | 书籍作者规则 | String | 否    | .//p\[@\='author']/text()         | 同上                                                              |
| ruleExtra   | 追加的规则  | JSON   | 否    | `{...}`                           | 具体查看1.4追加规则说明                                                   |

### 1.2、章节列表规则说明

| 参数          | 名称     | 参数类型   | 是否必填 | 示例值                                                                                                                            | 描述                                            |
| :---------- | :----- | :----- | :--- | :----------------------------------------------------------------------------------------------------------------------------- | :-------------------------------------------- |
| engine      | 解析引擎   | String | 是    | jsonpath                                                                                                                       | 取值范围`xpath,jsonpath`                          |
| preRequests | 前置请求   | Array  | 否    | `[{...},{...}]`                                                                                                                | 前置请求，具体参考1.5和2.8                              |
| request     | 请求信息   | String | 否    | @js: return config;                                                                                                            | 在请求URL之前可以处理一些参数，比如添加请求头，替换请求url等。具体可以查看2.1.2 |
| response    | 响应处理   | String | 否    | @js: return html;                                                                                                              | 在请求完成以后，会将请求到的html返回到这里，可以根据需求处理。具体可以查看2.2    |
| encode      | 编码方式   | String | 是    | utf-8                                                                                                                          | 取值范围`utf-8,gbk,gb2312`，默认认为utf-8              |
| list        | 章节列表规则 | String | 是    | \$..chapterlist\[\*]                                                                                                           | 规则代码                                          |
| name        | 章节名称规则 | String | 是    | chapterName                                                                                                                    | 这里的取值方式是获取list中的Dom或者JSON                     |
| url         | 章节地址规则 | String | 是    | [http://www.a.com/?bid\=\\{{bookId\\}}\&cid\=\\{{chapterId>\\}}](http://www.a.com/?bid=\\{{bookId\\}}\&cid=\\{{chapterId>\\}}) | 这里的取值方式是获取list中的Dom或者JSON                     |
| ruleExtra   | 追加的规则  | JSON   | 否    | `{...}`                                                                                                                        | 具体查看1.4追加规则说明                                 |

### 1.3、正文规则说明

| 参数          | 名称      | 参数类型   | 是否必填 | 示例值                            | 描述                                                                                       |
| :---------- | :------ | :----- | :--- | :----------------------------- | :--------------------------------------------------------------------------------------- |
| engine      | 解析引擎    | String | 是    | jsonpath                       | 取值范围`xpath,jsonpath`                                                                     |
| preRequests | 前置请求    | Array  | 否    | `[{...},{...}]`                | 前置请求，具体参考1.5和2.8                                                                         |
| request     | 请求信息    | String | 否    | @js: return config;            | 在请求URL之前可以处理一些参数，比如添加请求头，替换请求url等。。具体可以查看2.1.3                                           |
| response    | 响应处理    | String | 否    | @js: return html;              | 在请求完成以后，会将请求到的html返回到这里，可以根据需求处理。具体可以查看2.2                                               |
| page        | 正文总页数规则 | String | 否    | \$.data.page或者使用整数10           | 文章多页的情况下使用该规则进行获取下一页内容，那么使用这个参数必须配合pageStart和chapterUrl可以将恢复成一篇完整的文章，与next二选一，同时存在优先page |
| next        | 下一页规则   | String | 否    | //\*\[contains(.,"下一页")]/@href | 文章多页的情况下使用该规则进行获取下一页内容，因为是单线程操作，访问速度相对page多线程效率更慢，与page二选一，同时存在优先page                    |
| encode      | 编码方式    | String | 是    | utf-8                          | 取值范围`utf-8,gbk,gb2312`，默认认为utf-8                                                         |
| lines       | 正文规则    | String | 是    | \$.data.content                | 规则代码                                                                                     |
| cleaner     | 净化规则    | String | 否    | 你好\|张三\|李四                     | 净化文章中一些广告内容，多个使用"\|"分割                                                                   |

### 1.4、追加规则说明

| 参数              | 名称        | 参数类型   | 是否必填 | 示例值        | 描述 |
| :-------------- | :-------- | :----- | :--- | :--------- | :- |
| imageUrl        | 封面地址规则    | String | 否    | pic        |    |
| lastUpdateTime  | 最后更新的时间规则 | String | 否    | updateTime |    |
| lastChapterName | 最新的章节名称规则 | String | 否    | lastName   |    |
| introduce       | 书籍介绍规则    | String | 否    | intro      |    |
| classify        | 书籍分类规则    | String | 否    | category   |    |
| status          | 书籍完结状态规则  | String | 否    | status     |    |

### 1.5、前置请求参数说明

| 参数       | 名称   | 参数类型   | 是否必填 | 示例值                                           | 描述                               |
| :------- | :--- | :----- | :--- | :-------------------------------------------- | :------------------------------- |
| url      | 请求地址 | String | 是    | <http://www.com>                              | 请求地址                             |
| params   | 请求参数 | JSON   | 否    | {"keyword":"@get{keyword}"}                   | 参数                               |
| method   | 请求方式 | String | 是    | POST                                          | 取值范围`GET,POST`                   |
| encode   | 编码方式 | String | 是    | utf-8                                         | 取值范围`utf-8,gbk,gb2312`，默认认为utf-8 |
| response | 响应内容 | JSON   | 否    | {"engine":"jsonpath","put":{"key":"\$.data"}} | 分为2个参数engine和put，put说明请参考2.8     |

### 2、源规则中特定字段参数的说明

2.1、`request`，这个参数暂时只支持`@js:`的写法，也就说这个参数暂时是一个写js方法的参数。示例：

`@js: config['url'] = config.url.concat('more'); config['header'] = {'X-Requested-With':'XMLHttpRequest'}; return config;`&#x20;

以上就是一个完整的`request`示例写法，方法的最后必须将config对象return

这里有一个特定的对象`config`，其中包含了一些常用的参数，不同的规则中参数是有区别的。

> 注意：在JS中如果是两个字符串连接请使用concat()方法，不要使用“+”。

2.1.1 搜索规则config的参数说明：

| 参数名     | 获取方式           | 示例值                           | 描述                    |
| :------ | :------------- | :---------------------------- | :-------------------- |
| host    | config.host    | <http://www.a.com/>           | 站点地址                  |
| url     | config.url     | <http://www.a.com/search/>    | 请求地址，搜索地址/章节列表地址/正文地址 |
| header  | config.header  | {"a":"b"}                     | 请求头                   |
| cookies | config.cookies | {"a":"b"}                     | 请求cookies             |
| params  | config.params  | {"keyword":"搜索内容","type":"0"} | 请求参数                  |
| keyword | config.keyword | 搜索内容                          | 请求的关键字                |

2.1.2 章节列表规则config的参数说明：

| 参数名                     | 获取方式            | 示例值                       | 描述                                             |
| :---------------------- | :-------------- | :------------------------ | :--------------------------------------------- |
| host,url,header,cookies |                 |                           | 具体查看2.1.1                                      |
| bookName                | config.bookName | 三国演义                      | 书籍名称                                           |
| bookUrl                 | config.bookUrl  | <http://www.a.com/1.html> | 书籍章节列表初始地址，主要用途是在JS和\${bookUrl}的用法，不支持修改，不参与请求 |

2.1.3 正文规则config的参数说明：

| 参数名                     | 获取方式               | 示例值                         | 描述                                                                 |
| :---------------------- | :----------------- | :-------------------------- | :----------------------------------------------------------------- |
| host,url,header,cookies |                    |                             | 具体查看2.1.1                                                          |
| pageStart               | config.pageStart   | 2                           | 页面规则起始数，配合page参数可将多页数据整合为一个完整的数据                                   |
| chapterName             | config.chapterName | 第一章                         | 章节名称                                                               |
| chapterUrl              | config.chapterUrl  | <http://www.a.com/1/1/html> | 章节内容初始地址，主要用途是在JS和\${chapterUrl}的用法，在正文多页的情况配合page和pageStart参与规则处理 |

2.2、response，这个参数暂时只支持`@js:`的写法，也就说这个参数暂时是一个写js方法的参数。示例：

`@js: html = html.replace(/|<\/dd>|[\s\S]*?<\/dt>/g, ''); html = '<div class="list">'.concat(html).concat(''); return html;`

以上就是一个完整的`response`示例写法，方法的最后必须将`html`参数`return`

这里有两个特定的参数`html`和`config`，`html`参数代表了没任何处理的响应信息，`config`参数可以参考`2、源规则中特定字段参数的说明`。

2.3、在规则中使用{{}}和\${}的方式进行替换

> {{xxx}}代表xxx是一个xpath或者jsonpath的规则
>
> \${xxx}代表xxx是一个常用的参数，参数请参考 2.源规则中特定字段参数的说明

比如规则为 `${bookUrl}/b/\{{.//@href\}}` ，`${bookUrl}`会替换为书本的详情地址，`\{{.//@href\}}`会根据xpath获取对应信息，最后会得到一个完整的链接比如 <http://www.a.com/111/b/a.html>

2.4、在规则中使用\<js>\</js>方法

> 比如一个xpath规则获取书本名称“三国演义”，然后想将三国演义这个名称修改为“三国演义真好看”，那么只需要将规则这么写：
>
> //\*\[@class\="bookName"]/text()\<js>value \= value.concat('真好看'); return value;\</js>
>
> 程序会先处理xpath部分，然后将处理完成获取到的数据给到value,然后可以在js中处理，这里也支持config参数。

2.5、在规则中使用@put{}和@get{}的方法（IOS`2.1`以上版本，安卓`2.1`以上版本支持）

> @put{} 将一个规则获取到的内容存入临时内存中
>
> @get{} 获取@put{}存入的数据
>
> 比如：@put{//\*\[@class\='name']/text()#name}，这里的意思是将规则//\*\[@class\='name']/text()中获取到的值给到名称为name的参数，那么可以在其他规则中使用@get{name}即可获取相应的值，也可以使用@get{\$.name}，因为@get{}中的内容是一个`Jsonpath`规则

2.6、在JS中支持CryptoJS加密库，支持`Hash`、`AES`、`MD5`、`Base64`、`SHA-1`、`SHA-256`、`DES`、`PBKDF2`等方法。

> MD5：CryptoJS.MD5(data).toString();
>
> AES：CryptoJS.AES.decrypt(data, password, {iv: iv, padding: CryptoJS.pad.Pkcs7 }).toString(CryptoJS.enc.Utf8)};
>
> Base64：CryptoJS.enc.Utf8.parse(data).toString(CryptoJS.enc.Base64);

2.7、正文多页说明

在某些源中正文会被切割成多个页面，极简提供了多个方案可以准确的将多个页面恢复成一篇完整的文章。

示例一：使用request和page多线程请求方案

`章节内容第一页url地址为：https://www.xxx.com/book/160/313848.html`

`章节内容第二页url地址为：https://www.xxx.com/book/160/313848_2.html`

在正文规则中可以按照以下方式来设置规则

请求信息(request)：`@js: config['chapterUrl'] = config.chapterUrl.replace('.html', '').concat('_${i}.html'); config['pageStart'] = 2; return config;`

页面数量(page)：`//*[@class='bookname']/text()<js>var v = value.match(/\/(\d+)）/); return v[1];</js>`

页面数量这里是可以使用2个方案，方案一可为规则，方案二可以是整数，比如10，在第一页中能准确知道这个文章被分成几页的情况下，请使用规则。如果不能准确知道文章被分成多少页数，可以设置一个请求最大值。

示例二：使用next方案

该方案为单线程方案，也就是如果一个文章被分成了10页，那么极简会按照顺序请求页面，直到找不到下一页的内容。

下一页规则(next)：`//*[contains(.,"下一页")]/@href`

此方案对于规则的编写方面比较简单，但是没有示例一的请求效率高。极简在此方案中规定了最多请求50页，如果不满足的情况请选择方案一

2.8、前置请求

在搜索规则、章节列表、正文规则中都有个一个preRequests参数，该参数主要是用于比如搜索前，需要获取一些数据或者搜索页面每天都会变化的情况下使用。preRequests是一个数组，原则上可以无限进行请求。

> preRequests中put的参数等同于@put{}

\
最后如果有不懂的同学可以加qq群学习交流：593371452
