---
title: 教程：Azure Active Directory 与 Confluence SAML SSO by Microsoft 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 Confluence SAML SSO by Microsoft 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/05/2018
ms.author: jeedes
ms.openlocfilehash: 2e254faae0289cd00c7e66d430ec3148fccb364a
ms.sourcegitcommit: 02ce0fc22a71796f08a9aa20c76e2fa40eb2f10a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2018
ms.locfileid: "51288146"
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>教程：Azure Active Directory 与 Confluence SAML SSO by Microsoft 集成

本教程介绍如何将 Confluence SAML SSO by Microsoft 与 Azure Active Directory (Azure AD) 集成。

将 Confluence SAML SSO by Microsoft 与 Azure AD 集成可提供以下优势：

- 可在 Azure AD 中控制谁有权访问 Confluence SAML SSO by Microsoft。
- 可让用户使用其 Azure AD 帐户自动登录 Confluence SAML SSO by Microsoft（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)

## <a name="description"></a>说明:

在 Atlassian Confluence 服务器上使用 Microsoft Azure Active Directory 帐户启用单一登录。 这样，所有组织用户便可使用 Azure AD 凭据登录到 Confluence 应用程序。 此插件使用 SAML 2.0 进行联合身份验证。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Confluence SAML SSO by Microsoft 的集成，需要以下项：

- Azure AD 订阅
- 安装在 Windows 64 位服务器（本地或基于云 IaaS 基础结构）上的 Confluence 服务器应用程序
- Confluence 服务器已启用 HTTPS
- 请注意，下面部分列出了支持的 Confluence 插件版本。
- Confluence 服务器可以访问 Internet，尤其是访问用于身份验证的 Azure AD 登录页，还应当可以接收来自 Azure AD 的令牌
- 在 Confluence 中设置管理员凭据
- 在 Confluence 中禁用 WebSudo
- 在 Confluence 服务器应用程序中创建的测试用户

> [!NOTE]
> 不建议使用 Confluence 生产环境测试本教程中的步骤。 首先在应用程序的开发环境或过渡环境中测试集成，然后使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可在此处获取一个月的试用版：[试用产品/服务](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="supported-versions-of-confluence"></a>支持的 Confluence 版本

当前支持下列 Confluence 版本：

- Confluence：5.0 至 5.10
- Confluence：6.0.1
- Confluence：6.1.1
- Confluence：6.2.1
- Confluence：6.3.4
- Confluence：6.4.0
- Confluence：6.5.0
- Confluence：6.6.2
- Confluence：6.7.0
- Confluence：6.8.1
- Confluence：6.9.0
- Confluence：6.10.0
- Confluence：6.11.0
- Confluence：6.12.0

## <a name="scenario-description"></a>方案描述

在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Confluence SAML SSO by Microsoft
2. 配置和测试 Azure AD 单一登录

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a>从库中添加 Confluence SAML SSO by Microsoft

若要配置 Confluence SAML SSO by Microsoft 与 Azure AD 的集成，需要从库中将 Confluence SAML SSO by Microsoft 添加到托管 SaaS 应用列表。

**若要从库中添加 Confluence SAML SSO by Microsoft，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]

3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中键入“Confluence SAML SSO by Microsoft”，在结果面板中选择“Confluence SAML SSO by Microsoft”，然后单击“添加”按钮添加该应用程序。

    ![结果列表中的 Confluence SAML SSO by Microsoft](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，基于名为“Britta Simon”的测试用户配置和测试 Confluence SAML SSO by Microsoft 的 Azure AD 单一登录。

为使单一登录能正常工作，Azure AD 需要知道与 Azure AD 用户相对应的 Confluence SAML SSO by Microsoft 用户。 换句话说，需要建立 Azure AD 用户与 Confluence SAML SSO by Microsoft 中相关用户之间的链接关系。

若要配置和测试 Confluence SAML SSO by Microsoft 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configuring-azure-ad-single-sign-on)** - 让用户使用此功能。
2. **[创建 Azure AD 测试用户](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 Confluence SAML SSO by Microsoft 测试用户](#creating-confluence-saml-sso-by-microsoft-test-user)** - 在 Confluence SAML SSO by Microsoft 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assigning-the-azure-ad-test-user)** - 让 Britta Simon 使用 Azure AD 单一登录。
5. **[测试单一登录](#testing-single-sign-on)** - 验证配置是否正常工作。

### <a name="configuring-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Confluence SAML SSO by Microsoft 应用程序中配置单一登录。

**若要配置 Confluence SAML SSO by Microsoft 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中的 Confluence SAML SSO by Microsoft 应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“选择单一登录方法”对话框中，单击“SAML”模式对应的“选择”，以启用单一登录。

    ![配置单一登录](common/tutorial_general_301.png)

3. 在“使用 SAML 设置单一登录”页上，单击“编辑”图标以打开“基本 SAML 配置”对话框。

    ![配置单一登录](common/editconfigure.png)

4. 在“基本 SAML 配置”部分中，按照以下步骤操作：

    ![Confluence SAML SSO by Microsoft 域和 URL 单一登录信息](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，并单击“添加引用”。 在“登录 URL”文本框中，使用以下模式键入 URL： `https://<domain:port>/plugins/servlet/saml/auth`

    b. 在“标识符”文本框中，使用以下模式键入 URL：`https://<domain:port>/`

    c. 在 **“回复 URL”** 文本框中，使用以下模式键入 URL：`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE]
    > 这些不是实际值。 请使用实际的“标识符”、“回复 URL”和“登录 URL”更新这些值。 端口可选，以防止其为命名 URL。 在配置 Confluence 插件的过程中，将接收这些值，这将在教程的后面部分进行说明。

5. 在“SAML 签名证书”页的“SAML 签名证书”部分中，单击”复制”按钮来复制 **应用联合元数据 URL** ，并将其粘贴到记事本。

    ![证书下载链接](./media/confluencemicrosoft-tutorial/tutorial_metadataurl.png)

6. 在另一个 Web 浏览器窗口中，以管理员身份登录 Confluence 实例。

7. 将鼠标悬停在小齿轮上，并单击“外接程序”。

    ![配置单一登录](./media/confluencemicrosoft-tutorial/addon1.png)

8. 从 [Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=56503)下载插件。 使用“上传加载项”菜单手动上传由 Microsoft 提供的插件。 [Microsoft 服务协议](https://www.microsoft.com/servicesagreement/)涵盖了插件下载。

    ![配置单一登录](./media/confluencemicrosoft-tutorial/addon12.png)

9. 插件安装后，它会显示在“管理加载项”部分的“用户已安装”加载项部分。 单击“配置”配置新的插件。

    ![配置单一登录](./media/confluencemicrosoft-tutorial/addon13.png)

10. 在配置页上执行下列步骤：

    ![配置单一登录](./media/confluencemicrosoft-tutorial/addon52.png)

    > [!TIP]
    > 请确保一个应用仅映射一个证书，以免在解析元数据时出错。 如果有多个证书，则管理员会在解析元数据时收到错误。

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，并单击“添加引用”。 在“元数据 URL”文本框中，粘贴从 Azure 门户复制的**应用联合元数据 URL**值，然后单击“解析”按钮。 它将读取 IdP 元数据 URL，并填充所有字段信息。

    b. 复制“标识符、回复 URL 和登录 URL”值，并将其分别粘贴到 Azure 门户中“Confluence SAML SSO by Microsoft 域和 URL”部分的“标识符、回复 URL 和登录 URL”文本框内。

    c. 在“登录按钮名”中键入组织希望用户在登录屏幕上看到的按钮名称。

    d. 在“SAML 用户 ID 位置”中，选择“用户 ID 位于 Subject 语句的 NameIdentifier 元素之中”或“用户 ID 位于 Attribute 元素之中”。  此 ID 必须是 Confluence 用户 ID。如果用户 ID 不匹配，系统将禁止用户登录。 

    > [!Note]
    > 默认 SAML 用户 ID 位置是名称标识符。 可将其更改为属性选项，并输入适当的属性名称。
    
    e. 如果选择“用户 ID 位于 Attribute 元素之中”选项，则请在“Attribute 名称”文本框内键入应该出现用户 ID 的属性名称。 

    f. 如果正在使用 Azure AD 的联合域（如 ADFS 等），请单击“启用主领域发现”选项，并配置“域名”。
    
    g. 如果是基于 ADFS 的登录，请在“域名”中键入域名。

    h. 当用户从 Confluence 注销时，如果要从 Azure AD 注销，请选择“启用单一注销”。 

    i. 单击“保存”按钮保存设置。

    > [!NOTE]
    > 有关安装和故障排除的详细信息，请访问 [MS Confluence SSO 连接器管理员指南](../ms-confluence-jira-plugin-adminguide.md)，还可以参阅[常见问题解答](../ms-confluence-jira-plugin-faq.md)以获得帮助

### <a name="creating-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

1. 在 Azure 门户的左侧窗格中，依次选择“Azure Active Directory”、“用户”和“所有用户”。

    ![创建 Azure AD 用户][100]

2. 选择屏幕顶部的“新建用户”。

    ![创建 Azure AD 测试用户](common/create_aaduser_01.png) 

3. 在“用户属性”中，按照以下步骤操作。

    ![创建 Azure AD 测试用户](common/create_aaduser_02.png)

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，并单击“添加引用”。 在“名称”字段中，输入 BrittaSimon。
  
    b. 在“用户名”字段中键入 brittasimon@yourcompanydomain.extension  
    例如： BrittaSimon@contoso.com

    c. 选择“属性”，再选择“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 选择“创建”。

### <a name="creating-confluence-saml-sso-by-microsoft-test-user"></a>创建 Confluence SAML SSO by Microsoft 测试用户

要使 Azure AD 用户能够登录 Confluence 本地服务器，必须将其预配到 Confluence SAML SSO by Microsoft 中。 对于 Confluence SAML SSO by Microsoft，预配是一项手动任务。

**若要预配用户帐户，请执行以下步骤：**

1. 以管理员身份登录到 Confluence 本地服务器。

2. 将鼠标悬停在小齿轮上，并单击“用户管理”。

    ![添加员工](./media/confluencemicrosoft-tutorial/user1.png) 

3. 在“用户”部分，单击“添加用户”选项卡。在“添加用户”对话框页上，执行以下步骤：

    ![添加员工](./media/confluencemicrosoft-tutorial/user2.png) 

    a.在“解决方案资源管理器”中，右键单击项目文件夹下的“引用”文件夹，并单击“添加引用”。 在“用户名”文本框中，键入用户（例如 Britta Simon）的电子邮件地址。

    b. 在“全名”文本框中，键入用户（例如 Britta Simon）的全名。

    c. 在“电子邮件”文本框中，键入用户的电子邮件地址（例如 Brittasimon@contoso.com）。

    d. 在“密码”文本框中，键入 Britta Simon 的密码。

    e. 单击“确认密码”，重新输入该密码。

    f. 单击“添加”按钮。

### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Confluence SAML SSO by Microsoft 的权限，允许其使用 Azure 单一登录。

1. 在 Azure 门户中，选择“企业应用程序”，然后选择“所有应用程序”。

    ![分配用户][201]

2. 在应用程序列表中，选择“Confluence SAML SSO by Microsoft”。

    ![配置单一登录](./media/confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png)

3. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202]

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

5. 在“用户和组”对话框中，选择“用户”列表中的 Britta Simon，然后单击屏幕底部的“选择”按钮。

6. 在“添加分配”对话框中，选择“分配”按钮。

### <a name="testing-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

在访问面板中单击“Confluence SAML SSO by Microsoft”磁贴时，应该会自动登录 Confluence SAML SSO by Microsoft 应用程序。
有关访问面板的详细信息，请参阅[访问面板简介](../user-help/active-directory-saas-access-panel-introduction.md)。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [Azure Active Directory 的应用程序访问与单一登录是什么？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: common/tutorial_general_01.png
[2]: common/tutorial_general_02.png
[3]: common/tutorial_general_03.png
[4]: common/tutorial_general_04.png

[100]: common/tutorial_general_100.png

[201]: common/tutorial_general_201.png
[202]: common/tutorial_general_202.png
[203]: common/tutorial_general_203.png
