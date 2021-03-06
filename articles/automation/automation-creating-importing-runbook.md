---
title: 在 Azure 自动化中创建或导入 Runbook
description: 本文介绍了如何在 Azure 自动化中创建新的 Runbook，或如何从文件中导入 Runbook。
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 08/06/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: 2ccf9036d3701c710c6d3258f81390ed355c246c
ms.sourcegitcommit: 615403e8c5045ff6629c0433ef19e8e127fe58ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39578025"
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>在 Azure 自动化中创建或导入 Runbook

可以通过以下方法将 Runbook 添加到 Azure 自动化：[创建新的 Runbook](#creating-a-new-runbook)；从文件或 [Runbook 库](automation-runbook-gallery.md)导入现有 Runbook。 本文介绍如何通过文件创建和导入 Runbook。  可以在 [Azure 自动化的 Runbook 和模块库](automation-runbook-gallery.md)中获取有关如何访问社区 Runbook 和模块的所有详细信息。

## <a name="creating-a-new-runbook"></a>创建新的 Runbook

可以使用其中一个 Azure 门户或 Windows PowerShell 在 Azure 自动化中创建一个新的 Runbook。 一旦创建了 Runbook，便可以利用[了解 PowerShell 工作流](automation-powershell-workflow.md)和 [Azure 自动化中的图形创作](automation-graphical-authoring-intro.md)中的信息对其进行编辑。

### <a name="to-create-a-new-azure-automation-runbook-with-the-azure-portal"></a>使用 Azure 门户创建新的 Azure 自动化 Runbook

1. 在 Azure 门户中，打开自动化帐户。
1. 从中心单击“Runbook”，打开 Runbook 的列表。
1. 单击“添加 Runbook”按钮，并单击“创建新 Runbook”。
1. 键入 Runbook 的**名称**，并选择其[类型](automation-runbook-types.md)。 Runbook 名称必须以字母开头，可以使用字母、数字、下划线和短划线。
1. 单击“创建”以创建 Runbook 并打开编辑器。

### <a name="to-create-a-new-azure-automation-runbook-with-windows-powershell"></a>使用 Windows PowerShell 创建新的 Azure 自动化 Runbook
可以使用 [New-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/new-azurermautomationrunbook) cmdlet 创建空的 [PowerShell 工作流 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。 还应包括 **Type** 参数，以指定四种 Runbook 类型之一。

以下示例命令演示了如何创建新的空 Runbook。

```azurepowershell-interactive
New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
-Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell
```

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>将 Runbook 从文件导入 Azure 自动化

可以在 Azure 自动化中创建新的 Runbook，方法是导入 PowerShell 脚本或 PowerShell 工作流（扩展名为 .ps1）、导出的图形 Runbook (.graphrunbook) 或 Python 2 脚本（扩展名为.py）。  必须指定在导入期间创建的 [Runbook 类型](automation-runbook-types.md)，并考虑以下注意事项。

* .graphrunbook 文件只能导入到新的[图形 Runbook](automation-runbook-types.md#graphical-runbooks) 中，并且只能从 .graphrunbook 文件创建图形 Runbook。
* 包含 PowerShell 工作流的 .ps1 文件只能导入到 [PowerShell 工作流 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 中。  如果该文件包含多个 PowerShell 工作流，导入会失败。 必须将每个工作流保存到各自的文件中，并分别导入每个工作流。
* 不包含工作流的 .ps1 文件可以导入到 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 中，也可以导入到 [PowerShell 工作流 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 中。  如果将它导入到 PowerShell 工作流 Runbook 中，则会将其转换为工作流，并会在 Runbook 中添加注释，详述所做的更改。

### <a name="to-import-a-runbook-from-a-file-with-the-azure-portal"></a>使用 Azure 门户通过文件导入 Runbook

可通过以下过程将脚本文件导入 Azure 自动化。  

> [!NOTE]
> 请注意，只能通过此门户将 .ps1 文件导入 PowerShell 工作流 Runbook。

1. 在 Azure 门户中，打开自动化帐户。
2. 从中心单击“Runbook”，打开 Runbook 的列表。
3. 单击“添加 Runbook”按钮，并单击“导入”。
4. 单击“Runbook 文件”以选择要导入的文件
5. 如果“名称”字段已启用，则可以选择更改它。  Runbook 名称必须以字母开头，可以使用字母、数字、下划线和短划线。
6. 将自动选择 [Runbook 类型](automation-runbook-types.md)，但可以在考虑适用的限制后更改该类型。 
7. 新的 runbook 会出现在自动化帐户的 runbook 列表中。
8. 必须先[发布 Runbook](#publishing-a-runbook)，才能运行它。

> [!NOTE]
> 在导入图形 Runbook 或图形 PowerShell 工作流 Runbook 后，可以选择转换为其他类型（如果需要）。 无法转换为文本 runbook。
>  
> 

### <a name="to-import-a-runbook-from-a-script-file-with-windows-powershell"></a>使用 Windows PowerShell 从脚本文件中导入 Runbook
可以使用 [Import-AzureRMAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/import-azurermautomationrunbook) cmdlet 将脚本文件导入为 PowerShell 工作流 Runbook 草稿。 如果 Runbook 已存在，除非使用 *-Force* 参数，否则导入会失败。 

下面的示例命令演示了如何将脚本文件导入到 Runbook 中。

```azurepowershell-interactive
$automationAccountName =  "AutomationAccount"
$runbookName = "Sample_TestRunbook"
$scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
$RGName = "ResourceGroup"

Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
-ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
-Type PowerShellWorkflow
```

## <a name="publishing-a-runbook"></a>发布 Runbook

创建或导入新的 Runbook 时，必须先将其发布，然后才能导入。  自动化中的每个 Runbook 都有草稿版和已发布版。 只有已发布版才能用来运行，只有草稿版才能用来编辑。 已发布版不受对草稿版所做的任何更改的影响。 当草稿版可以使用时，可以发布草稿版，这样草稿版就会覆盖已发布版。

## <a name="to-publish-a-runbook-using-the-azure-portal"></a>使用 Azure 门户发布 Runbook

1. 在 Azure 门户中打开 Runbook。
1. 单击“编辑”按钮。
1. 单击“发布”按钮，并在出现验证消息时单击“是”。

## <a name="to-publish-a-runbook-using-windows-powershell"></a>使用 Windows PowerShell 发布 Runbook
可以使用 Windows PowerShell，通过 [Publish-AzureRmAutomationRunbook](https://docs.microsoft.com/powershell/module/azurerm.automation/publish-azurermautomationrunbook) cmdlet 来发布 Runbook。 以下示例命令显示了如何发布示例 Runbook。

```azurepowershell-interactive
$automationAccountName =  "AutomationAccount"
$runbookName = "Sample_TestRunbook"
$RGName = "ResourceGroup"

Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
-Name $runbookName -ResourceGroupName $RGName
```

## <a name="next-steps"></a>后续步骤

* 要了解可以如何从 Runbook 和 PowerShell 模块库中受益，请参阅 [Azure 自动化的 Runbook 和模块库](automation-runbook-gallery.md)
* 若要了解有关使用文本编辑器编辑 PowerShell 和 PowerShell 工作流 Runbook 的详细信息，请参阅 [编辑 Azure 自动化中的文本 Runbook](automation-edit-textual-runbook.md)
* 若要详细了解图形 Runbook 创作，请参阅 [Azure 自动化中的图形创作](automation-graphical-authoring-intro.md)