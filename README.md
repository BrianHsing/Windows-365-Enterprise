# Windows 365
Windows 365 是微軟推出的軟體及服務，主要提供虛擬桌面基礎架構解決方案，是基於 Azure 虛擬桌面的成功後，讓企業能夠更簡單快速的方式，建立屬於自己的混合工作環境，面對天災人禍、疫情、設備資源不足的挑戰。本篇會帶領讀者實際使用 Windows 365 企業版，透過手把手的步驟說明，讓讀者學會如何佈署與管理。<br>

# Windows 365 與 Azure 虛擬桌面的先決條件比較
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
- Azure 虛擬桌面<br>
  - 授權：M365 F3/E3/E5/BP<br>
  - 基礎架構需求：需要 Azure Subscription、並且建立 Azure 虛擬網路、Azure 檔案、工作階段主機。<br>
  - 身分驗證：下列選項均可獨立選擇<br>
    - 僅需要 Azure AD<br>
    - Azure AD + Azure AD Domain Services<br>
    - Azure AD + Windows AD<br>
  - 管理：Microsoft Endpoint Manager 或 Windows AD<br>
  - 用途：雲端個人電腦或共用集區<br>
  - 價格預估：依據需求彈性變化<br>