---
title: 教程：Azure Active Directory 与 Mimecast Admin Console 的集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Mimecast Admin Console 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: ce4142c5b4a20886a94c87699f262f7238fc2cb4
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39438563"
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>教程：Azure Active Directory 与 Mimecast Admin Console 的集成

本教程介绍如何将 Mimecast Admin Console 与 Azure Active Directory (Azure AD) 集成。

将 Mimecast Admin Console 与 Azure AD 集成具有以下优势：

- 可在 Azure AD 中控制谁有权访问 Mimecast Admin Console。
- 可以让用户使用其 Azure AD 帐户自动登录到 Mimecast Admin Console（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

要配置 Azure AD 与 Mimecast Admin Console 的集成，需要以下项：

- Azure AD 订阅
- 启用了 Mimecast Admin Console 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Mimecast Admin Console
1. 配置和测试 Azure AD 单一登录

## <a name="adding-mimecast-admin-console-from-the-gallery"></a>从库中添加 Mimecast Admin Console
要配置 Mimecast Admin Console 与 Azure AD 的集成，需要从库中将 Mimecast Admin Console 添加到托管 SaaS 应用列表。

**要从库中添加 Mimecast Admin Console，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

1. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]
    
1. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

1. 在搜索框中键入 Mimecast Admin Console，在结果面板中选择“Mimecast Admin Console”，并单击“添加”按钮添加该应用程序。

    ![结果列表中的 Mimecast Admin Console](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，将基于名为“Britta Simon”的测试用户配置并测试 Mimecast Admin Console 的 Azure AD 单一登录。

为使单一登录能正常工作，Azure AD 需要知道与 Azure AD 用户相对应的 Mimecast Admin Console 用户。 换句话说，需要在 Azure AD 用户与 Mimecast Admin Console 中相关用户之间建立链接关系。

可通过将 Azure AD 中“用户名”的值指定为 Mimecast Admin Console 中“用户名”的值，建立此链接关系。

要配置和测试 Mimecast Admin Console 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
1. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
1. **[创建 Mimecast Admin Console 测试用户](#create-a-mimecast-admin-console-test-user)** - 在 Mimecast Admin Console 中创建 Britta Simon 的对应用户，并将其链接到用户的 Azure AD 表示形式。
1. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
1. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Mimecast Admin Console 应用程序中配置单一登录。

**要配置 Mimecast Admin Console 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中的“Mimecast Admin Console”应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

1. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![“单一登录”对话框](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

1. 在“Mimecast Admin Console 域和 URL”部分中，执行以下步骤：

    ![Mimecast Admin Console 域和 URL 单一登录信息](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    在“登录 URL”文本框中，键入 URL：
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > 登录 URL 特定于区域。

1. 在“SAML 签名证书”部分中，单击“证书(base64)”，并在计算机上保存证书文件。

    ![证书下载链接](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

1. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/mimecast-admin-console-tutorial/tutorial_general_400.png)

1. 在“Mimecast Admin Console 配置”部分中，单击“配置 Mimecast Admin Console”以打开“配置登录”窗口。 从“快速参考”部分中复制“SAML 实体 ID 和 SAML 单一登录服务 URL”。

    ![Mimecast Admin Console 配置](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

1. 在另一个 Web 浏览器窗口中，以管理员身份登录到 Mimecast Admin Console。

1. 转到“服务”\>“应用程序”。

    ![服务](./media/mimecast-admin-console-tutorial/ic794998.png "服务")

1. 单击“身份验证配置文件”。

    ![身份验证配置文件](./media/mimecast-admin-console-tutorial/ic794999.png "身份验证配置文件")
    
1. 单击“新建身份验证配置文件”。

    ![新建身份验证配置文件](./media/mimecast-admin-console-tutorial/ic795000.png "新建身份验证配置文件")

1. 在“身份验证配置文件”部分中，执行以下步骤：

    ![身份验证配置文件](./media/mimecast-admin-console-tutorial/ic795015.png "身份验证配置文件")
    
    a. 在“描述”文本框中，键入配置名称。
    
    b. 选择“对 Mimecast Admin Console 强制实施 SAML 身份验证”。
    
    c. 对于“提供程序”，选择“Azure Active Directory”。
    
    d. 将从 Azure 门户复制的 SAML 实体 ID 粘贴到“颁发者 URL”文本框。
    
    e. 将从 Azure 门户复制的“SAML 单一登录服务 URL”粘贴到“登录 URL”文本框中。

    f. 将从 Azure 门户复制的“SAML 单一登录服务 URL”粘贴到“注销 URL”文本框中。
    
    >[!NOTE]
    >对于 Mimecast Admin Console，“登录 URL”值和“注销 URL”值是相同的。
    
    g. 在记事本中打开从 Azure 门户下载的 base-64 证书，删除第一行（“--”）和最后一行（“--”），将剩余的内容复制到剪贴板中，然后将其粘贴到“标识提供者证书(元数据)”文本框中。
    
    h. 选择“允许单一登录”。
    
    i. 单击“ **保存**”。

> [!TIP]
> 之后在设置应用时，就可以在 [Azure 门户](https://portal.azure.com)中阅读这些说明的简明版本了！  从“Active Directory”>“企业应用程序”部分添加此应用后，只需单击“单一登录”选项卡，即可通过底部的“配置”部分访问嵌入式文档。 可在此处阅读有关嵌入式文档功能的详细信息：[ Azure AD 嵌入式文档]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/mimecast-admin-console-tutorial/create_aaduser_01.png)

1. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/mimecast-admin-console-tutorial/create_aaduser_02.png)

1. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/mimecast-admin-console-tutorial/create_aaduser_03.png)

1. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。
 
### <a name="create-a-mimecast-admin-console-test-user"></a>创建 Mimecast Admin Console 测试用户

为了使 Azure AD 用户能够登录到 Mimecast Admin Console，必须将其预配到 Mimecast Admin Console 中。 对于 Mimecast Admin Console，需要手动执行预配。

* 需要注册一个域，才能创建用户。

**若要配置用户设置，请执行以下步骤：**

1. 以管理员身份登录到 **Mimecast Admin Console**。
1. 转到“目录”\>“内部”。
   
   ![目录](./media/mimecast-admin-console-tutorial/ic795003.png "目录")
1. 单击“注册新域”。
   
   ![注册新域](./media/mimecast-admin-console-tutorial/ic795004.png "注册新域")
1. 在创建新域后，单击“新建地址”。
   
   ![新建地址](./media/mimecast-admin-console-tutorial/ic795005.png "新建地址")
1. 在“新建地址”对话框中，执行以下步骤：
   
   ![保存](./media/mimecast-admin-console-tutorial/ic795006.png "保存")
   
   a. 将要预配的有效 Azure AD 帐户的“电子邮件地址”、“全局名称”、“密码”和“确认密码”属性键入到相关文本框中。

   b. 单击“ **保存**”。

>[!NOTE]
>可以使用 Mimecast Admin Console 提供的任何其他 Mimecast Admin Console 用户帐户创建工具或 API 来预配 Azure AD 用户帐户。 

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，将通过向 Britta Simon 授予 Mimecast Admin Console 的访问权限使之能够使用 Azure 单一登录。

![分配用户角色][200] 

**要将 Britta Simon 分配到 Mimecast Admin Console，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

1. 在应用程序列表中，选择“Mimecast Admin Console”。

    ![应用程序列表中的 Mimecast Admin Console 链接](./media/mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

1. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

1. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

1. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

1. 在“用户和组”对话框中单击“选择”按钮。

1. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

在访问面板中单击 Mimecast Admin Console 磁贴时，应自动登录到 Mimecast Admin Console 应用程序。
有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md)（访问面板简介）。 

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/mimecast-admin-console-tutorial/tutorial_general_203.png

