---
author: rayne-wiselman
ms.service: backup
ms.topic: include
ms.date: 11/09/2018
ms.author: raynew
ms.openlocfilehash: e62771096bc59bc05879ce7b7e2da19f050b27b0
ms.sourcegitcommit: 8d88a025090e5087b9d0ab390b1207977ef4ff7c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2018
ms.locfileid: "52279463"
---
## <a name="defining-a-backup-policy"></a>定义备份策略
备份策略定义由数据快照创建时间和这些快照的保留时间长度构成的矩阵。 定义 VM 的备份策略时，可以 *一天一次*地触发备份作业。 创建新策略时，该策略将应用到保管库。 备份策略界面如下所示：

![备份策略](./media/backup-create-policy-for-vms/backup-policy.png)

若要创建策略，请执行以下操作：

1. 输入 **策略名称**。
2. 数据快照可按“每日”或“每周”的间隔来创建。 使用“备份频率”下拉菜单来选择要“每日”还是“每周”创建数据快照。
   
   * 如果选择“每日”间隔，可使用突出显示的控件来选择要在一天中的什么时间创建快照。 要更改小时，请取消选择该小时值，并选择新的小时值。
     
     ![每日备份策略](./media/backup-create-policy-for-vms/backup-policy-daily.png) <br/>
   * 如果选择“每周”间隔，可使用突出显示的控件来选择要在哪个星期日期，以及该日期的什么时间创建快照。 在日期菜单中选择一个或多个日期。 在小时菜单中选择某个小时。 要更改小时，请取消选择选定的小时值，并选择新的小时值。
     
     ![每周备份策略](./media/backup-create-policy-for-vms/backup-policy-weekly.png)
3. 默认情况下，已选择所有“保留范围”选项。 请取消选中任何不想要使用的保留范围限制。 然后，指定要使用的时间间隔。
   
    使用每月和每年保留范围，可以基于每周或每日增量指定快照。
   
   > [!NOTE]
   > 在保护 VM 时，备份作业将每天运行一次。 每个保留范围的备份运行时间相同。
   > 
   > 
4. 设置策略的所有选项后，在边栏选项卡顶部单击“保存”。
   
    新策略将立即应用于保管库。

