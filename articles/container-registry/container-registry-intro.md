---
title: "Azure 中的私人 Docker 容器登錄 | Microsoft Docs"
description: "Azure 容器登錄庫服務的簡介，此服務提供雲端式管理的私人 Docker Registry。"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.translationtype: HT
ms.sourcegitcommit: 83f19cfdff37ce4bb03eae4d8d69ba3cbcdc42f3
ms.openlocfilehash: fd0356286be46f99fd9ab8eabc53256103038407
ms.contentlocale: zh-tw
ms.lasthandoff: 08/21/2017

---
# <a name="introduction-to-private-docker-container-registries"></a>私人 Docker 容器登錄的簡介


Azure 容器登錄是可管理的 [Docker Registry](https://docs.docker.com/registry/) 服務，架構於開放原始碼的 Docker Registry 2.0。 建立及維護 Azure 容器登錄庫，以儲存和管理您的私人 [Docker 容器](https://www.docker.com/what-docker)映像。 使用 Azure 的容器登錄庫進行現有容器的開發與部署管線，並利用 Docker 社群的專業知識。

如需有關 Docker 和容器的背景，請參閱︰

* [Docker 使用者指南](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>使用案例
從 Azure 容器登錄庫將映像提取到不同部署目標︰

* **可調整的協調流程系統**，會管理整個主機叢集上容器化的應用程式，包括 [DC/OS](https://docs.mesosphere.com/)、[Docker Swarm](https://docs.docker.com/swarm/)、 [Kubernetes](http://kubernetes.io/docs/)。
* **Azure 服務**，會支援依規模建置和執行的應用程式，包括 [Container Service](../container-service/index.yml)、[App Service](/app-service/index.md)、[Batch](../batch/index.md)、[Service Fabric](/azure/service-fabric/) 和其他應用程式。

開發人員也可以將推送到容器登錄庫，當做容器開發工作流程的一部分。 例如，以容器登錄庫為目標，並以 [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) 或 [Jenkins](https://jenkins.io/) 等持續整合與部署工具為起點。





## <a name="key-concepts"></a>重要概念
* **登錄庫** - 在您的 Azure 訂用帳戶中建立一或多個容器登錄庫。 每個登錄後有一個在相同位置中的標準 Azure [儲存體帳戶](../storage/common/storage-introduction.md)。 在與您的部署相同的 Azure 位置建立登錄，以利用容器映像接近網路的本機儲存體。 完整的登錄名稱具有 `myregistry.azurecr.io` 形式。

  使用 Azure Active Directory 支持的[服務主體](../active-directory/active-directory-application-objects.md)或提供的管理員帳戶，[控制](container-registry-authentication.md)對容器登錄庫的存取。 執行標準 `docker login` 命令驗證登錄庫。

* **受管理登錄** - 為三個 SKU 中的登錄提供額外功能的層級 - 基本、標準和進階。 這些 SKU 中的映像會儲存在 Azure Container Registries 服務所管理的儲存體帳戶中，因此提高可靠性，並啟用新功能。 新功能包括 Webhook 整合、與 Azure Active Directory 的存放庫驗證，以及刪除功能支援。 使用者可以選擇選取受管理的登錄，或是建立在建立登錄時由其專屬儲存體帳戶所支援的登錄。

* **儲存機制** - 登錄庫會包含一個或多個儲存機制，儲存機制是容器映像的群組。 Azure 容器登錄庫支援多層級的儲存機制命名空間。 這項功能可讓您將與特定應用程式相關的映像集合為群組，或將特定開發或作業團隊的應用程式集合為群組。 例如：

  * `myregistry.azurecr.io/aspnetcore:1.0.1` 表示全公司的映像
  * `myregistry.azurecr.io/warrantydept/dotnet-build` 表示用來建立 .NET 應用程式的映像，在保固部門之間共用
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web` 表示 Web 映像，其屬於保固部門所擁有的客戶提交應用程式群組

* **映像** - 儲存在儲存機制中，每個映像是 Docker 容器的唯讀快照。 Azure 容器登錄庫可以包含 Windows 和 Linux 映像。 您可以控制您的所有容器部署的映像名稱。 使用標準 [Docker 命令](https://docs.docker.com/engine/reference/commandline/) 將映像推送到儲存機制，或從儲存機制提取映像。

* **容器** - 容器定義軟體應用程式及其相依性，包裹在完整的檔案系統中，包括程式碼、執行階段、系統工具和程式庫。 根據您從容器登錄庫提取的 Windows 或 Linux 映像，執行 Docker 容器。 在單一電腦上執行的容器共用作業系統核心。 Docker 容器可完全移植到所有主要 Linux 散發版本、Mac 和 Windows。




## <a name="next-steps"></a>後續步驟
* [使用 Azure 入口網站建立容器登錄庫](container-registry-get-started-portal.md)
* [使用 Azure CLI 建立容器登錄庫](container-registry-get-started-azure-cli.md)
* [使用 Docker CLI 推送您的第一個映像](container-registry-get-started-docker-cli.md)
* 若要使用 Visual Studio Team Services、Azure Container Service 和 Azure Container Registry 建置持續整合與部署工作流程，請參閱[此教學課程](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md)。
* 如果您想在 Azure 中設定自己的 Docker 私人登錄 (不含公用端點)，請參閱[在 Azure 上部署您自己的私用 Docker Registry](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md)。

