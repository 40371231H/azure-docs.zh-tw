---
title: "IoT DevKit 到雲端：將 IoT DevKit AZ3166 連線到 Azure IoT 中樞 | Microsoft Docs"
description: "在本教學課程中了解如何設定 IoT DevKit AZ3166 並將其連線到 Azure IoT 中樞，以便它可以將資料傳送到 Azure 雲端平台。"
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: xshi
ms.translationtype: HT
ms.sourcegitcommit: eeed445631885093a8e1799a8a5e1bcc69214fe6
ms.openlocfilehash: 253a2d34ea5b3f4f8253900be27c54fe5ca1dacf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="connect-iot-devkit-az3166-to-azure-iot-hub-in-the-cloud"></a>將 IoT DevKit AZ3166 連線到雲端中的 Azure IoT 中樞

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

您可以使用 [MXChip IoT DevKit](https://microsoft.github.io/azure-iot-developer-kit/) 來開發及設定運用 Microsoft Azure 服務的物聯網 (IoT) 解決方案原型。 其包含具有豐富週邊設備與感應器的 Arduino 相容開發板、開放原始碼開發板套件，以及不斷擴展的[專案目錄](https://microsoft.github.io/azure-iot-developer-kit/docs/projects/)。

## <a name="what-you-do"></a>您要做什麼
將 [DevKit](https://microsoft.github.io/azure-iot-developer-kit/) 連線到您建立的 Azure IoT 中樞，收集來自感應器的溫度與溼度，並傳送資料至 IoT 中樞。

還沒有 DevKit 嗎？ [立即買一個](https://aka.ms/iot-devkit-purchase)。

## <a name="what-you-learn"></a>您學到什麼

* 如何將 IoT DevKit 連線到無線存取點以及準備您的開發環境。
* 如何建立 IoT 中樞並註冊 MXChip IoT DevKit 適用的裝置。
* 如何在 MXChip IoT DevKit 上執行範例應用程式來收集感應器資料。
* 如何將感應器資料傳送至 IoT 中樞。

## <a name="what-you-need"></a>您需要什麼

* 附有 Micro-USB 傳輸線的 MXChip IoT DevKit 開發板。 [立即買一個](https://aka.ms/iot-devkit-purchase)。
* 執行 Windows 10 或 macOS 10.10+ 的電腦。
* 有效的 Azure 訂用帳戶。 [啟動 30 天免費試用 Microsoft Azure 帳戶](https://azureinfo.microsoft.com/us-freetrial.html)。
  

## <a name="prepare-your-hardware"></a>準備硬體

將硬體連接到您的電腦。

您需要此硬體：

* DevKit 面板
* Micro-USB 傳輸線

![必要的硬體](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/hardware.jpg)

若要將 DevKit 連線到電腦：

1. 將 USB 端連線到電腦。
2. 將 Micro-USB 端連線到 DevKit。
3. 綠色的電源 LED 燈可確認連線成功。

![硬體連線](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect.jpg)

## <a name="configure-wi-fi"></a>設定 Wi-Fi

IoT 專案依賴網際網路連線。 請使用下列指示設定 DevKit，使其連線至 Wi-Fi。

### <a name="enter-ap-mode"></a>進入 AP 模式

按住按鈕 B，按下再放開 [Reset] 按鈕，然後放開按鈕 B。DevKit 會進入 AP 模式以供設定 Wi-Fi。 此畫面會顯示 DevKit 的服務組識別碼 (SSID) 以及設定入口網站 IP 位址。

![Reset 按鈕、按鈕 B 和 SSID](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ap.jpg)

### <a name="connect-to-devkit-ap"></a>連線至 DevKit AP

現在，使用另一個已啟用 Wi-Fi 的裝置 (電腦或行動電話) 來連線至 DevKit SSID (上圖中以紅框特別標示者)。 密碼則保持空白。

![網路資訊和 [連線] 按鈕](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/connect-ssid.png)

### <a name="configure-wi-fi-for-the-devkit"></a>為 DevKit 設定 Wi-Fi

在電腦或行動電話的瀏覽器上開啟 DevKit 畫面中所顯示的 IP 位址，選取您希望 DevKit 連線的 Wi-Fi 網路，然後輸入密碼。 選取 [ **連接**]。

![[密碼] 方塊和 [連線] 按鈕](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-portal.png)

連線成功後，DevKit 會在幾秒內重新啟動。 然後，您會在畫面上看到 Wi-Fi 名稱和 IP 位址：

![Wi-Fi 名稱和 IP 位址](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/wifi-ip.jpg)

> [!NOTE] 
> 圖中顯示的 IP 位址未必會符合 DevKit 畫面上所指派和顯示的實際 IP 位址。 這是正常現象，因為 Wi-Fi 會使用 DHCP 來動態指派 IP。

設定好 Wi-Fi 後，即使將裝置的接線拔除，該裝置上仍會留有用於該連線的認證。 例如，如果您為 DevKit 設定了家中的 Wi-Fi，然後將 DevKit 帶到辦公室，您必須重新設定 AP 模式 (從＜進入 AP 模式＞一節的步驟開始) 以將 DevKit 連線至辦公室的 Wi-Fi。 

## <a name="start-using-the-devkit"></a>開始使用 DevKit

在 DevKit 上執行的預設應用程式會檢查最新版本的韌體，並對您顯示某些感應器診斷資料。

### <a name="upgrade-to-the-latest-firmware"></a>升級至最新的韌體

如果您需要升級韌體，畫面會顯示目前的和最新的韌體版本。 若要升級，請遵循[升級韌體](https://microsoft.github.io/azure-iot-developer-kit/docs/upgrading/)指南。

![顯示目前的和最新的韌體版本](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/firmware.jpg)

> [!NOTE] 
> 這項工作只需執行一次。 在 DevKit 上開始進行開發並上傳應用程式後，最新的韌體就會隨著應用程式一起進入開發板中。

### <a name="test-various-sensors"></a>測試各種感應器

按下按鈕 B 來測試感應器。 不斷按下再放開 B 按鈕，以循環測試各個感應器。

![按鈕 B 和感應器顯示](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/sensors.jpg)

## <a name="prepare-the-development-environment"></a>準備開發環境

現在可以設定開發環境：工具與封裝可讓您建立令人驚嘆的 IoT 應用程式。 您可以根據您的作業系統選擇 Windows 或 macOS 版本。


### <a name="windows"></a>Windows

建議您使用安裝封裝以準備開發環境。 如果遇到任何問題，可以依照[手動步驟](https://microsoft.github.io/azure-iot-developer-kit/docs/installation/)來完成準備。

#### <a name="download-the-latest-package"></a>下載最新套件

您下載的 .zip 檔案包含進行 DevKit 開發所需的所有必要工具和套件。

> [!div class="button"]
[下載](https://azureboard.azureedge.net/prod/installpackage/devkit_install_1.0.2.zip)


.zip 檔案包含下列工具和套件。 如果您已安裝某些元件，指令碼將會偵測到並跳過它們。

* Node.js 和 Yarn：安裝指令碼和自動化工作的執行階段。
* [Azure CLI 2.0 MSI](https://docs.microsoft.com//cli/azure/install-azure-cli#windows)：用來管理 Azure 資源的跨平台命令列體驗。 此 MSI 包含相依的 Python 和 pip。
* [Visual Studio Code](https://code.visualstudio.com/) (VS Code)：用來開發 DevKit 的輕量型程式碼編輯器。
* [適用於 Arduino 的 Visual Studio Code 擴充功能](https://marketplace.visualstudio.com/items?itemName=vsciot-vscode.vscode-arduino)：此擴充功能可讓您在 Visual Studio Code 中開發 Arduino。
* [Arduino IDE](https://www.arduino.cc/en/Main/Software)：適用於 Arduino 的擴充功能需依賴此工具。
* DevKit 開發板套件：DevKit 的工具鏈、程式庫和專案。
* ST-Link 公用程式：基本工具和驅動程式。

#### <a name="run-the-installation-script"></a>執行安裝指令碼

在 [Windows 檔案總管] 中，找出 .zip 檔案並將它解壓縮。 尋找 install.cmd，用滑鼠右鍵按一下，然後選取 [以系統管理員身分執行]。

![檔案總管](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/run-admin.png)

在安裝期間，您會看到每個工具或套件的安裝進度。

![安裝進度](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/install.png)

#### <a name="install-drivers"></a>安裝驅動程式

適用於 Arduino 的 VS Code 擴充功能依賴 Arduino IDE。 如果這是您第一次安裝 Arduino IDE，系統會提示您安裝相關的驅動程式：

![getting-started-driver](media/iot-hub-arduino-devkit-az3166-get-started/getting-started/driver.png)

安裝所需時間約為 10 分鐘，視您的網際網路速度而定。 安裝完成之後，您應該會在桌面上看到 Visual Studio Code 和 Arduino IDE 的捷徑。

> [!NOTE] 
> 有時在您啟動 VS Code 時，系統會出現錯誤提示，指出找不到 Arduino IDE 或相關開發板套件。 請關閉 VS Code，然後重新啟動 Arduino IDE。 VS Code 接著應該就會正確找到 Arduino IDE 路徑。


### <a name="macos-preview"></a>macOS (預覽)

請遵循下列步驟以在 macOS 上準備開發環境。

#### <a name="install-azure-cli-20"></a>安裝 Azure CLI 2.0

1. 使用一個 `curl` 命令來安裝 Azure CLI 2.0：

   ```bash
   curl -L https://aka.ms/InstallAzureCli | bash
   ```

2. 重新啟動命令殼層以讓變更生效：

   ```bash
   exec -l $SHELL
   ```

如需安裝 Azure CLI 2.0 的詳細資訊，請參閱[官方指南](https://docs.microsoft.com//cli/azure/install-azure-cli)。

#### <a name="install-the-arduino-ide"></a>安裝 Arduino IDE

Visual Studio Code Arduino 擴充功能依賴 Arduino IDE。 下載並安裝[適用於 macOS 的 Arduino IDE](https://www.arduino.cc/en/Main/Software)。

#### <a name="install-visual-studio-code"></a>安裝 Visual Studio Code

下載並安裝[適用於 macOS 的 Visual Studio Code](https://code.visualstudio.com/)。 這是用來建置 DevKit IoT 應用程式的主要開發工具。

####  <a name="download-the-latest-package"></a>下載最新套件

1. 安裝 Node.js。 您可以使用熱門的 macOS 套件管理員 [Homebrew](https://brew.sh/) 或[預先建置的安裝程式](https://nodejs.org/en/download/)來進行安裝。

2. 下載 .zip 檔案 (內含要在 VS Code 上開發 DevKit 所需的工作指令碼)。

   > [!div class="button"]
   [下載](https://azureboard.azureedge.net/installpackage/devkit_tasks_1.0.2.zip)

3. 找到 .zip 檔並將其解壓縮。 然後啟動**終端機**應用程式並執行下列命令：

   a. 將解壓縮的資料夾移動至您的 macOS 使用者資料夾：
      ```bash
      mv [.zip extracted folder]/azure-board-cli ~/. ; cd ~/azure-board-cli
      ```
  
   b. 安裝 npm 套件：
      ```
      npm install
      ```

#### <a name="install-the-vs-code-extension-for-arduino"></a>安裝適用於 Arduino 的 VS Code 擴充功能

您可以直接在 Visual Studio Code 中安裝 Azure Marketplace 擴充功能。 在左窗格中選取擴充功能圖示，搜尋 **Arduino**，然後選取 [安裝]：

![尋找 Arduino 擴充功能](media/iot-hub-arduino-devkit-az3166-get-started/installation-extensions-mac.png)

#### <a name="install-the-devkit-board-package"></a>安裝 DevKit 開發板套件

使用 Visual Studio Code 中的 Board Manager 來新增 DevKit 開發板。

1. 使用 Cmd+Shift+P 開啟命令選擇區，輸入 **Arduino**，然後尋找並選取 [Arduino: Board Manager]。

2. 選取右下方的 [其他 URL]。
   ![其他 URL 連結](media/iot-hub-arduino-devkit-az3166-get-started/installation-additional-urls-mac.png)

3. 在 settings.json 檔案中，於 [使用者設定] 窗格底部新增一行，然後儲存。
   ```json
   "arduino.additionalUrls": "https://raw.githubusercontent.com/VSChina/azureiotdevkit_tools/master/package_azureboard_index.json"
   ```
   ![新增至 [使用者設定] 窗格的程式碼](media/iot-hub-arduino-devkit-az3166-get-started/installation-settings-json-mac.png)

4. 在 Board Manager 中搜尋 **az3166** 並安裝最新版本。
   ![安裝 az3166](media/iot-hub-arduino-devkit-az3166-get-started/installation-az3166-mac.png)

您現在已具備安裝 macOS 的所有必要工具與封裝。


## <a name="open-the-project-folder"></a>開啟專案資料夾

### <a name="start-vs-code"></a>啟動 VS Code

請確定 DevKit 未連線。 先啟動 VS Code，然後將 DevKit 連線至您的電腦。 VS Code 會自動尋找 DevKit，並開啟簡介頁面：

![[簡介] 頁面](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-vscode.png)

> [!NOTE] 
> 有時在您啟動 VS Code 時，系統會出現錯誤提示，指出找不到 Arduino IDE 或相關開發板套件。 請關閉 VS Code，然後重新啟動 Arduino IDE。 VS Code 接著應該就會正確找到 Arduino IDE 路徑。


### <a name="open-the-arduino-examples-folder"></a>開啟 Arduino 範例資料夾

在 [Arduino 範例] 索引標籤上，瀏覽至 [MXCHIP AZ3166 的範例] > [AzureIoT]，然後選取 [GetStarted]。

![[Arduino 範例] 索引標籤](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution-examples.png)

如果您不小心關閉該窗格，可予以重新開啟。 使用 Ctrl+Shift+P (macOS：Cmd+Shift+P) 開啟命令選擇區，輸入 **Arduino**，然後尋找並選取 [Arduino: Examples]。

## <a name="provision-azure-services"></a>佈建 Azure 服務

在解決方案視窗中，請藉由輸入 `task cloud-provision` 以透過 Ctrl+P (macOS：Cmd+P) 執行您的工作。

VS Code 終端機中會有互動式命令列來引導您佈建所需的 Azure 服務：

![互動式命令列](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/cloud-provision.png)

## <a name="build-and-upload-the-arduino-sketch"></a>建置並上傳 Arduino 草圖

### <a name="install-the-required-library"></a>安裝必要的程式庫

1. 選取 F1 或 Ctrl+Shift+P (macOS：Cmd+Shift+P) 開啟命令選擇區，輸入 **Arduino**，然後尋找並選取 [Arduino: Library Manager]。

2. 搜尋 **ArduinoJson** 程式庫，然後選取 [安裝]。

### <a name="build-and-upload-the-device-code"></a>組建並上傳裝置程式碼

使用 Ctrl+P (macOS：Cmd+P) 來執行 `task device-upload`。 終端機會提示您進入設定模式。 若要這樣做，請按住按鈕 A，然後按下再放開 [Reset] 按鈕。 畫面會顯示 [設定]。 這可讓您設定擷取自 `task cloud-provision` 步驟的連接字串。

然後終端機會開始驗證和上傳 Arduino 草圖：

![驗證和上傳 Arduino 草圖](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/device-upload.png)

DevKit 會重新開機，然後開始執行程式碼。

## <a name="test-the-project"></a>測試專案

在 VS Code 中，選取狀態列上的電源插頭圖示，以開啟「序列監視器」。

當您看到以下結果時，表示範例應用程式已成功執行：

* 序列監視器顯示與下列螢幕擷取畫面內容相同的資訊。
* MXChip IoT DevKit 上的 LED 燈在閃爍。

![VS Code 的最終輸出](media/iot-hub-arduino-devkit-az3166-get-started/mini-solution/connect-iothub/result-serial-output.png)

## <a name="problems-and-feedback"></a>問題與意見反應

如果您遇到問題，您可以尋找[常見問題集](https://microsoft.github.io/azure-iot-developer-kit/docs/faq/)。 您也可以在這個頁面留下評論，以對我們提供意見反應。

## <a name="next-steps"></a>後續步驟

您已成功將 MXChip IoT DevKit 連線到 IoT 中樞，並將擷取到的感應器資料傳送至 IoT 中樞。

若要繼續開始使用 Azure IoT 中樞以及瀏覽其他 IoT 案例，請參閱︰

- [透過 iothub-explorer 管理雲端裝置傳訊](https://docs.microsoft.com/azure/iot-hub/iot-hub-explorer-cloud-device-messaging)
- [將 IoT 中樞IoT 中樞儲存至 Azure 資料儲存體](https://docs.microsoft.com//azure/iot-hub/iot-hub-store-data-in-azure-table-storage)
- [使用 Power BI 將來自 Azure IoT 中樞的即時感應器資料視覺化](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-power-bi)
- [使用 Web Apps 將來自 Azure IoT 中樞的即時感應器資料視覺化](https://docs.microsoft.com//azure/iot-hub/iot-hub-live-data-visualization-in-web-apps)
- [在 Azure Machine Learning 中使用 IoT 中樞的感應器資料進行天氣預測](https://docs.microsoft.com/azure/iot-hub/iot-hub-weather-forecast-machine-learning)
- [透過 iothub-explorer進行裝置管理](https://docs.microsoft.com/azure/iot-hub/iot-hub-device-management-iothub-explorer)
- [搭配 Logic Apps 進行遠端監視和通知](https://docs.microsoft.com/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps)

