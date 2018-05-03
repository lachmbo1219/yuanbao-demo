# 元寶遊戲系統接口文檔

## 文件目的
本文檔介紹平台與元寶系統的服務串接流程、調用接口參數規範、接口加密驗簽規則，並於文末提供各語言版本串接範例。


## 接口清單
## 元寶系統接口清單

  - launch(GET)-<a href="#launch(GET)">取得遊戲連結</a>
  
  
## 平台方接口清單

  - login-info(GET)-<a href="#login-info(GET)">取得玩家資訊</a>
  - balance(GET)-<a href="#balance(GET)">取得玩家餘額</a>
  - balance(PUT)-<a href="#balance(PUT)">更動玩家餘額</a>


### <p id="launch(GET)">launch(GET)-取得遊戲連結</p>
#### Reuqest

- Method: **GET**
- URL: ```/launch```
- Headers： Content-Type:application/json
- Body:
```
{
 		"spId": "PL0001",
		"productId": "lottery",
		"returnUrl": "www.google.com",
		"token": "20180502zaauxfrr",
		"sign":"c08d3e4cb641fbbdc5b06b448dd22395"
}
```

#### Response
- Body
```
{
	"retCode": "0",
	"data": {
		"gameUrl": "www.yuanbao-system.com/lottery/k6yo0+UWN588ZNEjvDnFOgUBh6DN5amHLLqwkatz5VM="
	}
}
```


### <p id="login-info(GET)">login-info(GET)-取得玩家資訊</p>
#### Reuqest

- Method: **GET**
- URL: ```平台提供自定義接口位置```
- Headers： Content-Type:application/json
- Body:
```
{
	"token": "20180502zaauxfrr",
	"sign": "02f8fc61372977a104f7cfb6356977dd"
}
```

#### Response
- Body
```
{ 
	"retCode": "0",
	"data": {
		"account": "GA0000123",
		"name": "小胖子",
		"balance": 50000,
		"headerurl": "0.png"
	}
}
```


### <p id="balance(GET)">balance(GET)-取得玩家餘額</p>
#### Reuqest

- Method: **GET**
- URL: ```平台提供自定義接口位置```
- Headers： Content-Type:application/json
- Body:
```
{
	"token": "20180502zaauxfrr",
	"sign": "02f8fc61372977a104f7cfb6356977dd"
}
```

#### Response
- Body
```
{ 
	"retCode": "0",
	"data": {
		"balance": 50000
	}
}
```


### <p id="balance(PUT)">balance(PUT)-更動玩家餘額</p>
#### Reuqest

- Method: **PUT**
- URL: ```平台提供自定義接口位置```
- Headers： Content-Type:application/json
- Body:
```
{
	"action": "bet", 
	"token": "20180502zaauxfrr", 
	"sign": "02f8fc61372977a104f7cfb6356977dd"
}
```

#### Response
- Body
```
{
	"retCode": "0"
}
```


## 傳輸規範

  - 使用TPC/IP協議作為傳輸層
  - 使用HTTP作為應用層協議
  - 傳遞參數格式皆為json(須使用Content-type規範header)
  - 此接口清單遵循restful設計理念
  
  
## 安全規範

  - 所有接口必須校驗sign簽名值正確無誤,再處理業務邏輯
  - 建議平台將元寶系統通知主機加入信任名單,防範其餘外來主機偽裝調用接口
  - token由平台方自行生成,失效時間可由平台自行定義,失效即表示玩家斷線


## 仍需優化項目

 - 須加上簽名演算範例
 - 須補參數資料型態、格式、定義
 - 須補全局錯誤碼
 

## 更新日誌

 - 2018/05/02	創建文檔	by davidccc


## 附錄：

 - <a href="https://github.com/TorchStoneRD/yuanbao-demo">文檔與DEMO包</a>
