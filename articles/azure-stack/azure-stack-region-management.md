---
title: Azure Stack 中的区域管理 | Microsoft Docs
description: Azure Stack 中的区域管理概述。
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2018
ms.author: sethm
ms.reviewer: efemmano
ms.openlocfilehash: 80a8414d98eba984f2427f5f746cd0e1061248a4
ms.sourcegitcommit: 549070d281bb2b5bf282bc7d46f6feab337ef248
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2018
ms.locfileid: "53726901"
---
# <a name="region-management-in-azure-stack"></a>Azure Stack 中的区域管理

*适用于：Azure Stack 集成系统和 Azure Stack 开发工具包*

Azure Stack 使用“区域”的概念，这些区域是由构成 Azure Stack 基础结构的硬件资源组成的逻辑实体。 在区域管理中，可以找到成功操作 Azure Stack 基础结构所需的所有资源。

一个集成系统部署（称为 *Azure Stack 云*）可构成一个区域。 每个 Azure Stack 开发工具包都有一个名为 **local** 的区域。 如果部署第二个 Azure Stack 集成系统，或者在单独的硬件上设置开发工具包的另一个实例，则此 Azure Stack 云为不同的区域。

## <a name="information-available-through-the-region-management-tile"></a>通过区域管理磁贴提供的信息

Azure Stack 在“区域管理”磁贴中提供了一组区域管理功能。 Azure Stack 操作员可在管理员门户的默认仪表板上访问此磁贴。 可以通过此磁贴来监视和更新 Azure Stack 区域和及其区域特定的组件。

![“区域管理”磁贴](media/azure-stack-region-management/image1.png)

如果单击“区域管理”磁贴中的一个区域，可以访问以下信息：

[ ![区域管理边栏选项卡上的窗格的说明](media/azure-stack-region-management/regionssm.png "区域管理边栏选项卡") ](media/azure-stack-region-management/regions.png#lightbox)

1. **资源菜单**。 访问特定的基础结构管理领域，以及查看和管理用户资源，例如存储帐户和虚拟网络。

2. **警报**。 列出系统范围中的警报，并提供有关每个警报的详细信息。

3. **更新**。 查看 Azure Stack 基础结构的当前版本、可用更新和更新历史记录。 也可以更新集成系统。

4. **资源提供程序**。 管理运行 Azure Stack 时所需组件提供的用户功能。 每个资源提供程序均附带管理体验。 这项体验可能包括特定提供程序的警报、指标和其他特定于资源提供程序的管理功能。

5. **基础结构角色**。 运行 Azure Stack 时所需的组件。 仅报告警报的基础结构角色会列出。 通过选择角色，可以查看与角色关联的警报，以及运行此角色的角色实例。

6. Properties。 注册状态和你的环境中的区域管理边栏选项卡的详细信息。 状态可以是**Registered**或**未注册**。 如果注册，它还显示的 Azure 订阅 ID，用于注册 Azure Stack，以及注册的资源组和名称。

## <a name="next-steps"></a>后续步骤

- [在 Azure Stack 中监视运行状况和警报](azure-stack-monitor-health.md)
- [在 Azure Stack 中管理更新](azure-stack-updates.md)
