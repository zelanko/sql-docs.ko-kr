---
title: "작업 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: delete jobs
ms.assetid: bffb915e-bc84-4417-aa35-183243ca3312
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be3069cfd5be3845c6c3f2f08b9a17bb7243ee4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="delete-jobs"></a>작업 삭제
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 작업이란 SQL Server 에이전트가 순차적으로 수행하는 일련의 지정된 작업입니다. 기본적으로 실행이 완료되어도 작업은 삭제되지 않습니다. 작업의 성공 또는 실패에 관계없이 하나 이상의 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업을 삭제할 수 있습니다. 작업이 성공, 실패 또는 완료되었을 때 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 구성할 수도 있습니다.  
  
기본적으로 **sysadmin** 고정 서버 역할의 멤버는 [sp_delete_job(Transact-SQL)](http://msdn.microsoft.com/en-us/b85db6e4-623c-41f1-9643-07e5ea38db09) 시스템 저장 프로시저를 실행하여 작업을 삭제할 수 있습니다. 다른 사용자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] msdb **데이터베이스의 다음** 에이전트 고정 데이터베이스 역할 중 하나를 부여 받아야 합니다.  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
이러한 역할의 사용 권한에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](../../ssms/agent/sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
**sysadmin** 고정 서버 역할의 멤버만 **sp_delete_job** 을 실행하여 모든 작업을 삭제할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자는 해당 사용자가 소유한 작업만 삭제할 수 있습니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|||  
|-|-|  
|**설명**|**항목**|  
|하나 이상의 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업을 삭제하는 방법에 대해 설명합니다.|[하나 이상의 작업 삭제](../../ssms/agent/delete-one-or-more-jobs.md)|  
|작업이 성공, 실패 또는 완료되었을 때 자동으로 삭제하도록 [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트를 구성하는 방법에 대해 설명합니다.|[Automatically Delete a Job](../../ssms/agent/automatically-delete-a-job.md)|  
  
