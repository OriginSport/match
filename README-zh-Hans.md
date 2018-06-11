## API接口文档

## API接口文档

## BaseUrl
* test: http://test.ttnbalite.com:8021
* online: https://match.ttnbalite.com

## Category API
* [1. 查询比赛类别] 


### 1. 查询比赛类别
* 方法: `GET`
* URL: BaseUrl + /api/query/category/?level=game_category&lang=en-us
* URL: BaseUrl + /api/query/category/?level=game_parent&lang=en-us
* URL: BaseUrl + /api/query/category/?game_sub=basketball&lang=en-us

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  level    |  str       |   true| 类别层级, 'game_category'查询NBA,PL等，'game_parent',查询篮球、足球 , 'game_sub',查询篮球底下子类，nba
|game_sub| str|true|'game_sub',查询篮球底下子类，nba
|   lang     |     str    |    true|语言，默认英语, 'en-us', 中文：'zh-cn'

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  name | str       | 比赛类别名称，选择
|icon| str| 比赛类别图片
|id|int|比赛类别 id

* 结果示例：
```json
{
  "ok": true,
  "data": {
    "categories":[
      {
        "name": "nba",
        "icon": "xx.png",
        "id": 3,
          
      },
       {
        "name": "World Cup",
        "icon": "xx.png",
        "id": 3,
          
      },
    ]
  }
}
```






## Game API
* [1. 查询比赛信息] 
* [2. 查询一场比赛的详细信息]
* [3. 按utc日期查询赛程]
* [4. 查询比赛结果]




### 1. 查询比赛信息
* 方法: `GET`
* URL: BaseUrl + /api/query/game/?category_id=3&lang=en-us&page=5
* URL: BaseUrl + /api/query/game/?category_slug=nba&lang=en-us&page=1
 

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| category_id   | int|id slug任意传一个|比赛类别 id
|category_slug | str|id slug任意传一个|比赛类别 slug
|lang|str|true|默认是英文
|page|int|第几页，默认是第一页
|page_size|int|页面大小，默认是10
|type|str|赛程页面，投注页面，默认是投注页面，未开始比赛


| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  id|int    | 比赛 id
|name | str|比赛分类名称
|status|int|比赛状态,1：未开始，2：进行中，3：结束
|game_time|str|比赛开始时间 (utc)
|page|int|页数
|count|int|计数
|page_size|int|页面尺寸
|next|str|下一页url地址
|has_next|bool|是否有下一页
|comments|dic|比赛信息
|home_team_score|str|主队得分,比赛未开始是 ''
|away_team_score|str|客队得分
|home_team|obj|主队信息
|away_team|obj|客队信息
|name|str|球队名称
|icon|str|球队照片

* 结果示例：
```json
{
  "ok": true,
  "data": {
    "page":2,
    "count":96,
    "next":"/api/query/game/?lang=en-us&category_slug=uefacl&page=3",
    "page_size":10,
    "has_next":true,
    "games":{
      "games":[
    {
        "id": 1,
        "status": 1,
        "game_time":"2018-04-03T09:22:35Z",
        "home-team_score":100,
        "away_team_score":89,
        "home_team":{
          "name":"warriors",
          "icon": "xx.png",
          "short_name": "GSW"
        
      },
        "away_team":{
          "name":"spur",
          "icon": "xx.png",
          "short_name": "SAS"
      }
    }
    ],
      "lang": "en-us"
    }
  }
}
```




### 2. 查询一场比赛详细信息
* 方法: `GET`
* URL: BaseUrl + /api/query/game/detail/?game_id=550&lang=en-us

 

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| game_id   | int|true|比赛 id
|lang|str|rtue|默认是英文


| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  id|int    | 比赛 id
|name | str|比赛分类名称
|status|int|比赛状态,1：未开始，2：进行中，3：结束
|game_time|str|比赛开始时间 (utc)
|games|dic|比赛信息
|home_team_score|str|主队得分,比赛未开始是 ''
|away_team_score|str|客队得分
|home_team|obj|主队信息
|away_team|obj|客队信息
|name|str|球队名称
|icon|str|球队照片

* 结果示例：
```json
{
  "ok": true,
  "data": {
    "game":{
    {
      "id": 1,
      "status": 1,
      "game_time":"2018-04-03T09:22:35Z",
      "home-team_score":100,
      "away_team_score":89,
      "home_team":{
      "name":"warriors",
      "icon": "xx.png",
      "short_name": "GSW"
        
      },
      "away_team":{
        "name":"spur",
        "icon": "xx.png",
        "short_name": "SAS"
      }
    }
      "lang": "en-us"
    }
  }
}
```

### 3. 根据日期查询比赛
* 方法: `GET`
* URL: BaseUrl + /api/game/list/by/date/?game_date=2018-04-04&category_slug=uefacl&lang=en-us

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
|  game_date    |    str     | true  | 比赛日期
| category_id   | int|id slug任意传一个|比赛类别 id
|category_slug | str|id slug任意传一个|比赛类别 slug
|lang|str|rtue|默认是英文

| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|home_team_score   | str| 主队得分
|away_team_score| str| 客队得分
|game_time|str|比赛开始时间(utc)
|outer_id|str |链接
|id | int|比赛 id
|category|obj|比赛类别信息
|status|int|比赛状态,1：未开始，2：进行中，3：结束


* 结果示例：
```json
{
  "ok": true,
  "data": {
    "lange":"en-us",
    "games":[
    {
      "home_team_score":"4",
      "id":212,
      "game_time":"2018-04-04T18:45:00Z",
      "category":{
        "name": "uefacl",
        "slug": "uefacl",
        "id":"6"
    
      }
      "awaye_team_score":"1",
      "status":3,
      "outer_id":"50925030"
          
      },
    {
      "home_team_score":"2",
      "id":213,
      "game_time":"2018-04-04T18:45:00Z",
      "category":{
        "name": "uefacl",
        "slug": "uefacl",
        "id":"6"
    
      }
      "awaye_team_score":"1",
      "status":3,
      "outer_id":"50925031"
      }
    ]
  }
}
```



### 4. 查询比赛结果
* 方法: `GET`
* URL: BaseUrl + /api/query/game/result/?game_id=550&lang=en-us

 

| 输入参数      | 参数类型  | 必填  | 参数说明 |
| ---           | ---       | ---   | --- |
| game_id   | int|true|比赛 id
|lang|str|rtue|默认是英文


| 输出参数      | 参数类型    | 参数说明 |
| ---           | ---         | --- |
|  id|int    | 比赛 id
|name | str|比赛分类名称
|status|int|比赛状态,1：未开始，2：进行中，3：结束
|game_time|str|比赛开始时间 (utc)
|games|dic|比赛信息
|home_team_score|str|主队得分,比赛未开始是 ''
|away_team_score|str|客队得分
|home_team|obj|主队信息
|away_team|obj|客队信息
|name|str|球队名称
|icon|str|球队照片
|result|str|比赛结果字符串，未开始是 '-'


* 结果示例：
```json
{
  "ok": true,
  "data": {
    "game":{
    {
      "id": 1,
      "status": 1,
      "game_time":"2018-04-03T09:22:35Z",
      "home_team_score":100,
      "away_team_score":89,
      "home_team":{
      "name":"warriors",
      "icon": "xx.png",
      "short_name": "GSW"
        
      },
      "away_team":{
        "name":"spur",
        "icon": "xx.png",
        "short_name": "SAS"
      }
    }
      "lang": "en-us"
    }
    "result":"-"
  }
}
```
