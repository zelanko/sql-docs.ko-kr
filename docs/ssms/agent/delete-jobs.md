---
title: 작업 삭제
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d9b62de40a27cf7ebe6422f7ce64124cde0273ca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242474"
---
# <a name="delete-jobs"></a>작업 삭제
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

작업이란 SQL Server 에이전트가 순차적으로 수행하는 일련의 지정된 작업입니다. 기본적으로 실행이 완료되어도 작업은 삭제되지 않습니다. 작업의 성공 또는 실패에 관계없이 하나 이상의 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 삭제할 수 있습니다. 작업이 성공, 실패 또는 완료되었을 때 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성할 수도 있습니다.  
  
기본적으로 **sysadmin** 고정 서버 역할의 멤버는 [sp_delete_job(Transact-SQL)](https://msdn.microsoft.com/b85db6e4-623c-41f1-9643-07e5ea38db09) 시스템 저장 프로시저를 실행하여 작업을 삭제할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
**sysadmin** 고정 서버 역할의 멤버만 **sp_delete_job** 을 실행하여 모든 작업을 삭제할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자는 해당 사용자가 소유한 작업만 삭제할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|하나 이상의 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 삭제하는 방법에 대해 설명합니다.|[하나 이상의 작업 삭제](../../ssms/agent/delete-one-or-more-jobs.md)|  
|작업이 성공, 실패 또는 완료되었을 때 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성하는 방법에 대해 설명합니다.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
