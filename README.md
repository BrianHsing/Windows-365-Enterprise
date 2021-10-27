# Windows 365
Windows 365 是微軟推出的軟體及服務，主要提供虛擬桌面基礎架構解決方案，是基於 Azure 虛擬桌面的成功後，讓企業能夠更簡單快速的方式，建立屬於自己的混合工作環境，面對天災人禍、疫情、設備資源不足的挑戰。本篇會帶領讀者實際使用 Windows 365 企業版，並且模擬地端的環境進行實作，透過手把手的步驟說明，讓讀者學會如何佈署與管理。<br>

## Windows 365 與 Azure 虛擬桌面的比較
- Windows 365 商務版<br>
  - 授權：Windows 365 商務版<br>
  - 基礎架構需求：不需要，無法整合地端網路<br>
  - 身分驗證：Azure AD<br>
  - 管理：Microsoft 365 管理中心<br>
  - 用途：雲端個人電腦<br>
  - 價格預估：依據使用者數量固定費用<br>
- Windows 365 企業版<br>
  - 授權：<br>
    - 如果使用者的存取裝置為 Windows Pro 或以上版本：Windows 10 E3 + EMS E3/E5 或 M365 F3/E3/E5/BP<br>
    - 如果使用者的存取裝置使用其他作業系統：Win VDA E3 + EMS E3/E5 或 M365 F3/E3/F5/BP <br>
  - 基礎架構需求：需要 Azure Subscription，並且建立 Azure 虛擬網路，用於連線至 Azure 虛擬網路或地端的 Windows AD 進行驗證<br>
  - 身分驗證：Azure AD、Azure AD Hybrid Join、Windows AD<br>
  - 管理：Microsoft Endpoint Manager<br>
  - 用途：雲端個人電腦，可以整合地端環境，並且能透過 Azure 虛擬網路進行網路控制<br>
  - 價格預估：依據使用者數量固定費用<br>
https://docs.microsoft.com/zh-tw/windows-365/enterprise/overview<br>
- Azure 虛擬桌面<br>
  - 授權：M365 F3/E3/E5/BP<br>
  - 基礎架構需求：需要 Azure Subscription、並且建立 Azure 虛擬網路、Azure 檔案、工作階段主機。<br>
  - 身分驗證：下列選項均可獨立選擇<br>
    - 僅需要 Azure AD<br>
    - Azure AD + Azure AD Domain Services<br>
    - Azure AD + Windows AD<br>
  - 管理：Microsoft Endpoint Manager 或 Windows AD<br>
  - 用途：雲端個人電腦或共用集區，可彈性整合地端與多個區域，並且最有效利用資源<br>
  - 價格預估：依據需求彈性變化<br>
https://docs.microsoft.com/zh-tw/azure/virtual-desktop/overview<br>

## Windows 365 企業版部署必要條件

- 確認擁有 Azure 訂用帳戶，本篇使用 Visual Studio 訂用帳戶<br>
  - 擁有訂用帳戶擁有者權限、Azure AD 全域管理員<br>
  - 指派 Windows 365 權限，非別為訂用帳戶讀者、資源群組網路參與者、虛擬網路網路參與者<br>
  - 需要建立 Azure 虛擬網路<br>
  - 需要建立 Azure VM 模擬 Windows AD<br>
  - 需要建立 Azure AD Hybrid Join<br>
- 確認擁有相對應的 Windows 365 與 Microsoft 授權 (需要包含 Azure AD P1、Microsoft Endpoint Manager)<br>
  - 本篇使用 Microsoft 365 F3 搭配 Windows 365 Enterprise 4 vCPU, 16 GB, 128 GB<br>

## Lab 實戰演練

- [Lab 1 - 模擬地端 Windows AD 與網路環境](https://github.com/BrianHsing/Windows365/blob/main/Lab1.md)<br>
- [Lab 2 - 指派授權與設定權限](https://github.com/BrianHsing/Windows365/blob/main/Lab2.md)<br>
- [Lab 3 - 建立虛擬網路連線至模擬的環境](https://github.com/BrianHsing/Windows365/blob/main/Lab3.md)<br>
- [Lab 4 - 建立自訂映像檔](https://github.com/BrianHsing/Windows365/blob/main/Lab4.md)<br>
- [Lab 5 - 建立佈建原則](https://github.com/BrianHsing/Windows365/blob/main/Lab5.md)<br>
- [Lab 6 - Cloud PC 存取](https://github.com/BrianHsing/Windows365/blob/main/Lab6.md)<br>
- [Lab 7 - 設定條件式存取並開啟多重要素驗證](https://github.com/BrianHsing/Windows365/blob/main/Lab7.md)<br>
- [Lab 8 - MSIX 應用程式指派](https://github.com/BrianHsing/Windows365/blob/main/Lab8.md)<br>
- [Lab 9 - 分析報告](https://github.com/BrianHsing/Windows365/blob/main/Lab9.md)<br>

## 參考資料
- Windows 365 常見問題集<br>
  https://www.microsoft.com/zh-tw/windows-365/faq<br>
