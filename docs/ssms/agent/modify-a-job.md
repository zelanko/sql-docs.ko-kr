---
description: Modify a Job
title: Modify a Job
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
author: markingmyname
ms.author: maghan
ms.reviewer: mikeray
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 785d22adc5bb1047618a14f8931e728753c2a957
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482216"
---
# <a name="modify-a-job"></a>Modify a Job

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] 에이전트 작업의 속성을 변경하는 방법에 대해 설명합니다.  

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
**sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [SQL Server 에이전트 보안 구현](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-job"></a>작업을 수정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업** 을 차례로 확장한 다음 수정할 작업을 마우스 오른쪽 단추로 클릭하고 **속성** 을 클릭합니다.  
  
3.  **작업 속성** 대화 상자에서 해당 페이지를 사용하여 작업의 속성, 단계, 일정, 경고 및 알림을 업데이트합니다.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-modify-a-job"></a>작업을 수정하려면  
  
1.  개체 탐색기에서 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  쿼리 창에서 다음 시스템 저장 프로시저를 사용하여 작업을 수정합니다.  
  
    -   작업의 특성을 변경하려면 [sp_update_job(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-job-transact-sql.md) 을 실행합니다.  
  
    -   작업 정의에 대한 일정 정보를 변경하려면 [sp_update_schedule(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md) 을 실행합니다.  
  
    -   새 작업 단계를 추가하려면 [sp_add_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md) 을 실행합니다.  
  
    -   기존의 작업 단계를 변경하려면 [sp_update_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md) 을 실행합니다.  
  
    -   작업에서 작업 단계를 제거하려면 [sp_delete_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md) 을 실행합니다.  
  
    -   SQL Server 에이전트 마스터 작업을 수정하는 추가 저장 프로시저:  
  
        -   현재 작업과 연결되어 있는 서버를 삭제하려면 [sp_delete_jobserver(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql.md) 를 실행합니다.  
  
        -   현재 작업과 서버를 연결하려면 [sp_add_jobserver(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md) 를 실행합니다.  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>SQL Server 관리 개체 사용  
**작업을 수정하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **Job** 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)를 참조하세요.  
