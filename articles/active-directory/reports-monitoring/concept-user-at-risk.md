---
title: Azure Active Directory 门户中“标记为风险用户”的用户的安全报告 | Microsoft Docs
description: 了解 Azure Active Directory 门户中“标记为风险用户”的用户的安全报告
services: active-directory
author: priyamohanram
manager: mtillman
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 11/13/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 9a7a3877970d5ecf3b86471b94fbb1bf6e5efbb4
ms.sourcegitcommit: 1f9e1c563245f2a6dcc40ff398d20510dd88fd92
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51621065"
---
# <a name="users-flagged-for-risk-report-in-the-azure-portal"></a>Azure 门户中标记为存在风险的用户的报表

Azure Active Directory (Azure AD) 可以检测到与用户帐户相关的可疑操作。 每检测到一个可疑操作，就会创建一个名为[“风险事件”](concept-risk-events.md)的记录。

可以从 [Azure 门户](https://portal.azure.com)中通过选择“Azure Active Directory”边栏选项卡并导航到“安全性”部分来访问安全报告。 

检测到的风险事件用于计算：

- **风险登录** - 风险登录是指可能由非用户帐户合法拥有者进行的登录尝试。 

- **已标记为存在风险的用户** - 风险用户是指可能已泄露的用户帐户。 

若要了解如何配置触发这些风险事件的策略，请参阅[如何配置用户风险策略](../identity-protection/howto-user-risk-policy.md)。 

![有风险的登录](./media/concept-user-at-risk/10.png)


## <a name="what-azure-ad-license-do-you-need-to-access-the-users-at-risk-report"></a>访问风险用户报表需要什么 Azure AD 许可证？  

所有版本的 Azure Active Directory 都提供标记为存在风险的用户的报表。 但是，各版本的报表粒度级别有所不同： 

- 在“Azure Active Directory 免费版和基本版”中，获取一个列表，其中包含标记为存在风险的用户。 

- 此外，**Azure Active Directory Premium 1** 版本还允许你检查每个报告中检测到的某些底层风险事件。 

- Azure Active Directory Premium 2 版本提供有关所有潜在风险事件的最详细信息，并且还允许配置可自动响应已配置风险级别的安全策略。


## <a name="users-at-risk-report-for-azure-ad-free-and-basic-editions"></a>Azure AD 免费版和基本版的风险用户报告

Azure AD 免费版和基本版中“标记为风险用户”报告提供可能已泄露的用户帐户列表。 

![有风险的登录](./media/concept-user-at-risk/03.png)

选择用户可打开相关的用户数据边栏选项卡。 对于存在风险的用户，可查看其登录历史记录，并根据需要重置密码。

![有风险的登录](./media/concept-user-at-risk/46.png)


此对话框提供的选项用于：

- 下载报告

- 搜索用户

![有风险的登录](./media/concept-user-at-risk/16.png)


## <a name="users-at-risk-report-for-azure-ad-premium-editions"></a>Azure Active Directory Premium 版的风险用户报告

Azure AD Premium 版中“标记为风险用户”的用户的报告提供：

- 可能已泄露的用户帐户列表 

- 有关已检测到的[风险事件类型](concept-risk-events.md)的聚合信息

- 一个用于下载报表的选项

- 一个用于配置[用户风险补救策略](../identity-protection/howto-user-risk-policy.md)的选项  

![有风险的登录](./media/concept-user-at-risk/71.png)

选择用户时，可获取此用户的详细报表视图，以便：

- 打开“所有的登录”视图

- 重置用户密码

- 清除所有事件

- 为用户调查报告的风险事件。 

![有风险的登录](./media/concept-user-at-risk/324.png)

若要调查某个风险事件，请从列表中选择一个此类事件，以便打开该风险事件的“详细信息”边栏选项卡。 在“详细信息”边栏选项卡上，可选择手动关闭风险事件或重新激活已手动关闭的风险事件。 

![有风险的登录](./media/concept-user-at-risk/325.png)


## <a name="next-steps"></a>后续步骤

- [如何配置用户风险策略](../identity-protection/howto-user-risk-policy.md)
- [如何配置风险补救策略](../identity-protection/howto-user-risk-policy.md)
- [Azure Active Directory Identity Protection](../active-directory-identityprotection.md)

