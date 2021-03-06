---
title: "Service Fabric 服務的可用性 | Microsoft Docs"
description: "描述錯誤偵測、容錯移轉與服務復原"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 279ba4a4-f2ef-4e4e-b164-daefd10582e4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.translationtype: HT
ms.sourcegitcommit: 847eb792064bd0ee7d50163f35cd2e0368324203
ms.openlocfilehash: b0d4615a9b8ab566f69b27e4879b6e2d597b4990
ms.contentlocale: zh-tw
ms.lasthandoff: 08/19/2017

---

# <a name="availability-of-service-fabric-services"></a>Service Fabric 服務的可用性
本文章概述 Service Fabric 如何維護服務的可用性。

## <a name="availability-of-service-fabric-stateless-services"></a>Service Fabric 無狀態服務的可用性
Azure Service Fabric 服務可能是具狀態或無狀態。 無狀態服務是一種應用程式服務，並不具有必須是高度可用或可靠的任何[本機狀態](service-fabric-concepts-state.md)。

建立無狀態服務需要定義 `InstanceCount`。 執行個體計數定義了應該在叢集中執行之無狀態服務應用程式邏輯的執行個體數目。 增加執行個體數目是一種相應放大無狀態服務規模的建議方式。

當無狀態的具名服務執行個體失敗時，系統就會在叢集中的某個合格節點上建立新的執行個體。 例如，無狀態服務執行個體可能會在 Node1 上失敗並在 Node5 上重新建立。

## <a name="availability-of-service-fabric-stateful-services"></a>Service Fabric 可設定狀態服務的可用性
具狀態服務具有某些與其相關聯的狀態。 在 Service Fabric 中，可設定狀態服務會模型化為複本集。 每個複本 (Replica) 都是執行中的服務程式碼執行個體，並同時具有該服務的狀態複本 (Copy)。 讀取與寫入作業會在單一複本上執行 (稱為「主要複本」)。 從寫入作業對狀態進行的變更，會「複寫」至複本集中的其他複本 (稱為「作用中次要複本」) 並予以套用。 

只能有一個「主要複本」，但可以有多個「作用中次要複本」。 「作用中次要複本」的數目是可設定的，且複本數目越高，所能容許的並行軟體和硬體失敗次數就越多。

如果「主要複本」當機，Service Fabric 就會讓其中一個「作用中次要複本」成為新的「主要複本」。 此「作用中次要複本」已經有更新過的狀態版本 (透過「複寫」)，因此能夠繼續處理進一步的讀取和寫入作業。

此概念 (即複本不是「主要複本」就是「作用中次要複本」) 稱為「複本角色」。

### <a name="replica-roles"></a>複本角色
複本角色用來管理由該複本管理的狀態生命週期。 扮演「主要」角色的複本會為讀取要求提供服務。 「主要複本」同時也會藉由更新寫入要求的狀態並複寫變更，來處理所有寫入要求。 這些變更會套用至複本集內的「作用中次要複本」。 「作用中次要複本」的工作是接收「主要複本」已複寫的狀態變更，並更新其狀態檢視。

> [!NOTE]
> 更高階的程式設計模型 (例如 [Reliable Actors](service-fabric-reliable-actors-introduction.md) 和 [Reliable Services](service-fabric-reliable-services-introduction.md)) 會對開發人員隱藏複本角色的概念。 在 Actor 中，角色的概念是不必要的；但在 Services 中，則針對大多數案例大部分會予以簡化。
>

## <a name="next-steps"></a>後續步驟
如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章：

- [調整 Service Fabric 服務](service-fabric-concepts-scalability.md)
- [分割 Service Fabric 服務](service-fabric-concepts-partitioning.md)
- [定義和管理狀態](service-fabric-concepts-state.md)
- [Reliable Services](service-fabric-reliable-services-introduction.md)

