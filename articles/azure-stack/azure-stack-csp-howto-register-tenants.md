---
title: 将租户添加到 Azure Stack 以获取用量和计费信息 | Microsoft Docs
description: 将最终用户添加到云服务提供商 (CSP) 管理的 Azure Stack 所要执行的步骤。
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2019
ms.author: sethm
ms.reviewer: alfredo
ms.openlocfilehash: be240ea17a8679d25623f971f7be5ea5c3ad2e8f
ms.sourcegitcommit: d61faf71620a6a55dda014a665155f2a5dcd3fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54053224"
---
# <a name="add-tenant-for-usage-and-billing-to-azure-stack"></a>将租户添加到 Azure Stack 以获取用量和计费信息

*适用于：Azure Stack 集成系统*

本文介绍将最终用户添加到托管的云服务提供商 (CSP) 的 Azure Stack 部署所需的步骤。 当新租户使用资源时，Azure Stack 向其 CSP 订阅报告使用情况。

CSP 通常向其 Azure Stack 部署中的多个最终客户（租户）提供服务。 将租户添加到 Azure Stack 注册可确保每个租户的使用情况报告，并计入相应的 CSP 订阅。 如果未完成本文中的步骤，则会向 Azure Stack 初始注册中使用的订阅计收租户使用费。 可以将最终用户添加到 Azure Stack 以跟踪用量并管理其租户之前，你必须将 Azure Stack 配置为 CSP。 有关步骤和资源，请参阅[管理充当云服务提供程序的 Azure Stack 的用量的计费](azure-stack-add-manage-billing-as-a-csp.md)。

下图显示了 CSP 需要遵循用于实现新的客户使用 Azure Stack，并设置使用情况跟踪客户的步骤。 通过添加最终客户，您还将能够管理 Azure Stack 中的资源。 可通过两个选项来管理这些资源：

1. 你可以保留最终客户，并向最终客户提供本地 Azure Stack 订阅的凭据。  
2. 最终客户可以使用其订阅本地，并将 CSP 添加为所有者权限的来宾。  

## <a name="steps-to-add-an-end-customer"></a>添加最终客户的步骤

![设置云服务提供程序以进行用量跟踪，以及管理最终客户帐户](media/azure-stack-csp-enable-billing-usage-tracking/process-csp-enable-billing.png)

### <a name="create-a-new-customer-in-partner-center"></a>在合作伙伴中心创建新客户

在合作伙伴中心，为客户创建新的 Azure 订阅。 有关说明，请参阅[添加新客户](https://msdn.microsoft.com/partner-center/add-a-new-customer)。

### <a name="create-an-azure-subscription-for-the-end-customer"></a>为最终客户创建 Azure 订阅

在合作伙伴中心创建的客户记录后，可以对目录中的产品的订阅对它们进行销售。 有关说明，请参阅[创建、暂停或取消客户订阅](https://msdn.microsoft.com/partner-center/create-a-new-subscription)。

### <a name="create-a-guest-user-in-the-end-customer-directory"></a>在最终客户目录中创建来宾用户

如果最终客户管理其自己的帐户，在其目录中创建来宾用户并将其发送信息。 最终用户将添加来宾并提升对的来宾权限**所有者**Azure Stack CSP 帐户。

### <a name="update-the-registration-with-the-end-customer-subscription"></a>更新最终客户订阅中的注册

使用新的客户订阅更新你的注册。 Azure 报告使用合作伙伴中心客户标识客户的使用情况。 此步骤可确保，在该客户的个人 CSP 订阅报告每个客户的使用情况。 这使得跟踪用户使用情况和计费更容易。

> [!NOTE]  
> 若要执行此步骤，必须具有[注册 Azure Stack](azure-stack-register.md)。

1. 使用权限提升的提示符打开 Windows PowerShell，并运行：  
    `Add-AzureRmAccount`
2. 键入 Azure 凭据。
3. 在 PowerShell 会话中运行：

   ```powershell
   New-AzureRmResource -ResourceId "subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionId}" -ApiVersion 2017-06-01 -Properties <PSObject>
   ```

### <a name="new-azurermresource-powershell-parameters"></a>New-AzureRmResource PowerShell 参数

以下部分描述的参数**New-azurermresource** cmdlet:

| 参数 | 描述 |
| --- | --- |
|registrationSubscriptionID | 用于 Azure Stack 初始注册的 Azure 订阅。|
| customerSubscriptionID | 属于要注册的客户的 Azure 订阅（不是 Azure Stack）。 必须在 CSP 产品中创建；在实践中，这意味着通过合作伙伴中心创建。 如果客户有多个 Azure Active Directory 租户，则必须在用于登录 Azure Stack 的租户中创建此订阅。 客户订阅 ID 必须使用小写字母。 |
| resourceGroup | Azure 中用于存储注册的资源组。 |
| registrationName | Azure Stack 的注册名称。 它是 Azure 中存储的对象。 |
| 属性 | 指定资源的属性。 使用此参数指定特定于资源类型的属性的值。

> [!NOTE]  
> 必须通过它们使用每个 Azure Stack 注册租户。 如果您有两个 Azure Stack 部署，并且租户使用这两个文件，则必须使用租户订阅更新每个部署的初始注册。

### <a name="onboard-tenant-to-azure-stack"></a>将租户加入到 Azure Stack

配置 Azure Stack，以支持多个 Azure AD 租户中的用户使用 Azure Stack 中的服务。 有关说明，请参阅[在 Azure Stack 中启用多租户](azure-stack-enable-multitenancy.md)。

### <a name="create-a-local-resource-in-the-end-customer-tenant-in-azure-stack"></a>在 Azure Stack 中的最终客户租户内创建本地资源

将新客户添加到 Azure Stack，或者最终客户租户已启用拥有所有者特权的来宾帐户后，请验证是否可在其租户中创建资源。 例如，他们可以[使用 Azure Stack 门户创建 Windows 虚拟机](user/azure-stack-quick-windows-portal.md)。

## <a name="next-steps"></a>后续步骤

- 若要查看注册过程中触发的错误消息，请参阅[租户注册错误消息](azure-stack-csp-ref-infrastructure.md#usage-and-billing-error-codes)。
- 若要详细了解如何从 Azure Stack 检索资源使用情况信息，请参阅 [Azure Stack 中的使用情况和计费](azure-stack-billing-and-chargeback.md)。
- 若要查看如何最终客户可能会将你添加，为 CSP 的管理员为其提供 Azure Stack 租户，请参阅[启用云服务提供商来管理 Azure Stack 订阅](user/azure-stack-csp-enable-billing-usage-tracking.md)。
