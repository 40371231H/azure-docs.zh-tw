---
title: "Application Insights 使用的 IP 位址 | Microsoft Docs"
description: "Application Insights 所需的伺服器防火牆例外狀況"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 44d989f8-bae9-40ff-bfd5-8343d3e59358
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: bwren
ms.translationtype: Human Translation
ms.sourcegitcommit: 138f04f8e9f0a9a4f71e43e73593b03386e7e5a9
ms.openlocfilehash: eec83ceb6edbc1aaa68d51a85d2a913063677530
ms.contentlocale: zh-tw
ms.lasthandoff: 06/29/2017

---
# <a name="ip-addresses-used-by-application-insights"></a>Application Insights 使用的 IP 位址
[Azure Application Insights](app-insights-overview.md) 服務會使用一些 IP 位址。 如果您所監視的應用程式裝載於防火牆後面，您可能需要知道這些位址。

> [!NOTE]
> 雖然這些位址是靜態的，但可能隨時需要變更。
> 
> 

## <a name="outgoing-ports"></a>連出連接埠
您需要在伺服器防火牆開啟某些連出連接埠，以允許 Application Insights SDK 和/或狀態監視器將資料傳送至入口網站：

| 目的 | URL | IP | 連接埠 |
| --- | --- | --- | --- |
| 遙測 |dc.services.visualstudio.com<br/>dc.applicationinsights.microsoft.com |40.114.241.141<br/>104.45.136.42<br/>40.84.189.107<br/>168.63.242.221<br/>52.167.221.184<br/>52.169.64.244 |443 |
| 即時計量串流 |rt.services.visualstudio.com<br/>rt.applicationinsights.microsoft.com |23.96.28.38<br/>13.92.40.198 |443 |
| 內部遙測 |breeze.aimon.applicationinsights.io |52.161.11.71 |443 |

## <a name="status-monitor"></a>狀態監視器
狀態監視器組態 - 只有在進行變更時才需要。

| 目的 | URL | IP | 連接埠 |
| --- | --- | --- | --- |
| 組態 |`management.core.windows.net` | |`443` |
| 組態 |`management.azure.com` | |`443` |
| 組態 |`login.windows.net` | |`443` |
| 組態 |`login.microsoftonline.com` | |`443` |
| 組態 |`secure.aadcdn.microsoftonline-p.com` | |`443` |
| 組態 |`auth.gfx.ms` | |`443` |
| 組態 |`login.live.com` | |`443` |
| 安裝 |`packages.nuget.org` | |`443` |

## <a name="hockeyapp"></a>HockeyApp
| 目的 | URL | IP | 連接埠 |
| --- | --- | --- | --- |
| 當機資料 |gate.hockeyapp.net |104.45.136.42 |80、443 |

## <a name="availability-tests"></a>可用性集合
這是用來執行 [可用性 Web 測試](app-insights-monitor-web-app-availability.md) 的位址清單。 如果您想要在您的應用程式上執行 Web 測試，但您的 Web 伺服器限於為特定用戶端提供服務，則您必須允許來自我們的可用性測試伺服器的連入流量。

為來自這些位址 (IP 位址會依照位置分組) 的連入流量開啟連接埠 80 (http) 和 443 (https)︰

```
AU : Sydney
13.70.83.252
13.75.150.96
13.75.153.9
13.75.158.185
BR : Sao Paulo
191.232.32.122
191.232.172.45
191.232.176.218
191.232.191.225
CH : Zurich
94.245.66.43
94.245.66.44
94.245.66.45
94.245.66.48
FR : Paris
94.245.72.44
94.245.72.45
94.245.72.46
94.245.72.49
94.245.72.52
94.245.72.53
HK : Hong Kong
13.75.121.122
23.99.115.153
23.99.123.38
23.102.232.186
52.175.38.49
52.175.39.103
IE : Dublin
13.74.184.101
13.74.185.160
40.69.200.198
52.164.224.46
52.169.12.203
52.169.14.11
52.169.237.149
52.178.183.105
JP : Kawaguchi
52.243.33.33
52.243.33.141
52.243.35.253
52.243.41.117
NL : Amsterdam
52.174.166.113
52.174.178.96
52.174.31.140
52.174.35.14
52.178.104.23
52.178.109.190
52.178.111.139
52.233.166.221
RU : Moscow
94.245.82.32
94.245.82.33
94.245.82.37
94.245.82.38
SE : Stockholm
94.245.78.40
94.245.78.41
94.245.78.42
94.245.78.45
SG : Singapore
52.187.29.7
52.187.179.17
52.187.76.248
52.187.43.24
52.163.57.91
52.187.30.120
US : CA-San Jose
104.45.228.236
104.45.237.251
13.64.152.110
13.64.156.54
13.64.232.251
13.64.236.105
13.91.94.59
40.118.131.182
40.83.189.192
40.83.215.122
US : FL-Miami
65.54.78.49
65.54.78.50
65.54.78.51
65.54.78.54
65.54.78.57
65.54.78.58
65.54.78.59
65.54.78.60
US : IL-Chicago
23.96.247.139
23.96.249.113
52.162.124.242
52.162.126.139
52.162.241.147
52.162.246.222
52.162.247.136
52.237.153.231
52.237.154.216
52.237.156.14
52.237.157.218
52.237.157.37
US : TX-San Antonio
104.210.145.106
13.84.176.24
13.84.49.16
13.85.11.137
13.85.26.248
13.85.69.145
52.171.136.162
52.171.141.253
52.171.57.172
52.171.58.140
US : VA-Ashburn
13.82.218.95
13.90.96.71
13.90.98.52
13.92.137.70
40.85.187.235
40.87.61.61
52.168.8.247
52.170.38.79
52.170.80.61
52.179.9.26

```  

## <a name="data-access-api"></a>資料存取 API
| 目的 | URI | IP | 連接埠 |
| --- | --- | --- | --- |
| API |api.applicationinsights.io<br/>api1.applicationinsights.io<br/>api2.applicationinsights.io<br/>api3.applicationinsights.io<br/>api4.applicationinsights.io<br/>api5.applicationinsights.io |13.82.26.252<br/>40.76.213.73 |80,443 |
| API 文件 |dev.applicationinsights.io<br/>dev.applicationinsights.microsoft.com<br/>dev.aisvc.visualstudio.com<br/>www.applicationinsights.io<br/>www.applicationinsights.microsoft.com<br/>www.aisvc.visualstudio.com |13.82.24.149<br/>40.114.82.10 |80,443 |
| 內部 API |aigs.aisvc.visualstudio.com<br/>aigs1.aisvc.visualstudio.com<br/>aigs2.aisvc.visualstudio.com<br/>aigs3.aisvc.visualstudio.com<br/>aigs4.aisvc.visualstudio.com<br/>aigs5.aisvc.visualstudio.com<br/>aigs6.aisvc.visualstudio.com |動態|443 |

## <a name="application-insights-analytics"></a>Application Insights 分析

| 目的 | URI | IP | 連接埠 |
| --- | --- | --- | --- |
| Analytics 入口網站 | analytics.applicationinsights.io | 動態 | 80,443 |
| CDN | applicationanalytics.azureedge.net | 動態 | 80,443 |
| 媒體 CDN | applicationanalyticsmedia.azureedge.net | 動態 | 80,443 |

注意：*.applicationinsights.io 網域由 Application Insights 團隊所擁有。

## <a name="application-insights-azure-portal-extension"></a>Application Insights Azure 入口網站擴充功能

| 目的 | URI | IP | 連接埠 |
| --- | --- | --- | --- |
| Application Insights 擴充功能 | stamp2.app.insightsportal.visualstudio.com | 動態 | 80,443 |
| Application Insights 擴充功能 CDN | insightsportal-prod2-cdn.aisvc.visualstudio.com<br/>insightsportal-prod2-asiae-cdn.aisvc.visualstudio.com<br/>insightsportal-cdn-aimon.applicationinsights.io | 動態 | 80,443 |

## <a name="application-insights-sdks"></a>Application Insights SDK

| 目的 | URI | IP | 連接埠 |
| --- | --- | --- | --- |
| Application Insights JS SDK CDN | az416426.vo.msecnd.net | 動態 | 80,443 |
| Application Insights Java SDK | aijavasdk.blob.core.windows.net | 動態 | 80,443 |

## <a name="profiler"></a>分析工具

| 目的 | URI | IP | 連接埠 |
| --- | --- | --- | --- |
| 代理程式 | agent.azureserviceprofiler.net<br/>*.agent.azureserviceprofiler.net | 動態 | 443
| 入口網站 | gateway.azureserviceprofiler.net | 動態 | 443
| 儲存體 | *.core.windows.net | 動態 | 443

## <a name="snapshot-debugger"></a>快照集偵錯工具

| 目的 | URI | IP | 連接埠 |
| --- | --- | --- | --- |
| 代理程式 | ppe.azureserviceprofiler.net<br/>*.ppe.azureserviceprofiler.net | 動態 | 443
| 入口網站 | ppe.gateway.azureserviceprofiler.net | 動態 | 443
| 儲存體 | *.core.windows.net | 動態 | 443

