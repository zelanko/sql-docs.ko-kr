---
description: 방화벽 규칙 저장 프로시저 (Azure SQL Database)
title: 방화벽 규칙 저장 프로시저
titleSuffix: Azure SQL Database
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- firewall rules stored procedures
- firewall_rules, setting
- firewall_rules, Azure SQL Database
- firewall systems, Azure SQL Database
ms.assetid: 3d4c2585-00de-46b5-8eee-0efb71cb3aea
author: VanMSFT
ms.author: vanto
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: f4597a05c6f1376a39d98894d6e510b7928a450d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474664"
---
# <a name="firewall-rules-stored-procedures-azure-sql-database"></a>방화벽 규칙 저장 프로시저 (Azure SQL Database)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  이 섹션에는 방화벽 규칙을 설정 또는 삭제하는 다음과 같은 저장 프로시저가 있습니다. [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 방화벽 규칙은 및와 함께 사용할 수 있습니다 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] . 자세한 내용은 [Azure SQL Database 방화벽 규칙 구성-개요](/azure/azure-sql/database/firewall-configure)를 참조 하세요.

:::row:::
    :::column:::
        [sp_set_firewall_rule&#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [sp_set_database_firewall_rule&#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
    :::column:::
        [sp_delete_database_firewall_rule &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)
    :::column-end:::
:::row-end:::

&nbsp;
  
의 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 경우 Window 방화벽 규칙을 사용 합니다. 자세한 내용은 [데이터베이스 엔진 액세스에 대한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)을 참조하세요.   
