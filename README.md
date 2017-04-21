# DroiBaaS-SDK-Unity3D

- core 
存放歷史sdk
- release
存放最新版sdk


# DroiBaaS Unity3D快速入門

## 簡介
[DroiBaaS][droibaas]對於Unity3D開發人員提供方便使用的C#函式庫。讓Unity3D程式開發人員也可以使用最簡單的方式存取雲端資料庫以及相關的線上功能。

## 快速入門
----
### 環境需求
- Unity3D 5.4以上環境
>> 由於Unity3D 5.4提供的UnityWebRequest不支援gzip壓縮內容。當開發人員使用5.4版時，DroiCoreSDK將不會開啟gzip傳輸。不開啟壓縮的結果會造成資料傳輸量大增。

### SDK安裝步驟
由於[DroiBaaS][droibaas]是使用C#搭配Native Plugins撰寫而成，除了DLL外, 您也須引入對應平台的Native Plugins。
開發人員可以依照以下的步驟將[DroiBaaS][droibaas] Unity3D Core SDK增加至原專案之中  
  1. 下載 [DroiBaaS Core SDK for Unity3D](https://github.com/DroiBaaS/DroiBaaS-SDK-Unity3D/blob/master/release/sdk.unitypackage)  
  2. 直接將檔案匯入至原來的Project之中
>> 針對iOS xcode project, 可使用 Assets/Editor/Droi/DroiBuildPostprocessor.cs自動設定以下參數

  - Linked Framworks and Libraries 新增 ***libz.tbd***
  - Build Settings->Other Linker Flags 加入 ***-ObjC***

>> 匯出iOS專案時, 若backend language選擇il2cpp, 也須加入Assets/Editor/Droi/link.xml避免strip DroiCoreSDK

### 測試DroiBaaS Core SDK for Unity3D
在使用任何功能之中，你需要先至[DroiBaaS網站](http://www.droibaas.com)申請帳號並創建一個新的程式，得到app id以供測試使用。使用如下的程式碼，新增一筆資料至雲端資料庫

```c#
	// 初始化Core SDK，其中applicationId為申請到的唯一碼，
	DroiCore.initializeCore ( "applicationId" );

	// 新增一筆資料，表格名稱為ScoreTable
	DroiObject score = new DroiObject ("ScoreTable");
	score.put ("name", "John");
	score.put ("score", 99);
	
	// 使用Coroutine方式儲存資料
	StartCoroutine ( score.saveCoroutine ( ((bool res, DroiError error) => {
		if ( error.isOk() )
			Debug.Log( "saveData OK" );	
	} ) ) );

```  
