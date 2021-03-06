---
title: 如何配置 Azure SQL 数据库 - 单一实例 | Microsoft Docs
description: 了解如何配置和管理“Azure SQL 数据库 - 单一数据库”。
services: sql-database
ms.service: sql-database
ms.subservice: ''
ms.custom: ''
ms.devlang: ''
ms.topic: howto
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: carlr
manager: craigg
ms.date: 12/14/2018
ms.openlocfilehash: d34853220e423e73c6ca8cf7c76ba616b815b8bd
ms.sourcegitcommit: c2e61b62f218830dd9076d9abc1bbcb42180b3a8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2018
ms.locfileid: "53439744"
---
# <a name="how-to-use-single-database"></a>如何使用单一数据库

在本部分中，你可以找到可帮助你管理和配置“Azure SQL 数据库 - 单一数据库”的各种指南、脚本和说明。

## <a name="migrate"></a>迁移

- [迁移到 SQL 数据库](sql-database-cloud-migrate.md) – 了解迁移到托管实例时建议使用的迁移流程和工具。
- 了解如何[在迁移后管理 SQL 数据库](sql-database-manage-after-migration.md)。

## <a name="configure-features"></a>配置功能

- [配置事务性复制](replication-to-sql-database.md)以在数据库之间复制数据。
- [配置威胁检测](sql-database-threat-detection.md)来让 Azure SQL 数据库识别可疑活动，例如 SQL 注入或来自可疑位置的访问。
- [配置动态数据掩码](sql-database-dynamic-data-masking-get-started-portal.md)来保护敏感数据。
- 为数据库[配置备份保留](sql-database-long-term-backup-retention-configure.md)以在 Azure Blob 存储上保留备份。 作为替代方法，还提供了[使用 Azure 保管库配置备份保留（已弃用）](sql-database-long-term-backup-retention-configure-vault.md)方法。
- [配置异地复制](sql-database-geo-replication-portal.md)以将数据库副本保留在另一个区域中。
- [为异地副本配置安全性](sql-database-geo-replication-security-config.md)。

## <a name="monitor-and-tune-your-database"></a>监视和优化数据库

- [启用自动优化](sql-database-automatic-tuning-enable.md)来让 Azure SQL 数据库优化工作负荷的性能。
- [启用自动优化的电子邮件通知](sql-database-automatic-tuning-email-notifications.md)以获取有关优化建议的信息。
- [应用性能建议](sql-database-advisor-portal.md)并优化数据库。
- [创建警报](sql-database-insights-alerts-portal.md)以从 Azure SQL 数据库获取通知。
- [排查连接问题](sql-database-troubleshoot-common-connection-issues.md)：如果发现应用程序与数据库之间存在某些连接问题。 还可以[使用“资源运行状况”来排查连接问题](sql-database-resource-health.md)。
- [管理文件空间](sql-database-file-space-management.md)来监视数据库中的存储使用情况。

## <a name="query-distributed-data"></a>查询分布式数据

- 跨多个数据库[查询垂直分区的数据](sql-database-elastic-query-getting-started-vertical.md)。
- [跨横向扩展的数据层进行报告](sql-database-elastic-query-horizontal-partitioning.md)。
- [在具有不同架构的表中进行查询](sql-database-elastic-query-vertical-partitioning.md)。

## <a name="elastic-database-jobs"></a>弹性数据库作业

- 使用 PowerShell [创建和管理](elastic-jobs-powershell.md)弹性数据库作业。
- 使用 Transact-SQL [创建和管理](elastic-jobs-tsql.md)弹性数据库作业。
- [从旧的弹性作业进行迁移](elastic-jobs-migrate.md)。

## <a name="database-sharding"></a>数据库分片

- [升级弹性数据库客户端库](sql-database-elastic-scale-upgrade-client-library.md)。
- [创建分片应用](sql-database-elastic-scale-get-started.md)。
- [查询水平分片的数据](sql-database-elastic-query-getting-started.md)。
- 运行[多分片查询](sql-database-elastic-scale-multishard-querying.md)。
- [移动分片数据](sql-database-elastic-scale-configure-deploy-split-and-merge.md)。
- 在数据库分片中[配置安全性](sql-database-elastic-scale-split-merge-security-configuration.md)。
- 向当前的数据库分片集[添加分片](sql-database-elastic-scale-add-a-shard.md)。
- [解决分片映射问题](sql-database-elastic-database-recovery-manager.md)。
- [迁移分片 DB](sql-database-elastic-convert-to-use-elastic-tools.md)。
- [创建计数器](sql-database-elastic-database-perf-counters.md)。
- [使用实体框架](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)查询分片的数据。
- [使用 Dapper 框架](sql-database-elastic-scale-working-with-dapper.md)查询分片的数据。

## <a name="next-steps"></a>后续步骤
- 详细了解[托管实例中的操作指南](sql-database-howto-managed-instance.md)
