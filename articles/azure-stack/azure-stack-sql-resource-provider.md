---
title: 在 Azure Stack 中使用 SQL 数据库 | Microsoft Docs
description: 了解如何在 Azure Stack 中部署 SQL 数据库即服务，并通过便捷的步骤部署 SQL Server 资源提供程序适配器。
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2018
ms.author: jeffgilb
ms.reviewer: quying
ms.openlocfilehash: 3d608843ef31a1ed665fcb1fd90b822f34f77fdd
ms.sourcegitcommit: 5de9de61a6ba33236caabb7d61bee69d57799142
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50086346"
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a>Microsoft Azure Stack 上使用 SQL 数据库

使用 SQL Server 资源提供程序适配器来提供服务的 SQL 数据库[Azure Stack](azure-stack-poc.md)。 安装资源提供程序并将它连接到一个或多个 SQL Server 实例之后，你和用户可以创建：

- 适用于云原生应用的数据库。
- 使用 SQL 的网站。
- 使用 SQL 的工作负荷。

该资源提供程序并未提供 [Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)的所有数据库管理功能。 例如，它不支持自动分配资源的弹性池。 但是，该资源提供程序支持对 SQL Server 数据库执行类似的创建、读取、更新和删除 (CRUD) 操作。 

## <a name="sql-resource-provider-adapter-architecture"></a>SQL 资源提供程序适配器体系结构

该资源提供程序由以下三个组件构成：

- **SQL 资源提供程序适配器虚拟机 (VM)**，这是运行提供程序服务的 Windows Server VM。
- **资源提供程序**，它处理请求并访问数据库资源。
- **托管 SQL 服务器的服务器**，为称作宿主服务器的数据库提供容量。

必须创建至少一个 SQL Server 实例，或者提供对外部 SQL Server 实例的访问权限。

> [!NOTE]
> 必须通过租户订阅创建安装在 Azure Stack 集成系统上的宿主服务器， 而不能通过默认提供商订阅创建。 必须从租户门户或者使用 PowerShell 以及相应的登录名来创建它们。 所有宿主服务器都是可计费的虚拟机，并且必须具有许可证。 服务管理员可以是租户订阅的所有者。

## <a name="next-steps"></a>后续步骤

[部署 SQL Server 资源提供程序](azure-stack-sql-resource-provider-deploy.md)
