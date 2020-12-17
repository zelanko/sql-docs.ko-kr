---
description: 작업 삭제
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
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: c494163b12b3b5a0b374ac5143b5da3d45ad5d08
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97423818"
---
# <a name="delete-jobs"></a>작업 삭제
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

작업이란 SQL Server 에이전트가 순차적으로 수행하는 일련의 지정된 작업입니다. 기본적으로 실행이 완료되어도 작업은 삭제되지 않습니다. 작업의 성공 또는 실패에 관계없이 하나 이상의 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 삭제할 수 있습니다. 작업이 성공, 실패 또는 완료되었을 때 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성할 수도 있습니다.  
  
기본적으로 **sysadmin** 고정 서버 역할의 멤버는 [sp_delete_job(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md) 시스템 저장 프로시저를 실행하여 작업을 삭제할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
**sysadmin** 고정 서버 역할의 멤버만 **sp_delete_job** 을 실행하여 모든 작업을 삭제할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자는 해당 사용자가 소유한 작업만 삭제할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|Description|항목|  
|-|-|   
|하나 이상의 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업을 삭제하는 방법에 대해 설명합니다.|[하나 이상의 작업 삭제](../../ssms/agent/delete-one-or-more-jobs.md)|  
|작업이 성공, 실패 또는 완료되었을 때 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 구성하는 방법에 대해 설명합니다.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
