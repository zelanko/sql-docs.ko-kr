---
description: 기업 내 작업 관리
title: 기업 내 작업 관리
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 62e4eb1574d48ecd40af46ba081f6443bdafb000
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482226"
---
# <a name="manage-jobs-across-an-enterprise"></a>기업 내 작업 관리
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 외부에서 다중 서버 작업 정의를 변경하면 변경 사항을 다운로드 목록에 게시해야 대상 서버에서 업데이트된 작업을 다시 다운로드할 수 있습니다. 대상 서버가 최근의 작업 정의를 갖도록 하려면 다중 서버 작업을 업데이트한 후 다음과 같이 INSERT 명령을 게시하십시오.  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
다중 서버 작업이 수정되었음을 대상 서버에 알리려면 다음 프로시저 중 하나를 사용한 후 앞의 명령을 호출해야 합니다.  
  
-   [sp_add_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
-   [sp_update_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md)  
  
-   [sp_delete_jobstep(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql.md)  
  
-   [이벤트 관리](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
-   [sp_detach_schedule(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql.md)  
  
    > [!NOTE]  
    > 저장 프로시저에서는 요청된 변경 내용을 다운로드 목록에 자동 게시하기 때문에 **sp_update_job** 이나 **sp_delete_job** 을 호출한 다음에 **sp_post_msx_operation** 을 호출하지 않아도 됩니다.  
  
다음은 기업 전체에 걸쳐 업무 관리에 사용하는 공통 태스크입니다.  
  
**대상 서버의 상태를 점검하려면**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)  
  
-   [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**작업의 대상 서버를 변경하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql.md)  
  
-   [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**대상 서버의 위치를 변경하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/specify-a-target-server-s-location-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)  
  
-   [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
**대상 서버 클럭을 동기화하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql.md)  
  
**대상 서버가 마스터 서버를 폴링하도록 설정하려면**  
  
-   [SQL Server Management Studio](../../ssms/agent/force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
[이벤트 관리](../../ssms/agent/manage-events.md)  
