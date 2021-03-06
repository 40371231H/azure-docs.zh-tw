---
title: "使用 Azure CLI 2.0 管理 Web Apps for Containers | Microsoft Docs"
description: "使用 Azure CLI 2.0 管理 Web Apps for Containers。"
keywords: "azure app service, web 應用程式, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.translationtype: HT
ms.sourcegitcommit: 12c20264b14a477643a4bbc1469a8d1c0941c6e6
ms.openlocfilehash: d58fab0b423b7bc1382a82f4bf308b6ad7286296
ms.contentlocale: zh-tw
ms.lasthandoff: 09/07/2017

---
# <a name="manage-web-apps-for-containers-using-azure-cli"></a>使用 Azure CLI 管理 Web Apps for Containers

使用本文中的命令，即可使用 Azure CLI 2.0 建立和管理 Web Apps for Containers。
開始使用新版 CLI 的方式有兩種：

* 在您的電腦上[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。
* 使用 [Azure Cloud Shell (預覽)](../../cloud-shell/overview.md)

## <a name="create-a-linux-app-service-plan"></a>建立 Linux App Service 方案

若要建立 Linux App Service 方案，您可以使用下列命令：

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
```

## <a name="create-a-custom-docker-container-web-app"></a>建立自訂 Docker 容器 Web 應用程式

若要建立 Web 應用程式並設定它來執行自訂 Docker 容器，您可以使用下列命令：

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```

## <a name="activate-the-docker-container-logging"></a>啟動 Docker 容器記錄

若要啟動 Docker 容器記錄，您可以使用下列命令：

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```

## <a name="change-the-custom-docker-container-for-an-existing-web-apps-for-containers-app"></a>變更現有 Web Apps for Containers 應用程式的自訂 Docker 容器

若要將先前建立的應用程式從目前的 Docker 映像變更為新的映像，您可以使用下列命令：

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
```

## <a name="using-docker-images-from-a-private-registry"></a>使用私人登錄中的 Docker 映像

您可以將您的應用程式設定為使用私人登錄中的映像。 您需要提供登錄的 url、使用者名稱和密碼。 使用下列命令可達成此目的：

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
```

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>啟用自訂 Docker 映像的連續部署

使用下列命令，您可以啟用 CD 功能，並取得 Webhook url。 此 url 可以用來設定 DockerHub 或 Azure Container Registry 存放庫。

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
```

## <a name="create-a-web-apps-for-containers-app-using-one-of-our-built-in-runtime-frameworks"></a>使用任一個內建執行階段架構來建立 Web Apps for Containers 應用程式

若要建立 PHP 5.6 Web Apps for Containers 應用程式，您可以使用下列命令。

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
```

## <a name="change-framework-version-for-an-existing-web-apps-for-containers-app"></a>變更現有 Web Apps for Containers 應用程式的架構版本

若要將先前建立的應用程式從目前的架構版本變更為 Node.js 6.11，您可以使用下列命令：

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
```

## <a name="set-up-git-deployments-for-your-web-app"></a>為您的 Web 應用程式設定 Git 部署

若要為您的應用程式設定 Git 部署，您可以使用下列命令：

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
```

## <a name="next-steps"></a>後續步驟

* [什麼是 Azure Web Apps for Containers？](app-service-linux-intro.md)
* [安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (預覽)](../../cloud-shell/overview.md)
* [在 Azure App Service 中設定預備環境](../../app-service-web/web-sites-staged-publishing.md?toc=%2fazure%2fapp-service%2fcontainers%2ftoc.json)
* [使用 Azure Web Apps for Containers 進行持續部署](app-service-linux-ci-cd.md)

