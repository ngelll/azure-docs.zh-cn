---
title: 如何将用户和组分配到应用程序 | Microsoft Docs
description: 将用户分配到应用程序以授予访问权限
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 10/01/2018
ms.author: barbkess
ms.openlocfilehash: d99209af9b1b6697419a046812928e75fed70321
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53076948"
---
# <a name="assign-users-and-groups-to-an-application-in-azure-active-directory"></a>向 Azure Active Directory 中的应用程序分配用户和组
本文介绍如何将用户或组分配到 Azure Active Directory (Azure AD) 中的应用程序。 首先必须将用户分配给应用程序，然后管理员才能授予这些用户访问权限以执行以下操作：

-   通过**直接导航到应用程序的 URL**（也称为 SP 发起的登录）访问应用程序。

-   通过使用应用程序的“属性”页上的“用户访问 URL”（也称为 IDP 发起的登录）访问应用程序。

-   查看显示在其[应用程序访问面板](https://myapps.microsoft.com/)的应用程序或移动应用程序。

-   查看显示在其 [Office 365 应用程序启动器](https://support.office.com/article/Meet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a)中的应用程序。

## <a name="prerequisties"></a>先决条件
在将用户和组分配到应用程序之前，必须要求用户分配。 若要要求用户分配，请执行以下操作：

1. 使用管理员帐户登录到 Azure 门户。
2. 在主菜单中单击“所有服务”项。
3. 选择要用于应用程序的目录。
4. 单击“企业应用程序”选项卡。
5. 从与此目录关联的应用程序列表中选择应用程序。
6. 单击“属性”选项卡。
7. 将“需要进行用户分配?”切换为“是”。
8. 单击屏幕顶部的“保存”按钮。

## <a name="assign-users"></a>分配用户

要直接将一个或多个用户分配到应用程序，请按照以下步骤操作：

1.  打开 [**Azure 门户**](https://portal.azure.com/)，并以“全局管理员”身份登录。

2.  在左侧主导航菜单顶部单击“所有服务”，打开“Azure Active Directory 扩展”。

3.  在筛选器搜索框中键入“Azure Active Directory”，选择“Azure Active Directory”项。

4.  在 Azure Active Directory 的左侧导航菜单中，单击“企业应用程序”。

5.  单击“所有应用程序”，查看所有应用程序的列表。

    * 如果未看到要在此处显示的应用程序，请使用“所有应用程序列表”顶部的“筛选器”控件，并将“显示”选项设置为“所有应用程序”。

6.  从列表中选择要向其分配用户的应用程序。

7.  在应用程序加载后，在应用程序的左侧导航菜单中单击“用户和组”。

8.  单击“用户和组”列表顶部的“添加”按钮，以打开“添加分配”窗格。

9.  在“添加分配”窗格中，单击“用户和组”选择器。

10. 在“按名称或电子邮件地址搜索”搜索框中，键入要分配的用户的**全名**或**电子邮件地址**。

11. 将鼠标悬停在列表中的“用户”上方以显示“复选框”。 单击用户个人资料头像或徽标旁边的复选框，将用户添加到“已选择”列表。

12. **可选：** 如果要“添加多个用户”，请在“按名称或电子邮件地址搜索”搜索框中键入其他“全名”或“电子邮件地址”，然后单击复选框以将此用户添加到“已选择”列表。

13. 在完成用户的选择后，单击“选择”按钮将他们添加到要分配给应用程序的用户和组列表。

14. **可选：** 单击“添加分配”窗格中的“选择角色”选择器，选择一个角色来分配给所选用户。

15. 单击“分配”按钮，将应用程序分配给选定用户。

在一段很短的时间后，所选用户能够使用解决方案描述部分中所述的方法启动这些应用程序。

## <a name="assign-groups"></a>分配组

要直接将一个或多个组分配到应用程序，请遵循以下步骤：

1.  打开 [**Azure 门户**](https://portal.azure.com/)，并以“全局管理员”身份登录。

2.  在左侧主导航菜单顶部单击“所有服务”，打开“Azure Active Directory 扩展”。

3.  在筛选器搜索框中键入“Azure Active Directory”，选择“Azure Active Directory”项。

4.  在 Azure Active Directory 的左侧导航菜单中，单击“企业应用程序”。

5.  单击“所有应用程序”，查看所有应用程序的列表。

    * 如果未看到要在此处显示的应用程序，请使用“所有应用程序列表”顶部的“筛选器”控件，并将“显示”选项设置为“所有应用程序”。

6.  从列表中选择要向其分配用户的应用程序。

7.  在应用程序加载后，在应用程序的左侧导航菜单中单击“用户和组”。

8.  单击“用户和组”列表顶部的“添加”按钮，以打开“添加分配”窗格。

9.  在“添加分配”窗格中，单击“用户和组”选择器。

10. 在“按名称或电子邮件地址搜索”搜索框中，键入要分配的组的**完整组名**。

11. 将鼠标悬停在列表中的**组**上以显示**复选框**。 单击组头像或徽标旁边的复选框以将用户添加到“已选择”列表。

12. **可选：** 如果要“添加多个组”，请在“按名称或电子邮件地址搜索”搜索框中键入其他“完整组名”，然后单击复选框以将此组添加到“已选择”列表。

13. 选择完所有组后，单击“选择”按钮将所有已选择的组添加到要分配给应用程序的用户和组的列表中。

14. **可选：** 单击“添加分配”窗格中的“选择角色”选择器，选择一个角色来分配给所选组。

15. 单击“分配”按钮，将应用程序分配给所选组。

在一段很短的时间后，所选组中的用户能够使用解决方案描述部分中所述的方法启动这些应用程序。 如果是动态组，则这些分配组中的用户显示分配时可能会出现一些额外的处理延迟。

## <a name="enable-self-service-application-access"></a>启用自助应用程序访问

自助应用程序访问是帮助用户自己发现应用程序的绝佳方式，可选择性地允许业务组批准对这些应用程序的访问。 可允许业务组直接从其访问面板，管理分配给用户的密码单一登录应用程序的凭据。

若要启用应用程序的自助应用程序访问，请执行以下步骤：

1.  打开 [**Azure 门户**](https://portal.azure.com/)，并以“全局管理员”身份登录。

2.  在左侧主导航菜单顶部单击“所有服务”，打开“Azure Active Directory 扩展”。

3.  在筛选器搜索框中键入“Azure Active Directory”，选择“Azure Active Directory”项。

4.  在 Azure Active Directory 的左侧导航菜单中，单击“企业应用程序”。

5.  单击“所有应用程序”，查看所有应用程序的列表。

   * 如果未看到要在此处显示的应用程序，请使用“所有应用程序列表”顶部的“筛选器”控件，并将“显示”选项设置为“所有应用程序”。

6.  从列表中选择要对其启用自助访问的应用程序。

7.  加载应用程序后，在应用程序的左侧导航菜单中，单击“自助”。

8.  要对此应用程序启用自助应用程序访问，请将“允许用户请求对此应用程序的访问权限?”切换到“是”。

9.  接下来，要选择向其添加请求此应用程序访问权限的用户的组，请单击“分配的用户应添加到哪个组?”标签旁边的选择器，并选择一个组。

10. **可选：** 如果希望在获得业务批准之后才允许用户访问，请将“需要获得批准才能授权访问此应用程序?”切换到“是”。

11. **可选：对于仅使用密码单一登录的应用程序**，如果要允许业务审批人为已获得批准的用户指定发送到此应用程序的密码，请将“允许审批人设置此应用程序的用户密码?”切换到“是”。

12. **可选：** 若要指定有权批准对此应用程序访问的业务审批人，请单击“谁有权批准此应用程序的访问权限?”标签旁边的选择器，最多可选择 10 个单独的业务审批人。

  >[!NOTE]
  >不支持组。
  >
  >

13. **可选：**“对于公开角色的应用程序”，如果想要向角色分配已被批准使用自助服务的用户，请单击“在此应用程序中应向哪个角色分配用户?”旁边的选择器，选择要向其分配这些用户的角色。

14. 单击窗格顶部的“保存”按钮以完成操作。

完成自助应用程序配置后，用户可以导航到其[应用程序访问面板](https://myapps.microsoft.com/)，单击“+添加”按钮以查找已启用自助访问的应用。 业务审批人还可以在其[应用程序访问面板](https://myapps.microsoft.com/)中看到通知。 可以启用电子邮件，在用户请求需要审批人批准的应用程序的访问权限时，向审批人发送电子邮件通知。 

这些批准仅支持单个审批工作流，这意味着如果指定了多个审批人，任何一个审批人都可以批准对该应用程序的访问。

## <a name="next-steps"></a>后续步骤
[使用应用程序代理为应用提供单一登录](application-proxy-configure-single-sign-on-with-kcd.md)
