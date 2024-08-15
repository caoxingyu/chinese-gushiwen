## chinese-gushiwen
中华古诗文数据库和API。数据库收录10000首古文(诗、词、歌、赋以及其它形式的文言文)，近4000名作者，10000名句。
其中古文不仅包含原文，还提供注释、翻译、赏析以及朗诵音频地址链接；作者包含了详细生平介绍；名句包含原句以及出处。
- *因访问量原因，API暂时下线，无法访问，有需要的同学保存数据后可自行开发API。*
- *因音频文件被用户大量下载，音频地址添加了权限，无法直接访问，有需要的朋友通过邮箱1746569077@qq.com联系作者。*



- ### 数据库介绍
1. #### 古文(guwen文件夹)
   -------
   古文一共10000首，分别存在10个文件中，每个json文件存1000首。每一首都是一个json对象：
       
       {
         "id":{"$oid":"5b9a0136367d5c96f4cd2952"},
         "title":"将进酒",
         "dynasty":"唐代",
         "writer":"李白",
         "type":["乐府","唐诗三百首","咏物","抒情","哲理","宴饮"]",
         "content":"君不见，黄河之水天上来，奔流到海不复回。\n君不见，高堂明镜悲白发，朝如青丝暮成雪...",
         "remark":"将进酒：属乐府旧题。将（qiāng）：请。\n君不见：乐府中常用的一种夸语...",
         "translation":"你难道看不见那黄河之水从天上奔腾而来，波涛翻滚直奔东海，从不再往回流...",
         "shangxi":"这首诗非常形象的表现了李白桀骜不驯的性格：一方面对自己充满自信，孤高自傲；一方面在政治前途出现波折后...",
         "audioUrl":"https://guwen-1252396323.cos.ap-chengdu.myqcloud.com/guwen/20180913141830595.mp3"
       }
        
       id:古文的id，由于古文是从Mongodb数据库直接导出，所以id是此格式；
       title：古文标题；
       dynasty：古文所属朝代；
       writer：古文的作者；
       type：古文所属的类型；
       content：古文原文；
       remark：古文注释；
       translation：古文翻译；
       shangxi:古文的赏析；
       audioUrl：原文朗诵音频链接；
       
       注：并非每一首古文都有这些字段，但是一些千古流传的名作基本都有这些内容。
       
  
2. #### 作者(writer文件夹)
   -------
   数据库目前共收录3983名作者，存在writer文件夹，分别存在4个json文件中，每1000名作者存一个文件，每一个writer都是如下的json对象：
   
       {
          "_id":{"$oid":"5b9b6211367d5c24d8bcdc01"},
          "name":"李白",
          "headImageUrl":"https://guwen-1252396323.cos.ap-chengdu.myqcloud.com/headImage/20180914152354795.jpg",
          "simpleIntro":"李白（701年－762年），字太白，号青莲居士，唐朝浪漫主义诗人，被后人誉为“诗仙”...",
          "detailIntro":"{\"轶事典故\":\"姓名由来\\n  第一种说法...,\"家庭成员\":\"家人\\n据《旧唐书》记载，李白之父名叫李客..}"
       }
       
       id:作者id；
       name：作者名称；
       headImageUrl：作者头像地址；
       simpleIntro：作者简介；
       detailIntro：作者详介，也是一个Json对象。
       
       注:并非每一名作者都有这些字段，但是对于一些知名作者，我们提供尽可能详细的资料。
3. #### 名句(sentence文件夹)
   -------
   数据库目前共收录10000句流传后世、大家耳熟能详的名句，存在sentence文件夹，存在1个json文件中，每一个名句都是如下的json对象：
   
       {
           "_id":{"$oid":"5b9b713f367d5c55cca9c92a"},
           "name":"山有木兮木有枝，心悦君兮君不知。",
           "from":"佚名《越人歌》"
       }
       
       id:名句的id；
       name：名句内容；
       from：出自；     


- ### ~~API接口~~
所有接口皆为get方式，返回数据为json格式，分页查询除名句外每页大小皆为10，皆返回简单信息，要获取详细信息，需用id去查询相关接口，名句的分页查询每页为50，返回所有信息。
1. #### 古文
-----
- ##### 查询所有古文
需要一个参数：page表示第几页，没有则默认返回第一页，返回内容每页大小为10，只返回古文的简单信息，不包含remark、translation、shangxi以及audioUrl字段，要获取古文的详细内容，用返回的id访问"根据id获取古文"接口，见下面。

     https://www.caoxingyu.club/guwen/selectall?page=1，会返回前10条古文      

[示例1：查询前10条古文](https://www.caoxingyu.club/guwen/selectall?page=1) 

[示例2：查询第11-20条古文](https://www.caoxingyu.club/guwen/selectall?page=2)

- ##### 根据作者查询古文
需要两个参数：page表示第几页，没有默认返回第一页；writer作者名称；

    https://www.caoxingyu.club/guwen/selectbywriter?page=1&writer=李白，会返回作者为李白的前10条古文

[示例1：查询作者为李白的前10条古文](https://www.caoxingyu.club/guwen/selectbywriter?page=1&writer=李白)

[示例2：查询作者为杜甫的前10条古文](https://www.caoxingyu.club/guwen/selectbywriter?page=1&writer=杜甫)

- ##### 根据朝代查询古文
需要两个参数：page表示第几页，没有默认返回第一页；dynasty朝代名称；

     https://www.caoxingyu.club/guwen/selectbydynasty?page=1&dynasty=唐代.会返回朝代为唐代的前10条古文

[示例1：朝代为唐代的前10条古文](https://www.caoxingyu.club/guwen/selectbydynasty?page=1&dynasty=唐代)

[示例2：朝代为宋代的前10条古文](https://www.caoxingyu.club/guwen/selectbydynasty?page=1&dynasty=宋代)

- ##### 根据关键字查询古文（可输入标题、作者、原文中的内容）
需要两个参数：page表示第几页，没有默认返回第一页；keyword要查询的关键字，可以是作者、标题、原文中的内容。

     https://www.caoxingyu.club/guwen/selectbykeyword?page=1&keyword=李，会返回作者中包含“李”、标题中包含“李”、原文中包含“李”的前10条古文

[示例1：查询关键字为"李"的前10条古文](https://www.caoxingyu.club/guwen/selectbykeyword?page=1&keyword=李)     

[示例2：查询关键字为"静夜"的前10条古文](https://www.caoxingyu.club/guwen/selectbykeyword?page=1&keyword=静夜)   

- ##### 根据古文id查询古文详情
需要一个参数：id表示古文的id，上面的分页查询接口都会返回id。

     https://www.caoxingyu.club/guwen/selectbyid?id=5b9a0136367d5c96f4cd2952,会返回将进酒的详细信息

[示例1：查询id为"5b9a0136367d5c96f4cd2952"的古文](https://www.caoxingyu.club/guwen/selectbyid?id=5b9a0136367d5c96f4cd2952)        

2. #### 作者
-----
- ##### 查询所有作者
需要一个参数：page表示第几页，没有则默认返回第一页，返回内容每页大小为10，只返回作者的简单信息，不包含detailIntro字段。

     https://www.caoxingyu.club/guwen/writer/selectall?page=1,会返回前10条作者信息

[示例1：查询前10名作者](https://www.caoxingyu.club/guwen/writer/selectall?page=1) 

- ##### 根据作者名称查询

      https://www.caoxingyu.club/guwen/writer/selectbyname?name=李白,会返回李白的详细信息

[示例1：查询姓名为"李白"的作者信息](https://www.caoxingyu.club/guwen/writer/selectbyname?name=李白) 

- ##### 根据id查询作者详情
      https://www.caoxingyu.club/guwen/writer/selectbyid?id=5b9b6211367d5c24d8bcdc01，会返回李白的详细信息

[示例1：查询id为"5b9b6211367d5c24d8bcdc01"的作者信息](https://www.caoxingyu.club/guwen/writer/selectbyid?id=5b9b6211367d5c24d8bcdc01)       

3. #### 名句
-----
- ##### 查询所有名句
需要一个参数：page表示第几页，没有则默认返回第一页，返回内容每页大小为50。

     https://www.caoxingyu.club/guwen/sentence/selectall?page=1,会返回前50条名句

[示例1：查询前50条名句](https://www.caoxingyu.club/guwen/sentence/selectall?page=1) 

- ##### 根据名句查询原文
需要一个参数：sentence名句

    https://www.caxoingyu.club/guwen/selectbysententce?sentence=山有木兮木有枝，心悦君兮君不知。（会返回该名句所在的原文，也可用“根据关键字查询古文”接口）

[方法1：查询"山有木兮木有枝，心悦君兮君不知。"所在原文](https://www.caoxingyu.club/guwen/selectbysententce?sentence=山有木兮木有枝，心悦君兮君不知。) 

[方法2：查询"山有木兮木有枝，心悦君兮君不知。"所在原文](https://www.caoxingyu.club/guwen/selectbykeyword?page=1&keyword=山有木兮木有枝，心悦君兮君不知。)

- ### ~~“蜉蝣诗词古文”小程序~~（已下架，无法访问）
    “诗词歌赋全集”小程序已经上线，感兴趣的同学可立即扫码体验。      
   
  ![蜉蝣诗词古文](https://guwen-1252396323.cos.ap-chengdu.myqcloud.com/qrcode.jpg "蜉蝣诗词古文")   
    
  <br><br>&ensp;&ensp; *数据皆来自网络，由本人整理，仅供交流学习使用*



