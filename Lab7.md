# Lab 7 - 設定條件式存取並開啟多重要素驗證

## 設定條件式存取並開啟多重要素驗證

- 畫面登入`portal.azure.com`，瀏覽至「Azure Active Directory」，選擇左邊功能欄「安全性」，跳轉畫面後，在選擇左欄「條件式存取」，看到此畫面後，再點選「新增原則」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca1.png "ca1")<br>
- 命名原則，在工作分派下「使用者和群組」的部分選擇 w365_group<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca2.png "ca2")<br>
- 在「雲端應用程式或動作」的部分選擇 Windows 365<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca3.png "ca3")<br>
- 在「條件」的部分，點選「用戶端應用程式」，設定選擇「是」，新式驗證用戶端下方的「瀏覽器」、「行動裝置 App 及桌面用戶端均勾選」，之後點選「完成」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca4.png "ca4")<br>
- 在「授與」的部分，點選「授與存取權」，勾選需要「多重要素驗證」，針對多個控制項選擇「需要所有選取的控制項」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca5.png "ca5")<br>
- 在「工作階段」的部分，點選「登入頻率」，輸入「1」，單位選擇「小時」，如果登入時間是在１小時之後則會需要多重要素驗證<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca6.png "ca6")<br>
- 確認您的設定，並將「啟用原則」設定為「開啟」，最後點選建立<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca6.png "ca7")<br>

## 驗證使用者是否生效與初始設定

- 開啟瀏覽器，輸入`windows365.microsoft.com`，並且登入有授權的帳號，本篇使用 user1<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/login.png "login")<br>
- 點選 open in browser，開啟 Cloud PC，這邊會需要登入 user1<br>
- 登入後，會提醒使用者需要更多資訊，才能保護帳戶的安全，點選「下一步」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca6.png "ca8")<br>
- 跳轉畫面後，使用者就會需要遵循步驟進行相關驗證，您可以選擇使用簡訊或行動應用程式<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca9.png "ca9")<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca10.png "ca10")<br>
- 本篇選擇使用行動應用程式操作，點選「接收驗證的通知」後，點選設定<br>
- 這時會跳出畫面，請遵循上述步驟進行安裝行動應用程式與驗證<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca11.png "ca11")<br>
- 行動裝置畫面，安裝之後開啟應用程式，選擇「新增帳戶」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca12-1.png "ca12")<br>
- 選擇「工作或學校帳戶」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca13-1.png "ca13")<br>
- 點選「掃描 QR 代碼」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca14-1.png "ca14")<br>
- 掃描後會出現相關資訊，點選完成<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca15-1.png "ca15")<br>
- 完成後即可看到有出現使用者的帳戶<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca16-1.png "ca16")<br>
- 回到網頁的畫面，可以看到下一步已經可以點選，點選「下一步」<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca17.png "ca17")<br>
- 這個時候會需要驗證，行動裝置會出現核准登入的提示<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca18.png "ca18")<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca20-1.png "ca20-1")<br>
- 最後一步驟是要求您填寫行動裝置電話，預防您遺失行動應用程式的存取權，這一步完成就結束整個步驟<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca19.png "ca19")<br>
- 完成後會登入至 Windows 365，後續使用者就可以使用多重要素驗證保護帳號安裝<br>
  ![GITHUB](https://github.com/BrianHsing/Windows365/blob/main/images/ca21.png "ca21")<br>
  
前往[Lab 8 - 應用程式指派](https://github.com/BrianHsing/Windows365/blob/main/Lab8.md)<br>