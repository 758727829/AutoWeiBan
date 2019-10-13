<p align="center">
    <img src="https://i.loli.net/2019/07/22/5d3559f48053594320.png">
</p>

<h1 align="center">AutoWeiBan学习助手</h1>

<div align="center">

辅助麦课安全网课学习

![GitHub release](https://img.shields.io/github/release/WeiYuanStudio/AutoWeiBan.svg?style=flat-square)
![GitHub last commit](https://img.shields.io/github/last-commit/WeiYuanStudio/AutoWeiBan.svg?style=flat-square)

</div>

# 官方修改了登录POST请求参数，该脚本已经失效，该脚本已经失效，该脚本已经失效。详见Issues
# 等开学季再考虑修复了。十分抱歉，欢迎哪位大佬百忙中抽空PR帮忙修复

**当然备选方案也是有的**。
我的学弟用Java Script开发了一个刷课脚本，如果官方只修改了登录POST请求的话，理论上这个方案是可以的，您可以尝试一下这个方案。
详情访问：

学弟的WBKiller脚本的git仓库地址
<https://git.darc.pro/DarcJC/WBKiller>

使用方法链接位于学弟的个人博客
<https://darc.pro/archives/wbcourse-killer.html>

## 使用方法

1. 首先需要在运行设备上安装Python3运行环境。具体安装方法可以参考网上的教程进行一般操作。或者也可以使用包管理器很方便安装Python（Windows用户可以使用Choco，Mac可以使用Brew，Linux用户，恩，包管理器对于Linux用户来说就是传统艺能）。

2. 接着打开命令行操作界面，CD（Change Directory）到该脚本的目录下

3. 最后执行`python main.py` 即可开始运行该脚本，按照指示使用即可。

## 可以Modify（自定义）的地方

1. 院校码，这个没有深入研究如何获取到具体学校的tenantCode(院校码，用于发送请求时区分学校)。每个学校的都是不同的，如果你想获取自己学校的tenantCode的话，你可以自己试着登录一次，在浏览器开发者工具中的网络选项卡中查看网络请求信息抓取。或者实在不会操作可以提个Issues过来。

2. 课程间的延迟时间，在**WeiBanAPI.py文件**的头部中有两个参数分别为**baseDelayTime**基础延时秒数和**randomDelayDeviation**叠加随机延时差。**实际延迟时间 = 基础延时秒数 + 叠加随机延时差**

## 抓包

### 登录请求

Request URL: https://weiban.mycourse.cn/pharos/login/login.do

Method: POST

Status Code: 200 OK

HEAD:
```
Host: weiban.mycourse.cn
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 64
Connection: keep-alive
Referer: https://weiban.mycourse.cn/
Cookie: ****
```

Parameter:

|keyNumber       |学号            |
|----------------|----------------|
|password	     |密码            |
|tenantCode	     |学院编码         |

Response:
```JSON
{
    "code":"0",
    "data":{
        "userId":"用户ID",
        "userName":"账号，吉珠是身份证",
        "isBind":"1",
        "tenantCode":"学院编号",
        "batchCode":"003",
        "gender":1,
        "openid":"oeNC****57Zc",
        "switchGoods":1,
        "switchDanger":1,
        "switchNetCase":1,
        "isConfirmed":2,
        "preUserProjectId":"4ca8****c6a6任务ID",
        "preAlias":"新生安全教育",
        "preBanner":"https://h.mycourse.cn/pharosfile/resources/images/projectbanner/pre.png",
        "normalAlias":"安全课程",
        "normalBanner":"https://h.mycourse.cn/pharosfile/resources/images/projectbanner/normal.png",
        "specialAlias":"专题学习",
        "specialBanner":"https://h.mycourse.cn/pharosfile/resources/images/projectbanner/special.png",
        "militaryAlias":"军事理论",
        "militaryBanner":"https://h.mycourse.cn/pharosfile/resources/images/projectbanner/military.png",
        "isLoginFromWechat":2
    },
    "detailCode":"0"
}
```

### 课程请求

Request URL: https://weiban.mycourse.cn/pharos/usercourse/listCourse.do

Method: POST

Status Code: 200 OK

HEAD:
```
Host: weiban.mycourse.cn
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 89
Connection: keep-alive
Referer: https://weiban.mycourse.cn/
Cookie: ****
```

Parameter:

|userProjectId   |4ca8****c6a6任务ID|
|----------------|----------------|
|chooseType      |3 (未知值)      |
|tenantCode      |学院编号        |
|name            |空 (未知值)     |


Response:
```JSON
{
    "code":"0",
    "data":[
        {
            "categoryCode":"001001",
            "categoryName":"国家安全与安全文化",
            "categoryRemark":"国家安全是国家的基本利益，是一个国家处于没有危险的客观状态，也就是国家没有外部的威胁和侵害也没有内部的混乱和疾患的客观状态。
国家安全大类从领土安全、政治安全、军事安全、经济安全、文化安全、科技安全、生态安全、网络安全、相关法律法规等方面介绍了总体国家安全观内容，以及从反恐、间谍、邪教等方面介绍了国家安全知识内容。",
            "totalNum":11,
            "finishedNum":11,
            "courseList":[
                {
                    "userCourseId":"2d63****912b单课ID",
                    "resourceId":"b78de19d-********-5a61f9e2726b",
                    "resourceName":"邪教的自述",
                    "finished":1,
                    "isPraise":1,
                    "isShare":2,
                    "praiseNum":33345,
                    "shareNum":0,
                    "shared":2
                }
            ]
        }
    ]
}
```
### 进度请求

Request URL: https://weiban.mycourse.cn/pharos/project/showProgress.do

Method: POST

Status Code: 200 OK

HEAD:
```
Host: weiban.mycourse.cn
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 70
Connection: keep-alive
Referer: https://weiban.mycourse.cn/
Cookie: ****
```

Parameter:

|userProjectId	 |4ca8****c6a6任务ID|
|----------------|----------------|
|tenantCode	     |51900002        |


Response:
```JSON
{
    "code":"0",
    "data":{
        "courseNum":200,
        "courseFinishedNum":200,
        "pushNum":0,
        "pushFinishedNum":0,
        "optionalNum":0,
        "optionalFinishedNum":0,
        "requiredNum":200,
        "requiredFinishedNum":200,
        "examNum":2,
        "examFinishedNum":2,
        "endTime":"2019-04-30 00:00:00",
        "ended":1,
        "lastDays":0,
        "courseFinished":1
    },
    "detailCode":"0"
}
```

### 获取个人信息

Request URL: https://weiban.mycourse.cn/pharos/my/getInfo.do

Method: POST

Status Code: 200 OK

HEAD:
```
Host: weiban.mycourse.cn
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: application/json, text/plain, */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded
Content-Length: 63
Connection: keep-alive
Referer: https://weiban.mycourse.cn/
Cookie: ****
Cache-Control: max-age=0
```

Parameter:

|userId	         |fdc2****0043个人ID|
|----------------|----------------|
|tenantCode	     |学院码          |


Response:
```JSON
{
    "code":"0",
    "data":{
        "realName":"张三",
        "studentNumber":"",
        "examNumber":"",
        "enrollNumber":"",
        "gender":"",
        "tenantName":"学校名",
        "orgName":"计算机学院",
        "specialtyName":"软件工程",
        "mobile":""
    },
    "detailCode":"0"
}
```

### 请求完成课程

Request URL: https://weiban.mycourse.cn/pharos/usercourse/finish.do?userCourseId=2d63****8912b&tenantCode=51900002

Method: GET

Status Code: 200 OK

HEAD:
```
Host: weiban.mycourse.cn
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:67.0) Gecko/20100101 Firefox/67.0
Accept: */*
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Connection: keep-alive
Referer: *****
Cookie: ****
Pragma: no-cache
Cache-Control: no-cache
```
