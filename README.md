*[English](README.md) ∙ [简体中文](README-zh-Hans.md)*

## API Document

## API Document

## BaseUrl
* test: http://test.ttnbalite.com:8021
* online: https://match.ttnbalite.com


## Category API
* [1. Query Game Category] 


### 1. Query Game Category
* METHOD: `GET`
* URL: BaseUrl + /api/query/category/?level=game_category&lang=en-us
* URL: BaseUrl + /api/query/category/?level=game_parent&lang=en-us
* URL: BaseUrl + /api/query/category/?game_sub=basketball&lang=en-us

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  level    |  str       |   true| Category level, game_category can query NBA,PL and so on，game_parent can query basketball, soccer, game_sub can query basketball subcategory
|game_sub |str | true|'game_sub',查询篮球底下子类，nba
|   lang     |     str    |    true|language，defacult english, english: 'en-us', chinese：'zh-cn'

| Response      | Type    | Description |
| ---           | ---         | --- |
|  name | str       | category name
|icon| str| category icon
|id|int|category id

* Response：
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
* [1. Query Game Info] 
* [2. Query Game Detail]
* [3. Query Game Schedule By UTC Date]
* [4. Query Game Result]




### 1. Query Game Info
* 方法: `GET`
* URL: BaseUrl + /api/query/game/?category_id=3&lang=en-us&page=5
* URL: BaseUrl + /api/query/game/?category_slug=nba&lang=en-us&page=1
 

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| category_id   | int|id or slug|category id
|category_slug | str|id or slug|category slug
|lang|str|true|default english
|page|int|page, default 1
|page_size|int|page size, default 10
|type|str|schedule，bet，default bet page


| Response      | Type    | Description |
| ---           | ---         | --- |
|  id|int    | Game id
|name | str|category name
|status|int|game status,1：pre，2：play，3：post
|game_time|str|game start time (utc)
|page|int|page
|count|int|count
|page_size|int|page size
|next|str|next page url
|has_next|bool|
|comments|dic|Game info
|home_team_score|str|home_team_score, realtime score, pre status is ''
|away_team_score|str|away_team_score, realtime score, pre status is ''
|home_team|obj|home team info
|away_team|obj|away team info
|name|str|name
|icon|str|icon

* Response：
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




### 2. Query Game Detail
* 方法: `GET`
* URL: BaseUrl + /api/query/game/detail/?game_id=550&lang=en-us

 

|Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| game_id   | int|true|game id
|lang|str|rtue|default english


| Response     | Type    | Description |
| ---           | ---         | --- |
|  id|int    | game id
|name | str|category name
|status|int|game status,1：pre，2：play，3：post
|game_time|str|game start time(utc)
|games|dic|game info
|home_team_score|str|home_team_score, realtime score, pre status is ''
|away_team_score|str|away_team_score, realtime score, pre status is ''
|home_team|obj|home team info
|away_team|obj|away team info
|name|str|team name
|icon|str|team icon

* Response：
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

### 3. Query Game Schedule By UTC Date
* 方法: `GET`
* URL: BaseUrl + /api/game/list/by/date/?game_date=2018-04-04&category_slug=uefacl&lang=en-us

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
|  game_date    |    str     | true  | game date
| category_id   | int|id or slug|category id
|category_slug | str|id or slug|category slug
|lang|str|rtue|默认是英文

| Response      |   Mandatory  | Description |
| ---           | ---         | --- |
|home_team_score   | str| home_team_score, realtime score, pre status is ''
|away_team_score| str| away_team_score, realtime score, pre status is ''
|game_time|str|game start time(utc)
|outer_id|str |link
|id | int|game id
|category|obj|game category
|status|int|game status,1：pre，2：play，3：post


* Response：
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



### 4. Query Game Result
* 方法: `GET`
* URL: BaseUrl + /api/query/game/result/?game_id=550&lang=en-us

 

| Name      | Type  | Mandatory  | Description |
| ---           | ---       | ---   | --- |
| game_id   | int|true|game id
|lang|str|rtue|default english


| Response      | Type    | Description |
| ---           | ---         | --- |
|  id|int    | game id
|name | str|category name
|status|int|game status,1：pre，2：play，3：post
|game_time|str|game start time (utc)
|games|dic|game info
|home_team_score|str|home_team_score, realtime score, pre status is ''
|away_team_score|str|away_team_score, realtime score, pre status is ''
|home_team|obj|home team info
|away_team|obj|away team info
|name|str|name
|icon|str|icon
|result|str|result，pre '-'


* Response：
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
