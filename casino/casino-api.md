# Casino API Document
  
### API數量：**15**
-------
1. [註冊帳號](#註冊帳號)
1. [取得玩家登入網址](#取得玩家登入網址)
1. [查詢玩家](#查詢玩家)
1. [修改玩家暱稱](#修改玩家暱稱)
1. [設定玩家帳號模式](#設定玩家帳號模式)
1. [設定玩家是否啟用遊戲](#設定玩家是否啟用遊戲)
1. [設定玩家限輸](#設定玩家限輸)
1. [設定玩家限贏](#設定玩家限贏)
1. [玩家限注回復](#玩家限注回復)
1. [玩家額度轉出入](#玩家額度轉出入)
1. [玩家轉帳狀態查詢](#玩家轉帳狀態查詢)
1. [玩家下注查詢](#玩家下注查詢)
1. [玩家下注簡報查詢](#玩家下注簡報查詢)
1. [踢玩家](#踢玩家)
1. [踢多玩家](#踢多玩家)
2. [設定信用玩家額度](#設定信用玩家額度)
3. [查詢信用玩家額度](#查詢信用玩家額度)
4. [重設信用玩家額度](#重設信用玩家額度)
5. [查詢注區範本](#查詢注區範本)
6. [玩家注區範本設定查詢](#玩家注區範本設定查詢)
7. [玩家注區範本設定](#玩家注區範本設定)
8. [手機API串接](#手機API串接)

### *登入流程*
-------
1. 玩家透過平台登入
2. 平台透過[註冊帳號](#註冊帳號)註冊帳號
3. 平台透過[玩家額度轉出入](#玩家額度轉出入)
4. 平台透過[取得玩家登入網址](#取得玩家登入網址)
5. 使用[取得玩家登入網址](#取得玩家登入網址)回傳內容 `LoginUrl` 登入遊戲

### [流程圖連結](https://cacoo.com/diagrams/xgypN4flYVaJlTcU#28811)

![流程圖](https://cacoo.com/diagrams/xgypN4flYVaJlTcU-28811.png "API 登入 流程圖")

---

### <span id="GameType">遊戲類別</span>
| 遊戲名稱  | gameType                 | 
|---------- |-------------------------  |
| 百家樂         | 1   | 

--

### <span id="mode">玩家帳號模式</span>
| 代碼  | mode 說明                | 
|---------- |-------------------------  |
| 0         | 正常   | 
| 1        | 鎖單(不能下注)   | 
| 2        | 停用(不能進入遊戲)，修改狀態為 2時會執行踢除玩家   | 

--

### <span id="enable">玩家啟用狀態</span>
| 代碼  | enable 說明                 | 
|---------- |-------------------------  |
| 0         | 停用   | 
| 1        | 啟用   | 

--

### <span id="currency">支援幣別</span>
| 代碼  | 幣別                  | 
|---------- |-------------------------  |
| TWD        | 台幣   | 
| CNY       | 人民幣   | 

--

### <span id="language">支援語系</span>
| 代碼  | 說明                  | 
|---------- |-------------------------  |
| zh_TW     | 繁體中文   | 
| zh_CN     | 簡體中文   | 

--

### <span id="platformType">支援裝置</span>
| 代碼  | 說明                  |
|---------- |-------------------------  |
| Web     | 網頁電腦版  |
| Android    | App   |
| IOS     | App   |

--

### <span id="TableType">注區範本遊戲類別</span>
| 遊戲名稱  | gameType                 |
|---------- |-------------------------  |
| 百家樂         | 1   |
| 多檯         | 4   |

--

### *錯誤代碼*
-------
| 錯誤代碼  | 錯誤訊息                  | 錯誤說明              |
|---------- |-------------------------  |---------------------- |
| 1  | {parameter} is required   | 缺少必填參數            |
| 2  | key is invalid            | 提供的金鑰是不合法的    |
| 3  | hash is invalid           | 驗證碼是錯誤的           |
| 4  | player not found            | 找不到合法的使用者     |
| 5  | {method} is not allowed   | http method 不允許       |
| 6  | query time range out of limit   | 查詢時間範圍超出限制       |
| 7  | internal server error   | 伺服器內部錯誤       |
| 8  | player is offline   | 玩家離線       |
| 9  | player is online   | 玩家在線中，無法轉出入額度       |
| 10 | service not available   | 無法使用遊戲服務       |
| 11 | {parameter} is invalid   | 參數不合法       |
| 12 | gameType:{gameType} not found  | 無此遊戲存在       |
| 13 | account length between 4 - 20  |  帳號至少4位元以上      |
| 14 | nickname length between 1- 20  | 暱稱至少1位元以上       |
| 15 | enable setting is invalid  | 玩家啟用設定值不合法       |
| 16 | mode setting is invalid  | 玩家帳號模式設定值不合法       |
| 17 | transfer in error  | 額度轉入失敗       |
| 18 | transfer out error  | 額度轉出失敗       |
| 19 | player credit is not enough  | 玩家籌碼不足       |
| 20 | account:{account} has been used| 此帳號已被使用 |
| 21 | player have not yet checkout bet | 玩家有下注尚未結算注單，無法轉出入額度       |
| 22 | {param} must be a unsigned integer  | {param}設定值必須為正整數       |
| 23 | [startAt or  EndAt] value must be datetime Example：2017-01-01 00:00:00   | 查詢玩家注單，時間參數必須使用規定格式       |
| 24 |{transferId} is not exist   | 此筆交易單不存在       |
| 25 | transfer id can not be empty  | 交易的ID不可為空       |
| 26 | transferid:（平台方TransferID）has been used  | 此交易單已被使用       |
| 27 | transfer in or out can not be 0  | 額度轉出入設定值不可為0       |
|28|transfer id:{transfer id} transaction processing| 交易單處理中   |
|29|{params} must be entirely alpha-numeric characters| {param} 只允許英數   |
|30|{params} must be a unsigned decimal| {param} 只允許正數的 decimal   |
|31|{params} must be a integer| {param} 只允許整數   |
|32|player mode is been disabled   | 此帳號模式已被停用 |
|33|player enable is been disabled   | 此帳號已設定為不啟用 |
|34|tableType:{tableType} not found|您所設定的[注區範本遊戲類別](#注區範本遊戲類別)不支援|
|35|player stake limit setting max five count| 注區範本最大為5筆 |
|36|player stake limit setting value [{invalid stakeLimitValue}] is invalid| 注區範本設定值有不合法內容 |
|37|platform type {platformType} is invalid | 支援裝置不存在 |
|38|The cashtype is invalid | 此 api 操作不合法 |
|39|The credit reset action is padding | 回復設定尚在進行中 |
|40|{param} must be a unsigned integer, and only numeric characters | 只允許正數的 integer，且不允許正負記號 |
| 102|The currency:{currency} is not supported|您所設定的貨幣類型不支援|
| 103 | The language is not supported| 您所設定的語系類型不支援 |

### *API 使用*
-------

1. ## <span id="player-register">註冊帳號</span>

    ```
    POST /casino-api/player/register?
        key=<key>&
        account=<account>&
        nickname=<nickname>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  nickname   | 玩家暱稱 |  string  |     必填    |
    |  currency   | 玩家貨幣類型 |  設定玩家貨幣類型，設定之後不可更改  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + nickname + currency + secret)`**
    
    ---
    
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  nickname   | 玩家暱稱 |  string  |
    |  currency   | 玩家設定幣別 |  string  |
    |  playerId   | 遊戲方玩家編號 |  integer  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "nickname":"a99asdf",
            "currency":"TWD",
            "playerId":63
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```

   ---
   
   #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 13 | account length between 4 - 20  |
    | 14 | nickname length between 1- 20  |
   | 20 | account:{account} has been used  |
   | 102 | The currency:{currency} is not supported |
   
2. ## <span id="player-auth">取得玩家登入網址</span>

    ```
    GET /casino-api/player/auth?
        key=<key>&
        account=<account>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  gameType | [遊戲類別](#遊戲類別)  |  smallint  | 選填，預設為：1(百家樂)    |
    |  language | 語系代碼 |  string  | 選填[支援語系](#支援語系)，預設為：zh_TW    |
    |  platformType | 裝置代碼|string| 選填[支援裝置](#支援裝置)，預設為：Web    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  loginUrl | 遊戲登入網址|  string  | 
    | token | 登入用 token | string |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "loginUrl":"http://test.app/casino-api/player/login?token=......M1NyJ9",
            "token":"......M1NyJ9"}
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```
   
   ---
   
   #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found            |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 12 | gameType:{gameType}  not found|
    |22 |{param} must be a unsigned integer |
    |32|player mode is been disabled   | 
    |33|player enable is been disabled   |
    |37|platform type {platformType} is invalid |
    | 103 | The language is not supported |
   
3. ## <span id="player-info">查詢玩家</span>

    ```
    GET /casino-api/player/info?
        key=<key>&
        account=<account>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號|  string  | 
    |  nickname | 玩家暱稱|  string  | 
    |  enable | 帳號啟用|  smallint  | 
    |  mode | 帳號模式|  smallint  | 
    |  isOnline | 玩家是否在線|  smallint  | 
    |  credit | 額度|  decimal(19,4)  | 
    |  limitWin | 限贏|  decimal(19,4)  | 
    |  limitLose | 限輸|  decimal(19,4)  | 

    ---

    #### <span id="enable">玩家啟用狀態</span>
    | 代碼  | enable                  | 
    |---------- |-------------------------  |
    | 0         | 停用   | 
    | 1        | 啟用   | 
    
    #### <span id="mode">玩家帳號模式</span>
    | 代碼  | mode                  | 
    |---------- |-------------------------  |
    | 0         | 正常   | 
    | 1        | 鎖單(不能下注)   | 
    | 2        | 停用(不能進入遊戲)，修改狀態為 2時會執行踢除玩家   | 
        
    #### <span id="isOnline">玩家是否在線</span>
    | 代碼  | isOnline                  | 
    |---------- |-------------------------  |
    | 0        | 玩家離線  | 
    | 1        | 玩家在線  |

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "nickname":"a99asdf",
            "currency":"TWD",
            "enable":1,
            "mode":0,
            "isOnline":0,
            "credit":4101.0000,
            "limitWin":1099.0000,
            "limitLose":1.0000
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```
   
    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found            |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |


4. ## <span id="player-nickname">修改玩家暱稱</span>

    ```
    PUT /casino-api/player/nickname?
        key=<key>&
        account=<account>&
        nickname=<nickname>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  nickname   | 玩家暱稱 |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + nickname + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  nickname   | 玩家暱稱 |  string  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "nickname":"a99asdf"
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```
   
    ---
   
   #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |   
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 14 | nickname length between 1- 20  |
    
5. ## <span id="player-mode">設定玩家帳號模式</span>

    ```
    PUT /casino-api/player/mode?
        key=<key>&
        account=<account>&
        mode=<nickname>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  mode   | 帳號模式 |  smallint  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    
    #### <span id="mode">玩家帳號模式</span>
    | 代碼  | mode                  | 
    |---------- |-------------------------  |
    | 0         | 正常   | 
    | 1        | 鎖單(不能下注)   | 
    | 2        | 停用(不能進入遊戲)，修改狀態為 2時會執行踢除玩家   | 
    
    #### **`hash = md5(account + mode + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  mode   | 帳號模式 |  smallint  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "mode":1
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":16,"message":"mode setting is invalid"
        }
    }
   ```
   
   #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 16 | mode setting is invalid  |
    | 22 | {param} must be a unsigned integer  |
    |40|{param} must be a unsigned integer, and only numeric characters |

6. ## <span id="player-enable">設定玩家是否啟用遊戲</span>

    ```
    PUT /casino-api/player/enable?
        key=<key>&
        account=<account>&
        enable=<enable>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  enable   | 玩家帳號啟用 |  smallint  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### <span id="enable">玩家啟用狀態</span>
    | 代碼  | enable                  | 
    |---------- |-------------------------  |
    | 0         | 停用   | 
    | 1        | 啟用   | 

    #### **`hash = md5(account + enable + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  enable   | 玩家帳號啟用 |  smallint  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "enable":1
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":15,
            "message":"enable setting is invalid"
        }
    }
   ```


    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 15 | enable setting is invalid  |
    | 22 | {param} must be a unsigned integer  |
    |40|{param} must be a unsigned integer, and only numeric characters |
    
7. ## <span id="player-limit-lose">設定玩家限輸</span>

    ```
    PUT /casino-api/player/limit/lose?
        key=<key>&
        account=<account>&
        limit=<limit>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  limit   | 限輸值 |  decimal(19,4) |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + limit + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  limit   | 限輸值 |  decimal(19,4)  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "limitLose":10.1239
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":30,
            "message":"limit must be a unsigned decima"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 13 | account length between 4 - 20  |
    |30|{params} must be a unsigned decimal|
    
8. ## <span id="player-limit-win">設定玩家限贏</span>

    ```
    PUT /casino-api/player/limit/win?
        key=<key>&
        account=<account>&
        limit=<limit>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  limit   | 限贏值 |  decimal(19,4) |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + limit + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  limit   | 限贏值 |  decimal(19,4)  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "limitWin":10.1239
        }
    }
    ```

    失敗

   ```javascript
    {
        "status":"error",
        "error":{
            "code":30,
            "message":"limit must be a unsigned decima"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    |30|{params} must be a unsigned decimal|
    

9. ## <span id="player-recover">玩家限注回復</span>

    ```
    PUT /casino-api/player/limit/recover?
        key=<key>&
        account=<account>&
        hash=<hash>
    ```
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234"
        }
    }
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
    ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    

10. ### <spin id="player-transfer">玩家額度轉出入</spin>
   
    ```
    PUT /casino-api/player/credit/transfer?
        key=<key>&
        account=<account>&
        credit=<credit>&
        transferId=<transferId>&
        hash=<hash>
    ```
    
    #### *限現金平台使用
    
    #### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  credit | 轉出入額度 |integer  |必填，正值為轉入，負值為轉出。(目前不開放小數籌碼，請仍以整數串送)    |
    |transferId |平台方交易Id |string| 必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    
    #### **`hash = md5(account + credit + transferId + secret)`**
    ---
    
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  originCredit   | 交易前額度 |  decimal(19,4)  |
    |  addCredit   | 增加額度 |  integer  |
    |  finalCredit   | 交易後額度 |  decimal(19,4)  |
    |  transferId   | 平台方交易Id(只允許英數) |  string  |
    |  orderId   | 此筆交易單號 |  integer  |
    |  status   | 交易狀態 |  smallint  |

    #### <span id="enable">交易狀態</span>
    | 代碼  | status                  | 
    |---------- |-------------------------  |
    | 0         | 成功   | 
    
    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "originCredit":4201.6,
            "addCredit":500,
            "finalCredit":4701.6,
            "transferId":"AA1099",
            "orderId":28,
            "status":0
        }
    }
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":4,
            "message":"account not found"
        }
    }
    ```

    #### 會出現的錯誤項目
    
    | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid    |
    | 3  | hash is invalid    |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 9  | player is online   |
    |  10  |service not available |
    | 11 | {parameter} is invalid   |
    | 19 | player credit is not enough  |
    | 21 | player have not yet checkout bet |
    | 25 | transfer id can not be empty  |
    | 26 | transferid:（平台方TransferID）has been used  |
    | 27 | transfer in or out can not be 0  | 
    |29|{params} must be entirely alpha-numeric characters| {param} 只允許英數   |
    |31|{params} must be a integer|
    |38|The cashtype is invalid | 此 api 操作不合法 |
    
11. ### <spin id="player-transfer-status">玩家轉帳狀態查詢</spin>
    
    ```
    GET /casino-api/player/credit/transfer-status?
        key=<key>&
        transferId=<transferId>&
        hash=<hash>
    ```
    
    #### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |transferId |平台方交易Id |string| 必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(transferId + secret)`**
    
    ---
    #### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  originCredit   | 交易前額度 |  decimal(19,4)  |
    |  addCredit   | 增加額度 |  integer  |
    |  finalCredit   | 交易後額度 |  decimal(19,4)  |
    |  transferId   | 平台方交易Id |  string  |
    |  orderId   | 此筆交易單號 |  integer  |
    |  status   | 交易狀態 |  smallint  |

    #### <span id="status">交易狀態</span>
    | 代碼  | status                  | 
    |---------- |-------------------------  |
    | 0         | 成功   | 
    ---

    #### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "originCredit":4201.6,
            "addCredit":500,
            "finalCredit":4701.6,
            "transferId":"AA99",
            "orderId":28,
            "status":0
        }
    }
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":1,
            "message":"transferId is required"
        }
    }
    ```

    #### 會出現的錯誤項目
    | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found         |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    |  10  |service not available |
    | 11 | {parameter} is invalid   |
    | 24 |{transferId} is not exist   |
    |29|{params} must be entirely alpha-numeric characters| 


12. ### <span id="bet-report">玩家下注查詢</span>

    ```
    GET /casino-api/bet/report?
        key=<key>&
        startAt=<startAt>&
        endAt=<endAt>&
        hash=<hash>
    ```
    
    ##### 目前使用分頁式，一頁1000筆

    #### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  startAt | 起始時間 |  string|必填，格式 2017-01-01 12:00:10    |
    |  endAt   | 結束時間 |  string  |必填，格式 2017-01-01 13:00:10    |
    |   page   | 分頁 |  int  |     選填，預設：1   |
    | pageSize| 分頁筆數 |  int  | 選填，預設：1000，若有輸入錯誤，會自動填入1000   |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(startAt + endAt + secret)`**
    ---
    #### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  total | 總筆數 |  integer  | 
    |  perPage| 各分頁含有筆數 |integer  |
    |  currentPage| 目前所在頁數 |integer  |
    |  lastPage|下一頁頁數 |integer  |
    |  previousPageUrl|上一頁 (null 表示為第一頁)  | string or null |
    |  nextPageUrl|下一頁 (null 表示無下一頁) | string or null  |
    |  betResult| [下注明細](#betResult 說明) | array |
    
    #### <span id="betResult">betResult 說明</span>
    
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  betFormId| 注單編號 | integer |
    |  gameType| [遊戲類別](#遊戲類別) | smallint  |
    |gameMethod |[遊戲玩法](#遊戲玩法)| smallint |
    |tableType |[桌台類型](#桌台類型)| smallint |
    | tableId | 遊戲局桌檯Id | string |
    | round | 局號 | integer |
    | run | 輪號| smallint |
    | gameResult |[開牌結果](#百家樂遊戲開牌代碼說明)，順序：[閒1,莊1,閒2,莊2,閒補,莊補]，若空的表示 無補牌 | string |
    | playerId | 遊戲方玩家Id | integer |
    | account | 玩家帳號 | string |
    | amount | 總有效下注注額 | integer |
    | betList | 下注注區列表 | string(json) |
    | checkoutAmount | 結帳金額 | decimal(19,4) |
    | betTime | 當局最後一筆下注時間 | string |
    | billingDate | 結帳日 | string |
    | modifiedStatus | [注單狀態](#注單狀態) | smallint |
    | updatedAt | 更新時間 | string |
    | createdAt | 結帳時間 | string |
    
    ---
    
    ### <span id="gameMethods">遊戲玩法</span>
    | 名稱  | gameMethods                  | 
    |---------- |-------------------------  |
    | 百家樂標準         | 1   | 
    | 百家樂西洋         | 2   |
    | 百家樂免水         | 3   |
    
    ### <span id="tableType">桌台類型</span>
    | 名稱  | tableType                  | 
    |---------- |-------------------------  |
    | 標準百家樂         | 1   | 
    | 先發百家樂         | 2   |
    | 極速百家樂         | 3   |
    | 眯牌百家樂         | 4   |
    
    ### <span id="gameResultDescription">百家樂遊戲開牌代碼說明</span>
    |  牌例 |  對應                 | 
    |---------- |-------------------------  |
    | S1   | 黑桃 A   | 
    | H0   | 紅心 10   |
    | DJ   | 方塊 J   |
    | C6   | 梅花 6  |
    
    ### <span id="status">注單狀態</span>
    |  狀態 |  status               | 
    |---------- |-------------------------  |
    | 0  | 正常   | 
    | 1  | 改單   |
    | 2   | 取消單   |
    
    #### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "total":1,
            "perPage":1000,
            "currentPage":1,
            "lastPage":1,
            "previousPageUrl":null,
            "nextPageUrl":null,
            "betResult":[{
                "betFormId":299,
                "gameType":1,
                "gameMethod":1,
                "tableType":3,
                "tableId":"A",
                "round":1658620520,
                "run":4,
                "gameResult":"C1,CJ,DJ,H1,C7,C7",
                "playerId":26,
                "account":"EddyCount",
                "amount":1000,
                "betList":[{"spotId":18,"spotName":"BankerJQKA","betAmount":1000,"loseWinAmount":14000,"odds":14}],
                "checkoutAmount":"14000.0000",
                "betTime":"2017-08-25 16:30:09",
                "billingDate":"2017-08-26",
                "modifiedStatus":0,
                "updatedAt":"2017-08-25 16:31:24",
                "createdAt":"2017-08-25 16:31:24"}]
        }
    }  
              
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":23,
            "message":"[startAt or endAt] value must be datetime Example：2017-01-01 00:00:00"
        }
    }
    ```
   
    #### 會出現的錯誤項目
    | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 23 | [startAt or  EndAt] value must be datetime Example：2017-01-01 00:00:00   | 查詢玩家注單，時間參數必須使用規定格式       |

13. #### <span id="bet-report-multiple">玩家下注簡報查詢</span>

    ```
    GET /casino-api/bet/report-multiple?
        key=<key>&
        startAt=<startAt>&
        endAt=<endAt>&
        hash=<hash>
    ```
    
    #### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  startAt   | 起始時間 |  string  |     必填，格式 2017-01-01 12:00:10    |
    |  endAt   | 結束時間 |  string  |     必填，格式 2017-01-01 13:00:10    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(startAt + endAt + secret)`**
    
    ---
    #### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  betFormCount | 注單數量 |integer  |
    |  totalAmount | 總下注額度 |integer  |
    |  totalLoseWinAmount | 總輸贏 | decimal(19,4)  |
        
    ---

    #### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":[
            {
                "account":"a1234",
                "betFormCount":13,
                "totalAmount":2000,
                "totalLoseWinAmount":1000.88,
            },
            {
                "account":"a129995b",
                "betFormCount":67,
                "totalAmount":563900,
                "totalLoseWinAmount":-10647.6,
            },
        ]
    }
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":23,
            "message":"[startAt or endAt] value must be datetime Example：2017-01-01 00:00:00"
        }
    }
    ```

    #### 會出現的錯誤項目
    | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 23 | [startAt or  EndAt] value must be datetime Example：2017-01-01 00:00:00   | 查詢玩家注單，時間參數必須使用規定格式       |
    
14. #### <span id="player-kick">踢玩家</span>

    ```
    DELETE /casino-api/player/kick?
        key=<key>&
        account=<account>&
        reason=<reason>&
        hash=<hash>
    ```
    
    #### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 遊戲帳號 |  string  |     必填    |
    |  reason   | 原因 |  string  |     非必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + secret)`**
    ---
    #### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  status   | [帳號處理狀況](#帳號處理狀況)|  smallint  |
    ---

    ### <span id="status">帳號處理狀況</span>
    | 狀態代碼 | status                  | 
    |---------- |-------------------------  |
    | 0 | kick success  | 
    | 1 | player is not online | 


    #### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "status":1
        }
    }
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
    ```
    
    
    #### 會出現的錯誤項目
    | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found            |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    |  10  |service not available |
    | 11 | {parameter} is invalid   |
   
15. #### <span id="player-kick-multiple">踢多玩家</span>

    ```
    DELETE /casino-api/player/kick-multiple?
        key=<key>&
        account=<account>&
        reason=<reason>&
        hash=<hash>
    ```
    
    #### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 遊戲帳號 |  string  |     必填，多玩家使用 `,` 號隔開   |
    |  reason   | 原因 |  string  |     非必填    |
    |   hash   | 驗證參數 |  string  |     必填    |
    
    #### **`hash = md5(account + secret)`**
    ---
    #### Response 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號 |  string  | 
    |  status   | [多玩家帳號處理狀況](#多玩家帳號處理狀況)|  smallint  |
    ---

    ### <span id="status">多玩家帳號處理狀況</span>
    | 狀態代碼 | status                  | 
    |---------- |-------------------------  |
    | 0 | kick success  | 
    | 1 | player is not online | 
    | 2 | player not found |
    
    #### Response 結果
    
    成功
    
    ```javascript
    {
        "status":"success",
        "data":[
            {
                "account":"a1234",
                "status":0
            },
            {
                "account":"abc1234",
                "status":1
            },
            {
                "account":"bb8899",
                "status":2
            },
        ]
    }
    ```

    失敗

    ```javascript
    {
        "status":"error",
        "error":{
            "code":1,
            "message":"account is required"
        }
    }
    ```
    
    #### 會出現的錯誤項目
    | 錯誤代碼 | 錯誤說明 |     
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    |  10  |service not available |
    | 11 | {parameter} is invalid   |

3. ## <span id="player-credit-set">設定信用玩家額度</span>

    ```
    PUT /casino-api/player/credit?
        key=<key>&
        account=<account>&
        credit=<credit>&
        hash=<hash>
    ```

    #### *限信用平台使用

    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  credit | 額度 |  decimal(19,4)  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |

    #### **`hash = md5(account + credit + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號|  string  |
    |  credit | 額度|  decimal(19,4)  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "credit":4101.0000
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found            |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    |30|{params} must be a unsigned decimal| {param} 只允許正數的 decimal   |
    |38|The cashtype is invalid | 此 api 操作不合法 |

3. ## <span id="player-credit-info">查詢信用玩家額度</span>

    ```
    GET /casino-api/player/credit?
        key=<key>&
        account=<account>&
        hash=<hash>
    ```
    
    #### *限信用平台使用
    
    ### Request 參數說明

    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |

    #### **`hash = md5(account + credit + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號|  string  |
    |  credit | 額度|  decimal(19,4)  |
     |  currentCredit | 額度|  decimal(19,4)  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"a1234",
            "credit":5000.0000,
            "currentCredit":4101.0000
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found            |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    |38|The cashtype is invalid | 此 api 操作不合法 |

3. ## <span id="player-credit-reset">重設信用玩家額度</span>

    ```
    PUT /casino-api/credit/reset?
        key=<key>&
        callback=<callback>&
        hash=<hash>
    ```

    #### *限信用平台使用
    
    ### Request 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  callback | 執行完後通知平台 url |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |

    #### **`hash = md5(callback + secret)`**
    ---
    ### Response 參數說明
    無

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "recordId":12
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":3,
            "message":"key is invalid"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    |38|The cashtype is invalid | 此 api 操作不合法 |
    |39|The credit reset action is padding |
    
3. ## <span id="stake-limit-query">查詢注區範本</span>

    ```
    GET /casino-api/stake-limit-list?
        key=<key>&
        currency=<currency>&
        tableType=<tableType>&
        hash=<hash>
    ```

    ### Request 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  currency | [支援幣別](#支援幣別) |  string  |     必填    |
    |  tableType | [注區範本遊戲類別](#注區範本遊戲類別) |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |

    #### **`hash = md5(currency + tableType + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |
    |:--------:|:--------:|:--------:|
    |  stakeLimitId | 範本Id|  integer  |
    |  min | 最小下注值|  integer  |
    |  max | 最大下注值|  integer  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        {
            "status":"success",
            "data":[
                {"stakeListId":110,"min":50,"max":1000},
                {"stakeListId":111,"min":50,"max":2000},
                {"stakeListId":112,"min":100,"max":5000},
                {"stakeListId":118,"min":200,"max":10000},
                {"stakeListId":113,"min":200,"max":20000},
                {"stakeListId":119,"min":200,"max":30000},
                {"stakeListId":114,"min":500,"max":50000},
                {"stakeListId":115,"min":500,"max":100000},
                {"stakeListId":99,"min":50,"max":200000},
                {"stakeListId":116,"min":500,"max":200000},
                {"stakeListId":117,"min":1000,"max":400000}
            ]
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":3,
            "message":"key is invalid"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 34 | tableType:{tableType} not found|
    | 102 | The currency:{currency} is not supported|

3. ## <span id="player-stake-limit-setting-query">玩家注區範本設定查詢</span>

    ```
    GET /casino-api/player/stake-limit?
        key=<key>&
        account=<account>&
        tableType=<tableType>&
        hash=<hash>
    ```

    ### Request 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  tableType | [注區範本遊戲類別](#注區範本遊戲類別) |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |

    #### **`hash = md5(account + tableType + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號|  string  |
    |  tableType | [注區範本遊戲類別](#注區範本遊戲類別)  |  string  |
    |  stakeLimitValue | 玩家所設定範本 |  string  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"test001",
            "stakeLimitValue":"110,112,113"
        }
    }
    ```

    失敗

   ```javascript
   {
        "status":"error",
        "error":{
            "code":4,
            "message":"player not found"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found          |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 34 | tableType:{tableType} not found|

3. ## <span id="player-stake-limit-setting-query">玩家注區範本設定</span>

    ```
    PUT /casino-api/player/stake-limit?
        key=<key>&
        account=<account>&
        tableType=<tableType>&
        stakeLimitValue=<stakeLimitValue>&
        hash=<hash>
    ```

    ### Request 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     說明    |
    |:--------:|:--------:|:--------:|:-----------:|
    |    key   | 服務金鑰 |  string  | 由API端提供 |
    |  account | 玩家帳號 |  string  |     必填    |
    |  tableType | [注區範本遊戲類別](#注區範本遊戲類別) |  string  |     必填    |
    |  stakeLimitValue | 設定玩家幣別能使用的範本Id，多筆請用`,` 號 |  string  |     必填    |
    |   hash   | 驗證參數 |  string  |     必填    |

    #### **`hash = md5(account + tableType + stakeLimitValue + secret)`**
    ---
    ### Response 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |
    |:--------:|:--------:|:--------:|
    |  account | 玩家帳號|  string  |
    |  tableType | [注區範本遊戲類別](#注區範本遊戲類別)  |  string  |
    |  stakeLimitValue | 玩家所設定範本 |  string  |

    ---

    ### Response 結果
    成功

    ```javascript
    {
        "status":"success",
        "data":{
            "account":"test001",
            "tableType":4,
            "stakeLimitValue":"110,112,113,115"
        }
    }
    ```

    失敗

   ```javascript
    {
        "status":"error",
        "error":{
            "code":36,
            "message":
            "player stake limit setting value [133] is invalid"
        }
    }
   ```

    #### 會出現的錯誤項目
   | 錯誤代碼 | 錯誤說明 |
    |:--------:|:--------:|
    | 1  | {parameter} is required   |
    | 2  | key is invalid            |
    | 3  | hash is invalid           |
    | 4  | player not found          |
    | 5  | {method} is not allowed   |
    |  7  | internal server error |
    | 11 | {parameter} is invalid   |
    | 34 | tableType:{tableType} not found|
    | 35 | player stake limit setting max five count|
    | 36 | player stake limit setting value [{invalid stakeLimitValue}] is invalid|
    |40|{param} must be a unsigned integer, and only numeric characters | 

3. ## <span id="app-api">手機API串接</span>

    ###### scheme url
    
    ```
    pharao-casino-mobile://launch-game?
        token=eyJpdiI6Im9kYTk1WVFlaVRyZm5..&
        lang=zh_TW
    ```

    ### Request 參數說明
    | 參數名稱 | 參數說明 | 參數型態 |     說明    |   必填    |
    |:--------:|:--------:|:--------:|:-----------:|:-----------:|
    |    token   | 從[取得玩家登入網址](#取得玩家登入網址)取得的token |  string  | 用來驗證玩家 |Y|
    |  lang | [支援語系](#支援語系) |  string  |     遊戲內使用語系    |Y|

