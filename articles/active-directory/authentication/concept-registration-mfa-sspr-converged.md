---
title: Azure AD SSPR 和 MFA 的聚合式注册（公共预览）
description: Azure AD 多重身份验证和自助密码重置注册（公共预览）
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 12/10/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry, michmcla
ms.openlocfilehash: dbced5cfa2a47dc2fdcf630d62104bb7ba8e7bc0
ms.sourcegitcommit: 5b869779fb99d51c1c288bc7122429a3d22a0363
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2018
ms.locfileid: "53186644"
---
# <a name="converged-registration-for-self-service-password-reset-and-azure-multi-factor-authentication-public-preview"></a>针对自助密码重置和 Azure 多重身份验证的聚合式注册（公共预览）

截至目前，用户需要在两个不同的门户中注册 Azure 多重身份验证 (MFA) 和自助密码重置 (SSPR) 的身份验证方法。 Azure MFA 和 SSPR 使用类似的方法，但这些方法不同时在两个门户注册，这一点让很多用户感到困惑。 因此，某些用户无法在需要时使用 Azure MFA 或 SSPR，只得致电支持人员。 

现在，用户仅需注册一次即可同时享受 Azure MFA 和 SSPR 的益处。 用户无需为这些功能注册两次身份验证方法。  

在为组织启用此新体验之前，建议查看此文章和[用户文档](https://aka.ms/securityinfoguide)，了解该体验将对用户产生的影响。 可使用用户文档培训用户，让其准备好迎接新体验，同时帮助确保成功推广。

|     |
| --- |
| 针对自助密码重置和 Azure 多重身份验证的聚合式注册功能是 Azure Active Directory (Azure AD) 的一项公开预览功能。 有关预览版的详细信息，请参阅 [Microsoft Azure 预览版补充使用条款](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)。|
|     |

要让用户一次性注册 Azure 多重身份验证和自助密码重置的身份验证方法，请完成以下步骤：

1. 以全局管理员或用户管理员身份登录到 Azure 门户。
2. 依次浏览到“Azure Active Directory” > “用户设置” > “管理访问面板预览功能的设置”。
3. 在“用户可使用预览功能来注册和管理安全信息”下，可选择为“选定组的用户”或“所有”用户启用该选项”。

用户现可转到 [https://aka.ms/setupsecurityinfo](https://aka.ms/setupsecurityinfo) 来注册 MFA 和 SSPR 的身份验证方法。 若要详细了解用户将在此新体验中看到的内容，请参阅[用户文档](https://aka.ms/securityinfoguide)。  

> [!NOTE]
> 启用此体验后，通过新体验注册或确认其电话号码或移动应用的用户将能够将其用于 MFA 和 SSPR（如果 MFA 和 SSPR 策略中启用了这些方法）。 如果之后禁用了此体验，则对于在 https:/aka.ms/ssprsetup 处导航到旧版 SSPR 注册页的用户，需要执行多重身份验证，然后才能访问该页。  

## <a name="how-it-works"></a>工作原理

如果用户之前通过单独的 MFA 和 SSPR 注册体验注册了身份验证方法，则无需再次注册该信息。 但是，如果你的设置要求用户注册 MFA 或 SSPR，则他们可能会在登录时看到查看其安全信息的提示。

如果用户已注册可用于 MFA 的方法，则系统可能提示他们先执行多重身份验证，然后才可访问新体验。

如果已强制注册 MFA 或 SSPR，但某用户尚未注册，则系统会在其登录时提示注册。

登录时系统提示注册的用户将看到以下体验：

![聚合注册。 以新用户的身份设置方法。](./media/concept-registration-mfa-sspr-converged/concept-registration-add-methods.png)

> [!NOTE]
> 仅在系统在用户登录时提示注册的情况下才显示此体验。 对于在 https://aka.ms/setupsecurityinfo 处直接转到该体验的用户，将显示不同版本的体验（详见本文的稍后部分）。

显示的身份验证方法将基于 MFA 或 SSPR 策略中启用的方法进行更改。 系统将要求用户注册符合 MFA 策略和/或 SSPR 策略所需的最小数目的身份验证方法。 如果用户能够灵活选择可注册的身份验证方法，则可选择“选择安全信息”，从而选择其他身份验证方法。  

> [!NOTE]
> 如果支持使用移动用户通知和移动应用代码，通过通知来注册 Microsoft Authenticator 应用的用户将可使用通知和代码来验证其身份。

与之前的 MFA 注册体验不同，在进行新的注册体验时，系统不会提示用户注册应用密码。 相反，他们应遵循应用密码教程中列出的步骤，在新体验中注册应用密码。  

用户完成注册后，将自动设置其默认的 MFA 方法。 如果用户注册了验证器应用，则默认方法将设置为“应用”。 如果用户未注册验证器应用，且仅注册了其电话号码，则默认方法将设置为“电话”。 用户可转到 https://aka.ms/setupsecurityinfo，然后选择“更改默认值”来更改其默认值。  

如果不强制注册，用户可在 https://aka.ms/setupsecurityinfo 自行管理身份验证方法。 如果用户之前已注册可用于 MFA 的方法，系统将要求其执行多重身份验证，然后才可访问页面。  

![聚合注册。 以已注册用户的身份编辑方法。](./media/concept-registration-mfa-sspr-converged/concept-registration-edit-methods.png)

在此页面上，用户将看到之前注册的身份验证方法以及为其注册的身份验证方法（例如办公电话）。 用户还可添加、编辑或删除其身份验证方法（办公电话除外）。  

要查看这一新体验的审核日志，请查看审核日志的身份验证方法类别。  

## <a name="known-issues"></a>已知问题

已确定一个聚合注册 bug：启用了聚合注册的 B2B 访客用户无法注册 MFA。 将用户定向到注册页面时，页面会出错。开发人员已注意到此问题，正在努力提供解决方案。 目前，建议创建一个组并从该组中排除任何 B2B 用户。

**用户使用短信注册电话时，默认的 MFA 方法设置为“电话”**

   * 一些用户可能注意到，在其使用短信注册电话号码后，默认的 MFA 方法被设置为“电话”。 用户可以通过遵循[管理安全信息（预览）](../user-help/security-info-manage-settings.md#change-your-info)一文中的说明更改其默认方法来解决此问题。

**在管理员禁用其默认方法后，用户无法访问新的注册体验**

   * 如果管理员已禁用用户之前注册的默认 MFA 方法，则这些用户可能无法访问新的注册体验。 示例场景如下：
      1. 用户之前注册了电话号码，并将其默认方法设置为“电话”。
      2. 管理员禁止将电话作为租户的 MFA 方法。
      3. 系统在用户登录期间提示其注册，因为其需要注册其他方法以满足租户 SSPR 策略。
      4. 用户尝试注册，但由于未设置默认方法，因此无法访问该页面并卡在循环中。

## <a name="next-steps"></a>后续步骤

[了解如何部署 Azure AD 自助密码重置](howto-sspr-deployment.md)

[了解如何在登录时要求多重身份验证](howto-mfa-getstarted.md)

[了解如何配置用户身份验证方法](https://aka.ms/securityinfoguide)