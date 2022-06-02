苏州大学传媒学院 王汇森<br />联系方式：w1227686341（微信） 18896978797（电话）
<a name="cVGeB"></a>

## 流程概述

主要包含两个部分：获取推文和社交机器人身份鉴定
<a name="p1Lnt"></a>

### 获取推文数据

1. 确定数据范围（获取推文的关键词、推文类型、推文语言、时间范围、数据字段等等）

2. 调整Python脚本参数

3. 调用脚本（注意脚本中断问题）

4. 数据清洗（注意字符编码问题）
   <a name="aaSSU"></a>
   
   ### 社交机器人检测

5. 输入推文文档

6. 将推文作者ID输入脚本

7. 调用Botomter API（注意请求速率）

8. 返回该用户检测结果
   <a name="GsQFl"></a>
   
   ## 开发环境准备
   
   至少需要达到以下环境要求：
- Python 3.7+
- Jupyter Notebook（首选）/Visual Studio Code（配置了Jupyter环境）
- 访问国际互联网的工具👀

Python学习资源推荐（别买课，Python学习资源多如牛毛）：

- 廖雪峰的官网：[https://www.liaoxuefeng.com/](https://www.liaoxuefeng.com/)（入门强推，非常适合初学者）

- 骆昊的教程：[https://github.com/jackfrued/Python-100-Days](https://github.com/jackfrued/Python-100-Days)（进阶教程，全面且困难）

- 崔庆才的博客：[https://cuiqingcai.com/about/](https://cuiqingcai.com/about/)（爬虫方向，博主是帅锅）

- 《动手学深度学习》网页版：[https://zh-v2.d2l.ai/index.html](https://zh-v2.d2l.ai/index.html)（深度学习方向，书是好书，但是深度学习本身很难）

- Jack Cui的博客：[https://cuijiahua.com/](https://cuijiahua.com/)（人工智能应用，图一乐还是真操作都值得一看）
  <a name="Cj5TA"></a>
  
  ### Python环境配置
  
  Python官网提供了下载入口，选择3.7及以上版本安装。记得根据操作系统选择安装（mac系统内置了Python2，但并不兼容本项目代码！），此处以WIN系统为例，访问如下网站可以选择合适的版本进行下载：<br />[https://www.python.org/downloads/windows/](https://www.python.org/downloads/windows/)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654096651113-443de80c-9a08-4a3f-b91b-8d34e7befbda.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=758&id=ufbe1d2ce&margin=%5Bobject%20Object%5D&name=image.png&originHeight=947&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=277258&status=done&style=none&taskId=u833678af-26fb-472b-b191-c844773387e&title=&width=1536)<br />左侧为稳定版，右侧为开发版，功能新但是不一定稳定，可能出bug。<br />这里选择稳定版的Python3.9.13，选择Windows installer（64bit）下载。<br />进入安装后，勾选上“Add Python 3.9 to PATH”，然后直接“Install Now”即可快速安装。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654096998964-67f6d449-df25-4ad9-917e-4e92b7924c02.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=408&id=u523f3444&margin=%5Bobject%20Object%5D&name=image.png&originHeight=510&originWidth=830&originalType=binary&ratio=1&rotation=0&showTitle=false&size=146830&status=done&style=none&taskId=u0b799638-e570-485d-8f74-a9e879ae0f9&title=&width=664)<br />注意，一定要将Python添加到环境变量，因为在使用过程中会大量调用命令行工具（即CMD，按一下键盘的WIN键再输入cmd按一下enter即可打开命令行工具）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654097294243-e11ac967-a7eb-4cf8-87d8-f997af1b5b59.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=506&id=u6299d1e7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=632&originWidth=1223&originalType=binary&ratio=1&rotation=0&showTitle=false&size=15701&status=done&style=none&taskId=u1272226a-9b72-42ab-9e16-95fcf53439c&title=&width=978.4)<br />如果顺利安装并且配置好了环境变量，在命令行输入python即可进入python的命令行开发模式：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654097409974-5ef41614-d08a-4349-be09-5a6f51dea2a8.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=504&id=u38e45583&margin=%5Bobject%20Object%5D&name=image.png&originHeight=630&originWidth=1219&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29412&status=done&style=none&taskId=u7eee53bf-de46-4e43-8a2b-20eff6d647d&title=&width=975.2)<br />在命令行模式写代码是一件非常低效的事，因为只能输入一行执行一行，并不利于连贯的代码逻辑的表示。为此，我们通常使用一些IDE（Integrated development environment，开发集成环境，可以理解为一个集成了软件开发中所需的编程语言运行环境、代码编辑器、插件、调试工具等功能的一套综合的开发环境）进行开发。<br />Pycharm无疑是业界公认最强Python的IDE，官网可以下载免费版：<br />[https://www.jetbrains.com/pycharm/download/#section=windows](https://www.jetbrains.com/pycharm/download/#section=windows)<br />个人倾向于使用VS Code（不解释，VS Code天下第一），功能极其强大，插件多如牛毛，几乎兼容所有编程语言（插件花样百出，甚至可以摸鱼），而且纯免费，但是配置稍微复杂，有兴趣可以参考以下文章进行Vscode配置：<br />[https://zhuanlan.zhihu.com/p/342873841](https://zhuanlan.zhihu.com/p/342873841)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654098167123-e03fbfde-0a6f-4fce-a9f5-bd642841d2d2.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=824&id=u15c730aa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1030&originWidth=1919&originalType=binary&ratio=1&rotation=0&showTitle=false&size=161276&status=done&style=none&taskId=u45c3b56c-2aee-49ad-b4c0-e9ac296c2ea&title=&width=1535.2)
  <a name="JYnVM"></a>
  
  ### Jupyter环境安装
  
  前面两个IDE都是桌面软件，且功能复杂、配置繁琐。Jupyter就是一个非常好的工具，它能够直接使得我们能够在网页中进行代码编辑，随用随退，功能精简。<br />Jupyter可以通过pip安装。pip是Python预置的下载工具，Python社区活跃，有大量开发者每天无偿将自己编写的代码包贡献给Python，有了大量无私的程序员，才有今天的Python。用pip可以免费下载这些代码包。<br />首先，测试一下电脑是否配置好了pip，在cmd中输入“pip”，弹出如下内容即证明配置良好：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654099297491-f26ad9b6-872b-492a-b72d-0d9a18dfc8b8.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=510&id=u14fd84ce&margin=%5Bobject%20Object%5D&name=image.png&originHeight=638&originWidth=1218&originalType=binary&ratio=1&rotation=0&showTitle=false&size=70369&status=done&style=none&taskId=u0d6cee24-f734-4e0c-b0a8-b8ab908bf1e&title=&width=974.4)<br />pip命令很多，最常用的是'intsall'，安装jupyter很简单，输入：
  
  ```
  pip install jupyter
  ```
  
  ![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654099708858-5724e3e1-063c-4c93-83f9-07506bdd0ac6.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=509&id=u59643bee&margin=%5Bobject%20Object%5D&name=image.png&originHeight=636&originWidth=1219&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122393&status=done&style=none&taskId=uc561567a-3109-4dd0-b8ed-f0c4720a2d1&title=&width=975.2)<br />不出意料，将会进入一段漫长的下载阶段。这是因为pip的源服务器在境外，加上每天大量用户使用，其传输速度堪忧。好消息是国内许多高校和公司都建立了自己的镜像平台。<br />我们可以手动配置pip下载的地址，在cmd输入：
  
  ```
  pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
  ```
  
  这里使用的是清华大学提供的镜像，还有很多，替代相应链接即可：

- 豆瓣：[http://pypi.douban.com/simple/](http://pypi.douban.com/simple/)

- 中科大：[https://pypi.mirrors.ustc.edu.cn/simple/](https://pypi.mirrors.ustc.edu.cn/simple/)

- 阿里云：[https://mirrors.aliyun.com/pypi/simple/](https://mirrors.aliyun.com/pypi/simple/)

安装完Jupyter后，在命令行输入'jupyter notebook'，如果不行就用'jupyter-notebook'试试：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654100494132-6a41fd67-d0b6-4d57-9997-a5f401d055bf.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=498&id=udc999a58&margin=%5Bobject%20Object%5D&name=image.png&originHeight=622&originWidth=1220&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63980&status=done&style=none&taskId=u2ee04853-f850-4ae6-b85a-66fa1f12d92&title=&width=976)<br />随后命令行会自动搭建Jupyter本地服务器，浏览器会自动弹出，界面如图所示：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654100619889-e279309a-1355-4ab1-9ae2-8a25cad6eb0c.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=824&id=u6a3e12fa&margin=%5Bobject%20Object%5D&name=image.png&originHeight=1030&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57866&status=done&style=none&taskId=u81e9d5b7-88e7-434a-8400-41313648052&title=&width=1536)<br />这样就代表整个环境运行正常，可以进行后后续操作了，我们创建一个jupyter文件。（注意，jupyter的格式为ipynb，而python官方指定的后缀为py，需要区别的是，jupyter要执行py代码需要创建一个新的ipynb文件，将py代码复制粘贴进去再运行）<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654100912771-5490a314-d517-40b9-93f7-04877901ceb5.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=269&id=ue00c0ccb&margin=%5Bobject%20Object%5D&name=image.png&originHeight=336&originWidth=264&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19115&status=done&style=none&taskId=ubdd76b54-e1f1-4817-b361-bc107f16f14&title=&width=211.2)<br />我们随便在新建的jupyter记事本当中输入两段段代码，点击运行即可，你会发现，Jupyter是一行一行，即时反馈运行结果的，这样就为代码的调试带来了巨大优势，这也是我常使用jupyter的Python的原因，用vscode只能一次性执行完所有代码，选到哪行执行哪里，非常灵活。<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654100980114-24771034-3e0a-441b-ac02-96f7b276e6f4.png#clientId=u542d8cd2-b863-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=750&id=ufc33c415&margin=%5Bobject%20Object%5D&name=image.png&originHeight=938&originWidth=1920&originalType=binary&ratio=1&rotation=0&showTitle=false&size=64708&status=done&style=none&taskId=ubf111cd6-d516-438c-94c4-ac5ceb84d87&title=&width=1536)<br />至此，基础的开发环境已经安装完毕了。
<a name="JfUn4"></a>

### 进入国际互联网

后面调用Twitter API是一定需要使用国际互联网的，如果你还不会科学上网请咨询你的亲朋好友。~~这里也不提供方法：~~<br />~~Clash：~~[~~https://wwe.lanzoup.com/b01u2exxe~~](https://wwe.lanzoup.com/b01u2exxe)~~（5252）~~<br />~~订阅链接：~~[~~https://openit.ml/Clash.yaml~~](https://openit.ml/Clash.yaml)
<a name="Drg9x"></a>

## 获取推特数据

获取Twitter数据较为简单，并不需要单独编写爬虫，Twitter官方提供了接口，供开发者调用以获取推特数据（学术版请查看Twitter API v2）。<br />Twitter API官方文档：[https://developer.twitter.com/en/docs/twitter-api](https://developer.twitter.com/en/docs/twitter-api)<br />类似的，微博也有官方提供的数据分发平台。<br />微热点：[https://www.wrd.cn/login.shtml](https://www.wrd.cn/login.shtml)
<a name="DAUUD"></a>

### 准备

- Twitter  API学术版
- 必要的Python依赖库（requests、pandas、datetime、unicodedata等）
- 梯子

这里需要着重强调一下Twitter API，理论而言，我们可以按照Twitter API官网的要求按需求申请即可。但在实际操作中并不理想，不知道是由于IP地址的原因还是针对中国大陆用户，Twitter屡次拒绝我的申请（也许只是学术版Twitter API申请特别难？）。最关键的是，一旦一个Twitter账号申请被拒后，就再也不能申请了。最后转而找到一个申请成功的博主并租用其API（有需要可以联系，微信gggs1024，非广告）。这里建议大家联系自己海外留学的朋友代为自己申请，可能会容易的多。<br />依赖库安装很简单，直接'pip install xxx'即可。梯子不解释。
<a name="SzNYK"></a>

### 脚本解释

调用Twitter API需要我们编写一个Python脚本，脚本的核心功能无非就是用Python创建HTTP请求，得到响应数据并进行一定的格式化并保存在本地。<br />这里提供一个我先前编写的一个脚本，并对其进行简要的说明。
<a name="jlWeU"></a>

#### Python库依赖

```python
# 依赖库，按照所列，pip安装即可
import requests
import os
import json
import pandas as pd
import csv
import datetime
import dateutil.parser
import unicodedata
import time
```

<a name="GBLgQ"></a>

#### 函数解释

脚本使用了函数式编程的基本思想，将核心功能抽离出来，编写为功能单一的函数，以便于后期调用，同时便于理解。

```python
# 返回Twitter API密钥（需要学术版）
def auth(token):
    return token

# 创建HTTP请求头
def create_headers(bearer_token):
    headers = {"Authorization": "Bearer {}".format(bearer_token)}
    return headers

# 创建请求地址
def create_url(keyword, start_date, end_date, max_results = 10):

    # 所调用的Twitter API终端，根据需求而定，详见Twitter API官方文档
    search_url = "https://api.twitter.com/2/tweets/search/all" 

    # 请求参数，此处需要根据自己需求调整，详见Twitter API官方文档
    query_params = {'query': keyword, # 查询关键词
                    'start_time': start_date, # 开始日期
                    'end_time': end_date, # 结束日期
                    'max_results': max_results, # 请求数量
                    'expansions': 'author_id,in_reply_to_user_id,geo.place_id', # 拓展信息
                    'tweet.fields': 'id,text,author_id,in_reply_to_user_id,geo,conversation_id,created_at,lang,public_metrics,referenced_tweets,reply_settings,source', # 推文信息字段
                    'user.fields': 'id,name,username,created_at,description,entities,location,pinned_tweet_id,profile_image_url,protected,public_metrics,verified,url,withheld', # 用户信息字段
                    'place.fields': 'full_name,id,country,country_code,geo,name,place_type', # 地理信息字段
                    'next_token': {} # 下一阶段的密钥，因为一次请求并不能返回所有推文，所有每次请求带上next_token即可接续上次查询的位置，按顺序得到所需推文
                   }

    return (search_url, query_params)

# 发起请求，返回调用结果
def connect_to_endpoint(url, headers, params, next_token = None):
    params['next_token'] = next_token   #params object received from create_url function
    response = requests.request("GET", url, headers = headers, params = params)
    print("Endpoint Response Code: " + str(response.status_code))
    if response.status_code != 200:
        raise Exception(response.status_code, response.text)
        return response.json()

    # 将结果添加到本地csv
    def append_to_csv(json_response, fileName, count): # 传参为connect_to_endpoint所返回的结果，以及保存路径还有计数器

        # 计数变量，不用管
        counter = 0

        # 打开csv文件文件并准备写入
        csvFile = open(fileName, "a", newline="", encoding='utf-8')
        csvWriter = csv.writer(csvFile)

        # 遍历请求反返回的数据。返回数据为JSON类型
        for i in range(len(json_response['data'])):
            # 每条tweet和user
            tweet = json_response['data'][i]
            for item in json_response['includes']['users']:
                if item['id'] == tweet['author_id']:
                    user = item
                    break
                    # 解析JSON，即提取出我们所需的字段
                    tweet_id = tweet['id'] if tweet['id'] else 'None'
                    text = tweet['text']+ ' ' if tweet['text'] else 'None'
                    author_id = tweet['author_id'] if tweet['author_id'] else 'None'
                    name = user['name']+ ' ' if user['name'] else 'None'
                    username = user['username']+ ' ' if user['username'] else 'None'
                    if ('in_reply_to_user_id' in tweet):   
                        in_reply_to_user_id = tweet['in_reply_to_user_id']
                    else:
                        in_reply_to_user_id = "None"
                        if ('geo' in tweet):   
                            geo = tweet['geo']['place_id']
                        else:
                            geo = "None"
                            if ('conversation_id' in tweet):   
                                conversation_id = tweet['conversation_id']
                            else:
                                conversation_id = "None"
                                created_at = tweet['created_at'] if tweet['created_at'] else 'None'
                                lang = tweet['lang'] if tweet['lang'] else 'None'
                                like_count = tweet['public_metrics']['like_count'] if tweet['public_metrics']['like_count'] else 0
                                quote_count = tweet['public_metrics']['quote_count'] if tweet['public_metrics']['quote_count'] else 0
                                reply_count = tweet['public_metrics']['reply_count'] if tweet['public_metrics']['reply_count'] else 0
                                retweet_count = tweet['public_metrics']['retweet_count'] if tweet['public_metrics']['retweet_count'] else 0
                                if ('referenced_tweets' in tweet):
                                    referenced_tweets_id = tweet['referenced_tweets'][0]['id']
                                    tweet_type = tweet['referenced_tweets'][0]['type']
                                else:
                                    referenced_tweets_id = 'None'
                                    tweet_type = 'origin'          
                                    reply_settings = tweet['reply_settings'] if tweet['reply_settings'] else 'None'
                                    source = tweet['source'] if tweet['source'] else 'None'
                                    user_created_at = user['created_at'] if user['created_at'] else 'None'
                                    description = user['description']+ ' ' if user['description'] else 'None'
                                    if ('location' in user):
                                        location = user['location'] + ' '
                                    else:
                                        location = "None"        
                                        if ('profile_image_url' in user):   
                                            profile_image_url = user['profile_image_url']
                                        else:
                                            profile_image_url = "None"
                                            protected = user['protected'] if user['protected'] else 'False'
                                            followers_count = user['public_metrics']['followers_count'] if user['public_metrics']['followers_count'] else 0
                                            following_count = user['public_metrics']['following_count'] if user['public_metrics']['following_count'] else 0
                                            listed_count = user['public_metrics']['listed_count'] if user['public_metrics']['listed_count'] else 0
                                            tweet_count = user['public_metrics']['tweet_count'] if user['public_metrics']['tweet_count'] else 0
                                            verified = user['verified'] if user['verified'] else 'False'
                                            url = user['url'] if user['url'] else 'None'

                                            # 将提取的字段数据合并为一行
                                            res = [tweet_id,text,author_id,name,username,in_reply_to_user_id,geo,conversation_id,created_at,lang,like_count,quote_count,reply_count,retweet_count,referenced_tweets_id,tweet_type,reply_settings,source,
                                                   user_created_at,description,location,profile_image_url,protected,followers_count,following_count,listed_count,tweet_count,verified,url]

                                            # 写入到csv文件当中
                                            csvWriter.writerow(res)
                                            counter += 1

                                            # 关闭文件写入
                                            csvFile.close()

    # 输出本次请求所添加的推文数量
    print("# of Tweets added from this response: ", counter) 
```

<a name="gAxyA"></a>

#### 参数解释

```python
# 参数填写

# 获取api密钥
bearer_token = auth('AAAAAAAAAAAAAAAAAAAAABxIRQEAAAAAL7fzqTTYXbPyMEQRVjxkHx3VCRk%3DzsMFUXwoFFHb5vBoVvxIcLRsekLpjGmk1kr5DTRejmBCzPXv5Z')
# 创建HTTP请求头
headers = create_headers(bearer_token)
# 查询语句(很重要)，Twitter API官方文档有一套专门的查询语言：
keyword = "#Tencent OR #Alibaba OR #Huawei OR #ByteDance OR #CATL lang:en"
# 查询的日期，这里注意，start_list和end_list为一对一的关系，即2018-12-07T11:43:04.000Z到2019-01-06T00:00:00.000Z为一个查询区间，以此类推
start_list =    [
                 '2018-12-07T11:43:04.000Z',
                 '2019-01-13T00:00:00.000Z',
                 '2020-05-17T00:00:00.000Z',
                 '2021-01-01T00:00:00.000Z'
                ]

end_list =      [
                 '2019-01-06T00:00:00.000Z',
                 '2019-02-10T00:00:00.000Z',
                 '2020-05-31T00:00:00.000Z',
                 '2021-07-05T00:00:00.000Z'
                ]
# 单次请求的最大推文数量
max_results = 400
# 计数变量，统计所有推文数量，不用管
total_tweets = 0

# 创建文件并准备写入，请使用csv格式
csvFile = open("data2.csv", "a", newline="", encoding='utf-8-sig') # 此处填写路径
csvWriter = csv.writer(csvFile)

# 输入表格头
csvWriter.writerow(['tweet_id','text','author_id','name','username','in_reply_to_user_id','geo','conversation_id','created_at','lang','like_count','quote_count','reply_count','retweet_count','referenced_tweets_id','tweet_type','reply_settings','source',
                'user_created_at','description','location','profile_image_url','protected','followers_count','following_count','listed_count','tweet_count','verified','url'
                ])
csvFile.close()
```

<a name="YQ0on"></a>

#### 调用流程

```python
# 执行部分

# 遍历日期
for i in range(0,len(start_list)):

    # 参数
    count = 0 # 记录数量的变量
    flag = True # 判断是否结束的变量
    next_token = None # 下一轮调用的密钥，前面已经解释过了
    counter = 0 # 记录第几次请求的变量

    # 判断是否获取结束，未结束则一直循环执行
    while flag:
        print("-------------------")
        print("Token: ", next_token)
        url = create_url(keyword, start_list[i],end_list[i], max_results)
        json_response = connect_to_endpoint(url[0], headers, url[1], next_token)
        tempStr = json.dumps(json_response)
        f = open(f'./archive1/{count}new_json{counter}.json', 'w') # 原始数据备份，以免意外
        f.write(tempStr)
        f.close()
        result_count = json_response['meta']['result_count']

        # 存在next_token说明还没获取完
        if 'next_token' in json_response['meta']:
            # 保存好next_token
            next_token = json_response['meta']['next_token']
            print("Next Token: ", next_token)
            if result_count is not None and result_count > 0 and next_token is not None:
                print("Start Date: ", start_list[i])
                append_to_csv(json_response, "data2.csv", count) # 写入csv文件
                count += result_count
                total_tweets += result_count
                print("Total # of Tweets added: ", total_tweets)
                print("-------------------")
                time.sleep(5) # 暂停几秒，以免超出速率限制   

        # 不存在next_token说明获取完了
        else:
            if result_count is not None and result_count > 0:
                print("-------------------")
                print("Start Date: ", start_list[i])
                append_to_csv(json_response, "data2.csv", count)
                count += result_count
                total_tweets += result_count
                print("Total # of Tweets added: ", total_tweets)
                print("-------------------")
                time.sleep(5)

            # 完毕，改变flag
            flag = False
            next_token = None
        time.sleep(5)
        counter += 1

print("Total number of results: ", total_tweets)
```

<a name="BGfCS"></a>

### 运行注意事项

- 全程使用国际互联网。

- 遇到中断，需要及时记录好最后写入的推文的时间，然后调整时间区间的数值，以免重复获取数据。

- 同时记得新建一个csv文件并且新建一个archive文件夹以便备份。

- 还没获取完的适合尽量不要打开正在写入csv文件，以免意外。
  <a name="aC4Ek"></a>
  
  ## 检测社交机器人
  
  要进行社交机器人鉴定，有许多工具可选，这里以由美国印第安纳大学社交媒体实验室开发的Botometer为例，简要说明其原理以及使用方式。
  <a name="z16JX"></a>
  
  ### 原理简介
  
  由美国印第安纳大学社交媒体实验室开发的Botometer是目前学界普遍采用的一种较为成熟和准确的社交机器人鉴别工具。目前最新的Botomter v4版本通过训练多个专门针对不同类型的社交机器人的分类器（社交机器人种类多样，有政治机器人、有娱乐机器人、有商业机器人），构建了一个能够更好地泛化的机器人检测系统。<br />这里需要补充说明的是，Botometer判定的社交机器人更多时候并非纯自动化生成并运作的机器人，而是至少部分通过自动化程序控制的Twitter账户，这类账户通常由提前设定好的触发器或者脚本操纵，在个人资料、朋友、社交网络结构、时间活动模式、语言和情绪等方面表现出异于人类的特征，Botometer将这些特征作为判定的依据。我们甚至可以自己使用一些工具来控制自己的Twitter账户。<br />BOT LIBRE：[https://www.botlibre.org/](https://www.botlibre.org/)<br />Botometer的工作流程大致为，通过Twitter API的鉴权，将需要检测的账户连同从Twitter获取到的用户特征一同发送到Botomter的服务器，Botomter服务器会将取得的用户特征与系统内已训练好的监督机器学习模型中成千上万个已被打上标记的例子进行比对，从而得到一个取值区间为[0, 5]的分数，分数显示了目标账号为机器人的可能性，0代表着最不可能为社交机器人，5代表最可能为社交机器人。当样本量较大时，可以使用Botometer v4的轻量版本BotometerLite，得到的是经过精简的分数区间[0, 1]，按照先前研究的经验，超过0.5即从概率上被认为是机器人账号。
  <a name="koyIa"></a>
  
  ### 准备

- 购买Botomter Pro API（小贵，大概50刀每月）

- Twitter API v1.1（用于鉴权，v2版本的Twitter API暂不支持）

- Pandas包（Python超强的数据分析工具，这里主要用于操作csv表格）

- Botomter的Python包

- 梯子

Botomter团队在Rapid API网站运营这个项目，这是其地址：<br />[https://rapidapi.com/OSoMe/api/botometer-pro](https://rapidapi.com/OSoMe/api/botometer-pro)<br />注册并购买Botometer Pro需要使用VISA卡。注意，用完以后记得及时退订，否则会自动扣费！<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/22532099/1654156094555-9b81f085-8d5e-42db-b329-4ce39b1a0b84.png#clientId=u607e242b-958e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=474&id=u5ad3e96f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=592&originWidth=1143&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91471&status=done&style=none&taskId=ub8f0f4e5-d43b-4d41-8b3a-9f1293c76f6&title=&width=914.4)<br />即使购买了仍然有使用次数的限制。Botometer LIte可以一次性检测100个账户。也就是说，一天最多可以检测27280个账户，所以事先对数据按用户去重很重要，可以节省资源。
<a name="oiyPQ"></a>

### 脚本解释

<a name="O6a96"></a>

#### 依赖

```python
import pandas as pd
import csv
import json
import time
import botometer
import math
```

<a name="NsKPD"></a>

#### 参数

```python
# 读取推文数据
df = pd.read_csv('./res.csv')
# BotometerAPI配置

# botometerAPI
rapidapi_key = "413fb65c04msh662dbc4d886621ap1aaed3jsnc6ce77e69865"
# Twitter API的密钥
twitter_app_auth = {
    'consumer_key': '5qDFi9HDTPYw9NoXGbgOmDgjH',
    'consumer_secret': 'ALHGUKpEvvShHLuA82zTAT85dbrHNKdrkXMfsoQ41WNpcuxuOE',
    'access_token': '1418747495828451331-37WC8wMOkpaozZAEl05okSFCV0uZ3m',
    'access_token_secret': '6CVAWOqHoqshkenxbsFv18ayx3H7d74Jtg3mnhs21DzWH',
  }

# 创建Botometer对象
blt_twitter = botometer.BotometerLite(rapidapi_key=rapidapi_key, **twitter_app_auth)
```

<a name="YFOmD"></a>

#### 必要操作

```python
# 数据去重去空（很重要）
df = df.dropna(subset=['author_id'])
df = df.drop_duplicates('author_id')
userList = list(df['author_id']) # 单独提出author ID
count = len(userList) / 100
count = math.floor(count) # 计算请求次数
# 准备写入文件
resFile = open('./boto.csv', "a", newline="", encoding='utf-8')
csvWriter = csv.writer(resFile)
csvWriter.writerow(['botscore', 'tweet_id', 'user_id'])
resFile.close() 
```

<a name="adD8s"></a>

#### 定义函数

```python
# 写入csv
def writeToCsv(file, row):
    file = open(file, "a", newline="", encoding='utf-8')
    csvWriter = csv.writer(file)
    csvWriter.writerow(row)
    file.close()

# 主函数
def run():
    for i in range(0, count): # 实现计算好的次数
        print(f'正在爬取第{i}轮...')
        tempList = userList[i*100:(i+1)*100] # 截取100个用户
        blt_scores = blt_twitter.check_accounts_from_user_ids(tempList) # 调用api
        tempStr = json.dumps(blt_scores)
        f = open(f'./archive1/new_json{i}.json', 'w') # 备份结果
        f.write(tempStr)
        f.close()
        # 写入csv
        for item in blt_scores:
            botscore = item['botscore']
            tweet_id = item['tweet_id'] if item['tweet_id'] else 'None'
            user_id = item['user_id']
            tempRow = [botscore, tweet_id, user_id]
            writeToCsv('./boto.csv', tempRow)
        time.sleep(5) # 暂停一会，以免超速
```

```python
# 执行主函数
run()
```

<a name="n2S5R"></a>

### 注意事项

如果发生中断，记得改参数，并新建csv文件（和调用Twitter API时类似），以免重复。<br />顺利的话，拿到boto.csv文件后再利用Excel的vlookup函数将分数添加到原始推文数据里面即可。
