---
title: 更新 Azure Stack SQL 资源提供程序 | Microsoft Docs
description: 了解如何更新 Azure Stack SQL 资源提供程序。
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
ms.date: 12/04/2018
ms.author: jeffgilb
ms.reviewer: quying
ms.openlocfilehash: 8fc8be105c6c610e6b246fa0ec619fecc81b1dd9
ms.sourcegitcommit: 5d837a7557363424e0183d5f04dcb23a8ff966bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/06/2018
ms.locfileid: "52966239"
---
# <a name="update-the-sql-resource-provider"></a>更新 SQL 资源提供程序

*适用于：Azure Stack 集成系统。*

你在将 Azure Stack 更新到新的 内部版本时，可能碰上我们发布新的 SQL 资源提供程序。 虽然现有的适配器可以继续使用，但仍建议尽快更新到最新的内部版本。

> [!IMPORTANT]
> 必须按更新的发布顺序安装更新。 不能跳过版本。 请参阅[部署资源提供程序的先决条件](./azure-stack-sql-resource-provider-deploy.md#prerequisites)中的版本列表。

## <a name="overview"></a>概述

若要更新资源提供程序，请使用 *UpdateSQLProvider.ps1* 脚本。 新 SQL 资源提供程序的下载包中提供此脚本。 更新过程类似于[部署资源提供程序](./azure-stack-sql-resource-provider-deploy.md)时使用的过程。 更新脚本与 DeploySqlProvider.ps1 脚本使用相同的参数，你需要提供证书信息。

### <a name="update-script-processes"></a>更新脚本过程

*UpdateSQLProvider.ps1* 脚本可使用最新的资源提供程序代码创建新的虚拟机 (VM)。

> [!NOTE]
> 建议从市场管理下载最新的 Windows Server 2016 Core 映像。 如需安装更新，可以将**单个** MSU 包放置在本地依赖项路径中。 如果此位置中有多个 MSU 文件，则脚本将失败。

*UpdateSQLProvider.ps1* 脚本在创建新的 VM 后，会从旧的提供程序 VM 中迁移以下设置：

* 数据库信息
* 宿主服务器信息
* 必要的 DNS 记录

### <a name="update-script-powershell-example"></a>更新脚本 PowerShell 示例

可以在权限提升的 PowerShell ISE 中编辑并运行以下脚本。 

记住按环境需要更改帐户信息和密码。

> [!NOTE]
> 此更新过程仅适用于 Azure Stack 集成系统。

```powershell
# Install the AzureRM.Bootstrapper module, set the profile and install the AzureStack module
Install-Module -Name AzureRm.BootStrapper -Force
Use-AzureRmProfile -Profile 2018-03-01-hybrid -Force
Install-Module -Name AzureStack -RequiredVersion 1.5.0

# Use the NetBIOS name for the Azure Stack domain. On the Azure Stack SDK, the default is AzureStack but this might have been changed at installation.
$domain = "AzureStack"

# For integrated systems, use the IP address of one of the ERCS virtual machines.
$privilegedEndpoint = "AzS-ERCS01"

# Provide the Azure environment used for deploying Azure Stack. Required only for Azure AD deployments. Supported values for the <environment name> parameter are AzureCloud, AzureChinaCloud or AzureUSGovernment depending which Azure subscription you are using. 
$AzureEnvironment = "<EnvironmentName>"

# Point to the directory where the resource provider installation files were extracted.
$tempDir = 'C:\TEMP\SQLRP'

# The service administrator account (this can be Azure AD or AD FS).
$serviceAdmin = "admin@mydomain.onmicrosoft.com"
$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ($serviceAdmin, $AdminPass)

# Set the credentials for the new resource provider VM.
$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

# Add the cloudadmin credential required for privileged endpoint access.
$CloudAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$CloudAdminCreds = New-Object System.Management.Automation.PSCredential ("$domain\cloudadmin", $CloudAdminPass)

# Change the following as appropriate.
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory to the folder where you extracted the installation files.
# Then adjust the endpoints.
. $tempDir\UpdateSQLProvider.ps1 -AzCredential $AdminCreds `
  -VMLocalCredential $vmLocalAdminCreds `
  -CloudAdminCredential $cloudAdminCreds `
  -PrivilegedEndpoint $privilegedEndpoint `
  -AzureEnvironment $AzureEnvironment `
  -DefaultSSLCertificatePassword $PfxPass `
  -DependencyFilesLocalPath $tempDir\cert `

 ```

## <a name="updatesqlproviderps1-parameters"></a>UpdateSQLProvider.ps1 参数

运行脚本时，可在命令行中指定以下参数。 如果未指定参数或任何参数验证失败，系统会提示提供所需的参数。

| 参数名称 | 说明 | 注释或默认值 |
| --- | --- | --- |
| **CloudAdminCredential** | 访问特权终结点时所需的云管理员凭据。 | _必需_ |
| **AzCredential** | Azure Stack 服务管理员帐户的凭据。 使用部署 Azure Stack 时所用的相同凭据。 | _必需_ |
| **VMLocalCredential** | SQL 资源提供程序 VM 的本地管理员帐户的凭据。 | _必需_ |
| **PrivilegedEndpoint** | 特权终结点的 IP 地址或 DNS 名称。 |  _必需_ |
| **AzureEnvironment** | 用于部署 Azure Stack 的服务管理员帐户的 Azure 环境。 仅对于 Azure AD 部署是必需的。 受支持的环境名称**AzureCloud**， **AzureUSGovernment**，或如果使用中国 Azure AD **AzureChinaCloud**。 | AzureCloud |
| **DependencyFilesLocalPath** | 同样必须将证书 .pfx 文件放在此目录中。 | 对单节点为可选，但对多节点为必选 |
| **DefaultSSLCertificatePassword** | .pfx 证书的密码。 | _必需_ |
| **MaxRetryCount** | 操作失败时，想要重试每个操作的次数。| 2 |
| **RetryDuration** |每两次重试的超时间隔（秒）。 | 120 |
| **卸载** | 删除资源提供程序和所有关联的资源。 | 否 |
| **DebugMode** | 防止在失败时自动清除。 | 否 |

## <a name="next-steps"></a>后续步骤

[维护 SQL 资源提供程序](azure-stack-sql-resource-provider-maintain.md)
