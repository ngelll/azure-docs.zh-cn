---
title: 管理 Azure Stack 的服务主体 |Microsoft Docs
description: 介绍如何管理新的服务主体可用于使用基于角色的访问控制 Azure 资源管理器中管理资源访问权限。
services: azure-resource-manager
documentationcenter: na
author: sethmanheim
manager: femila
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/18/2018
ms.author: sethm
ms.openlocfilehash: 50ece9edbc4bee1dea2cc61f2cdd851b278aa7b0
ms.sourcegitcommit: 549070d281bb2b5bf282bc7d46f6feab337ef248
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2018
ms.locfileid: "53720432"
---
# <a name="provide-applications-access-to-azure-stack"></a>向应用程序提供 Azure Stack 的访问权限

*适用于：Azure Stack 集成系统和 Azure Stack 开发工具包*

当应用程序需要在 Azure Stack 通过Azure 资源管理器部署或配置资源的访问权限时，请创建服务主体（它是应用程序的凭据）。 然后可以仅将必需的权限委派给该服务主体。  

例如，你可能有一个使用 Azure 资源管理器来清点 Azure 资源的配置管理工具。 在此方案中，可以创建服务主体，向该服务主体授予读者角色，并将配置管理工具限制为只能进行只读访问。 

与使用自己的凭据运行应用相比，服务主体更优，原因在于：

 - 可以向服务主体分配不同于自己的帐户权限的权限。 通常情况下，这些权限仅限于应用需执行的操作。
 - 职责变化时，无需更改应用的凭据。
 - 执行无人参与的脚本时，可使用证书自动进行身份验证。  

## <a name="getting-started"></a>入门

根据部署 Azure Stack 的方式，可以首先创建服务主体。 本文档介绍了创建服务主体：

- [Azure Active Directory (Azure AD)](#create-service-principal-for-azure-ad)。 Azure AD 是多租户、 基于云的目录和标识管理服务。 可以与已连接的 Azure Stack 配合使用 Azure AD。
- [Active Directory 联合身份验证服务 (AD FS)](#create-service-principal-for-ad-fs)。 AD FS 提供简化、 安全的标识联合身份验证和 Web 单一登录 (SSO) 功能。 使用连接和断开连接 Azure Stack 实例，可以使用 AD FS。

创建服务主体后，将使用普遍适用于 AD FS 和 Azure Active Directory 的一组步骤向角色[委派权限](#assign-role-to-service-principal)。

## <a name="manage-service-principal-for-azure-ad"></a>管理 Azure ad 服务主体

如果已部署 Azure Stack 与 Azure Active Directory (Azure AD) 为你的标识管理服务，可以创建服务主体就像 Azure。 本部分演示如何通过门户执行这些步骤。 在开始之前，请检查是否具有[所需的 Azure AD 权限](../active-directory/develop/howto-create-service-principal-portal.md#required-permissions)。

### <a name="create-service-principal"></a>创建服务主体

在本部分中，将在 Azure AD 中创建表示你的应用程序的应用程序（服务主体）。

1. 通过 [Azure 门户](https://portal.azure.com)登录到 Azure 帐户。
2. 选择“Azure Active Directory” > “应用注册” > “新建应用程序注册”
3. 为应用提供名称和 URL。 选择“Web 应用/API”或“本机”作为要创建的应用程序的类型。 设置这些值后，选择“创建”。

已为应用程序创建服务主体。

### <a name="get-credentials"></a>获取凭据

以编程方式登录时，需要使用应用程序、Web 应用/API 的 ID 和身份验证密钥。 若要获取这些值，请使用以下步骤：

1. 从 Active Directory 中的“应用注册”，选择应用程序。

2. 复制“应用程序 ID”并将其存储在应用程序代码中。 [示例应用程序](#sample-applications)部分的应用程序引用此值作为客户端 ID。

     ![客户端 ID](./media/azure-stack-create-service-principal/image12.png)
3. 若要为 Web 应用/API 生成身份验证密钥，请选择“设置” > “密钥”。 

4. 提供密钥说明和密钥持续时间。 完成后，选择“保存”。

保存密钥后, 会显示密钥的值。 将此值复制到记事本或其他某个临时位置，因为以后无法检索该密钥。 提供密钥值及应用程序 ID 登录为该应用程序。 将密钥值存储在应用程序可检索的位置。

![保存的密钥](./media/azure-stack-create-service-principal/image15.png)

完成后，你可以[将你的应用程序角色分配](#assign-role-to-service-principal)。

## <a name="manage-service-principal-for-ad-fs"></a>管理适用于 AD FS 服务主体

如果你部署 Azure Stack 与 Active Directory 联合身份验证服务 (AD FS) 作为标识管理服务，使用 PowerShell 创建服务主体、 分配角色的访问权限，并使用该标识登录。

可以使用两种方法之一来使用 AD FS 创建服务主体。 可以：
 - [创建服务主体使用的证书](azure-stack-create-service-principals.md#create-a-service-principal-using-a-certificate)
 - [创建服务主体使用的客户端机密](azure-stack-create-service-principals.md#create-a-service-principal-using-a-client-secret)

管理 AD FS 的任务的服务主体。

| 类型 | 操作 |
| --- | --- |
| AD FS 证书 | [创建](azure-stack-create-service-principals.md#create-a-service-principal-using-a-certificate) |
| AD FS 证书 | [更新](azure-stack-create-service-principals.md#update-certificate-for-service-principal-for-AD-FS) |
| AD FS 证书 | [Remove](azure-stack-create-service-principals.md#remove-a-service-principal-for-AD-FS) |
| AD FS 客户端机密 | [创建](azure-stack-create-service-principals.md#create-a-service-principal-using-a-client-secret) |
| AD FS 客户端机密 | [更新](azure-stack-create-service-principals.md#create-a-service-principal-using-a-client-secret) |
| AD FS 客户端机密 | [Remove](azure-stack-create-service-principals.md##remove-a-service-principal-for-AD-FS) |

### <a name="create-a-service-principal-using-a-certificate"></a>创建服务主体使用的证书

在创建时的服务主体将 AD FS 用于标识时，可以使用证书。

#### <a name="certificate"></a>证书

需要证书。

**证书要求**

 - 加密服务提供程序 (CSP) 必须是旧密钥提供程序。
 - 证书格式必须是 PFX 文件，因为公钥和私钥都是必需的。 Windows 服务器使用包含公钥文件（SSL 证书文件）和关联的私钥文件的 .pfx 文件。
 - 对于生产环境，证书必须由内部证书颁发机构或公共证书颁发机构颁发。 如果你使用公共证书颁发机构，则必须将基础操作系统映像中的颁发机构包括为 Microsoft 信任根颁发机构计划的一部分。 可以在 [Microsoft 信任根证书计划：参与者](https://gallery.technet.microsoft.com/Trusted-Root-Certificate-123665ca)中找到完整列表。
 - Azure Stack 基础结构必须能够通过网络访问证书中发布的证书颁发机构的证书吊销列表 (CRL) 位置。 此 CRL 必须是一个 HTTP 终结点。

#### <a name="parameters"></a>parameters

以下信息是作为自动化参数的输入所必需的：

|参数|描述|示例|
|---------|---------|---------|
|名称|SPN 帐户的名称|MyAPP|
|ClientCertificates|证书对象的数组|X509 证书|
|ClientRedirectUris<br>(可选)|应用程序重定向 URI|-|

#### <a name="use-powershell-to-create-a-service-principal"></a>使用 PowerShell 创建服务主体

1. 打开提升的 Windows PowerShell 会话，并运行以下 cmdlet:

   ```PowerShell  
    # Credential for accessing the ERCS PrivilegedEndpoint, typically domain\cloudadmin
    $creds = Get-Credential

    # Creating a PSSession to the ERCS PrivilegedEndpoint
    $session = New-PSSession -ComputerName <ERCS IP> -ConfigurationName PrivilegedEndpoint -Credential $creds

    # If you have a managed certificate use the Get-Item command to retrieve your certificate from your certificate location.
    # If you don't want to use a managed certificate, you can produce a self signed cert for testing purposes: 
    # $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=<yourappname>" -KeySpec KeyExchange
    $cert = Get-Item "<yourcertificatelocation>"
    
    $ServicePrincipal = Invoke-Command -Session $session -ScriptBlock { New-GraphApplication -Name '<yourappname>' -ClientCertificates $using:cert}
    $AzureStackInfo = Invoke-Command -Session $session -ScriptBlock { get-azurestackstampinformation }
    $session|remove-pssession

    # For Azure Stack development kit, this value is set to https://management.local.azurestack.external. This is read from the AzureStackStampInformation output of the ERCS VM.
    $ArmEndpoint = $AzureStackInfo.TenantExternalEndpoints.TenantResourceManager

    # For Azure Stack development kit, this value is set to https://graph.local.azurestack.external/. This is read from the AzureStackStampInformation output of the ERCS VM.
    $GraphAudience = "https://graph." + $AzureStackInfo.ExternalDomainFQDN + "/"

    # TenantID for the stamp. This is read from the AzureStackStampInformation output of the ERCS VM.
    $TenantID = $AzureStackInfo.AADTenantID

    # Register an AzureRM environment that targets your Azure Stack instance
    Add-AzureRMEnvironment `
    -Name "AzureStackUser" `
    -ArmEndpoint $ArmEndpoint

    # Set the GraphEndpointResourceId value
    Set-AzureRmEnvironment `
    -Name "AzureStackUser" `
    -GraphAudience $GraphAudience `
    -EnableAdfsAuthentication:$true

    Add-AzureRmAccount -EnvironmentName "azurestackuser" `
    -ServicePrincipal `
    -CertificateThumbprint $ServicePrincipal.Thumbprint `
    -ApplicationId $ServicePrincipal.ClientId `
    -TenantId $TenantID

    # Output the SPN details
    $ServicePrincipal

   ```
   > [!Note]  
   > 出于验证目的可以创建自签名的证书，使用下面的示例：

   ```PowerShell  
   $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=<yourappname>" -KeySpec KeyExchange
   ```


2. 自动化完成后，它将显示使用该 SPN 所需的详细信息。 建议用于存储输出以供将来使用。

   例如：

   ```shell
   ApplicationIdentifier : S-1-5-21-1512385356-3796245103-1243299919-1356
   ClientId              : 3c87e710-9f91-420b-b009-31fa9e430145
   Thumbprint            : 30202C11BE6864437B64CE36C8D988442082A0F1
   ApplicationName       : Azurestack-MyApp-c30febe7-1311-4fd8-9077-3d869db28342
   PSComputerName        : azs-ercs01
   RunspaceId            : a78c76bb-8cae-4db4-a45a-c1420613e01b
   ```

### <a name="update-certificate-for-service-principal-for-ad-fs"></a>更新服务主体证书适用于 AD FS

如果已部署 Azure Stack 与 AD FS，可以使用 PowerShell 来更新服务主体的密码。

从 ERCS 虚拟机上的特权终结点运行脚本。

#### <a name="parameters"></a>parameters

以下信息是作为自动化参数的输入所必需的：

|参数|描述|示例|
|---------|---------|---------|
|名称|SPN 帐户的名称|MyAPP|
|ApplicationIdentifier|唯一标识符|S-1-5-21-1634563105-1224503876-2692824315-2119|
|ClientCertificate|证书对象的数组|X509 证书|

#### <a name="example-of-updating-service-principal-for-ad-fs"></a>更新适用于 AD FS 服务主体的示例

该示例创建自签名的证书。 在生产部署中运行这些 cmdlet，使用[Get-item](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Management/Get-Item)检索你想要使用的证书的证书对象。

1. 打开提升的 Windows PowerShell 会话，并运行以下 cmdlet:

     ```powershell
          # Creating a PSSession to the ERCS PrivilegedEndpoint
          $session = New-PSSession -ComputerName <ERCS IP> -ConfigurationName PrivilegedEndpoint -Credential $creds

          # This produces a self signed cert for testing purposes. It is preferred to use a managed certificate for this.
          $Newcert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=<yourappname>" -KeySpec KeyExchange

          $RemoveServicePrincipal = Invoke-Command -Session $session -ScriptBlock {Set-GraphApplication -ApplicationIdentifier  S-1-5-21-1634563105-1224503876-2692824315-2120 -ClientCertificates $Newcert}

          $session|remove-pssession
     ```

2. 自动化完成后，它将显示为 SPN 身份验证所需的更新的指纹值。

     ```Shell  
          ClientId              : 
          Thumbprint            : AF22EE716909041055A01FE6C6F5C5CDE78948E9
          ApplicationName       : Azurestack-ThomasAPP-3e5dc4d2-d286-481c-89ba-57aa290a4818
          ClientSecret          : 
          RunspaceId            : a580f894-8f9b-40ee-aa10-77d4d142b4e5
     ```

### <a name="create-a-service-principal-using-a-client-secret"></a>创建服务主体使用的客户端机密

在创建时的服务主体将 AD FS 用于标识时，可以使用证书。 特权的终结点将用于运行这些 cmdlet。

从特权终结点 ERCS 虚拟机上运行这些脚本。 有关特权终结点的详细信息，请参阅[在 Azure Stack 中使用特权终结点](https://docs.microsoft.com/azure/azure-stack/azure-stack-privileged-endpoint)。

#### <a name="parameters"></a>parameters

以下信息是作为自动化参数的输入所必需的：

| 参数 | 描述 | 示例 |
|----------------------|--------------------------|---------|
| 名称 | SPN 帐户的名称 | MyAPP |
| GenerateClientSecret | 创建机密 |  |

#### <a name="use-the-ercs-privilegedendpoint-to-create-the-service-principal"></a>使用 ERCS PrivilegedEndpoint 创建服务主体

1. 打开提升的 Windows PowerShell 会话，并运行以下 cmdlet:

     ```PowerShell  
      # Credential for accessing the ERCS PrivilegedEndpoint, typically domain\cloudadmin
     $creds = Get-Credential

     # Creating a PSSession to the ERCS PrivilegedEndpoint
     $session = New-PSSession -ComputerName <ERCS IP> -ConfigurationName PrivilegedEndpoint -Credential $creds

     # Creating a SPN with a secre
     $ServicePrincipal = Invoke-Command -Session $session -ScriptBlock { New-GraphApplication -Name '<yourappname>' -GenerateClientSecret}
     $AzureStackInfo = Invoke-Command -Session $session -ScriptBlock { get-azurestackstampinformation }
     $session|remove-pssession

     # Output the SPN details
     $ServicePrincipal
     ```

2. Cmdlet 运行后，shell 会显示使用该 SPN 所需的详细信息。 请确保存储客户端机密。

     ```PowerShell  
     ApplicationIdentifier : S-1-5-21-1634563105-1224503876-2692824315-2623
     ClientId              : 8e0ffd12-26c8-4178-a74b-f26bd28db601
     Thumbprint            : 
     ApplicationName       : Azurestack-YourApp-6967581b-497e-4f5a-87b5-0c8d01a9f146
     ClientSecret          : 6RUZLRoBw3EebMDgaWGiowCkoko5_j_ujIPjA8dS
     PSComputerName        : 192.168.200.224
     RunspaceId            : 286daaa1-c9a6-4176-a1a8-03f543f90998
     ```

#### <a name="update-client-secret-for-a-service-principal-for-ad-fs"></a>适用于 AD FS 更新服务主体的客户端机密

新的客户端密码是自动生成的 PowerShell cmdlet。

从 ERCS 虚拟机上的特权终结点运行脚本。

##### <a name="parameters"></a>parameters

以下信息是作为自动化参数的输入所必需的：

| 参数 | 描述 | 示例 |
|-----------------------|-----------------------------------------------------------------------------------------------------------|------------------------------------------------|
| ApplicationIdentifier | 唯一标识符。 | S-1-5-21-1634563105-1224503876-2692824315-2119 |
| ChangeClientSecret | 更改客户端密码滚动更新周期为 2880 分钟旧密钥将仍然有效。 |  |
| ResetClientSecret | 立即更改客户端机密 |  |

##### <a name="example-of-updating-a-client-secret-for-ad-fs"></a>更新适用于 AD FS 的客户端机密的示例

该示例使用**resetclientsecret**参数，它立即更改客户端机密。

1. 打开提升的 Windows PowerShell 会话，并运行以下 cmdlet:

     ```PowerShell  
          # Creating a PSSession to the ERCS PrivilegedEndpoint
          $session = New-PSSession -ComputerName <ERCS IP> -ConfigurationName PrivilegedEndpoint -Credential $creds

          # This produces a self signed cert for testing purposes. It is preferred to use a managed certificate for this.
          $Newcert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=<yourappname>" -KeySpec KeyExchange

          $UpdateServicePrincipal = Invoke-Command -Session $session -ScriptBlock {Set-GraphApplication -ApplicationIdentifier  S-1-5-21-1634563105-1224503876-2692824315-2120 -ResetClientSecret}

          $session|remove-pssession
     ```

2. 自动化完成后，它将显示 SPN 身份验证所需的新生成的机密。 请确保将新的客户端机密存储。

     ```PowerShell  
          ApplicationIdentifier : S-1-5-21-1634563105-1224503876-2692824315-2120
          ClientId              :  
          Thumbprint            : 
          ApplicationName       : Azurestack-Yourapp-6967581b-497e-4f5a-87b5-0c8d01a9f146
          ClientSecret          : MKUNzeL6PwmlhWdHB59c25WDDZlJ1A6IWzwgv_Kn
          RunspaceId            : 6ed9f903-f1be-44e3-9fef-e7e0e3f48564
     ```

### <a name="remove-a-service-principal-for-ad-fs"></a>删除适用于 AD FS 服务主体

如果已部署 Azure Stack 与 AD FS，可以使用 PowerShell 删除服务主体。

从 ERCS 虚拟机上的特权终结点运行脚本。

#### <a name="parameters"></a>parameters

以下信息是作为自动化参数的输入所必需的：

|参数|描述|示例|
|---------|---------|---------|
| 参数 | 描述 | 示例 |
| ApplicationIdentifier | 唯一标识符 | S-1-5-21-1634563105-1224503876-2692824315-2119 |

> [!Note]  
> 若要查看所有现有服务主体和其应用程序标识符的列表，可以使用 get graphapplication 命令。

#### <a name="example-of-removing-the-service-principal-for-ad-fs"></a>删除 AD FS 的服务主体的示例

```powershell  
     Credential for accessing the ERCS PrivilegedEndpoint, typically domain\cloudadmin
     $creds = Get-Credential

     # Creating a PSSession to the ERCS PrivilegedEndpoint
     $session = New-PSSession -ComputerName <ERCS IP> -ConfigurationName PrivilegedEndpoint -Credential $creds

     $UpdateServicePrincipal = Invoke-Command -Session $session -ScriptBlock { Remove-GraphApplication -ApplicationIdentifier S-1-5-21-1634563105-1224503876-2692824315-2119}

     $session|remove-pssession
```

## <a name="assign-a-role"></a>分配角色

要访问订阅中的资源，必须将应用程序分配到角色。 决定哪个角色表示应用程序的相应权限。 若要了解有关可用角色的信息，请参阅 [RBAC：内置角色](../role-based-access-control/built-in-roles.md)。

可将作用域设置为订阅、资源组或资源级别。 较低级别的作用域将继承权限。 例如，将某个应用程序添加到资源组的“读取者”角色意味着该应用程序可以读取该资源组及其包含的所有资源。

1. 在 Azure Stack 门户中，导航到要将应用程序分配到的作用域级别。 例如，若要在订阅范围内分配角色，选择“订阅”。 可改为选择资源组或资源。

2. 选择特定订阅（资源组或资源），向其中分配应用程序。

     ![选择进行分配的订阅](./media/azure-stack-create-service-principal/image16.png)

3. 选择“访问控制 (IAM)”。

     ![选择访问权限](./media/azure-stack-create-service-principal/image17.png)

4. 选择“添加角色分配”。

5. 选择要分配到应用程序的角色。

6. 搜索你的应用程序，并选择它。

7. 选择“确定”完成角色分配。 该应用程序会显示在分配到该范围角色的用户列表中。

既然已创建服务主体并已分配角色，可以开始在应用程序中使用此服务主体访问 Azure Stack 资源。  

## <a name="next-steps"></a>后续步骤

[为 AD FS 添加用户](azure-stack-add-users-adfs.md)  
[管理用户权限](azure-stack-manage-permissions.md)  
[Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory)  
[Active Directory 联合身份验证服务](https://docs.microsoft.com/windows-server/identity/active-directory-federation-services)
