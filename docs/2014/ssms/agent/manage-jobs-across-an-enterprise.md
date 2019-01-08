---
title: 기업 내 작업 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver job management [SQL Server]
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
- target servers [SQL Server], job changes
ms.assetid: 4fe7f6c6-f89b-4430-979c-4994a5dcf7a6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3f051b3de9ba88354f5fded8cd1f429e3b277747
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52812435"
---
# <a name="manage-jobs-across-an-enterprise"></a>기업 내 작업 관리
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 외부에서 다중 서버 작업 정의를 변경하면 변경 사항을 다운로드 목록에 게시해야 대상 서버에서 업데이트된 작업을 다시 다운로드할 수 있습니다. 대상 서버가 최근의 작업 정의를 갖도록 하려면 다중 서버 작업을 업데이트한 후 다음과 같이 INSERT 명령을 게시하십시오.  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 다중 서버 작업이 수정되었음을 대상 서버에 알리려면 다음 프로시저 중 하나를 사용한 후 앞의 명령을 호출해야 합니다.  
  
-   [sp_add_jobstep(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)  
  
-   [sp_update_jobstep(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql)  
  
-   [sp_delete_jobstep(Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql)  
  
-   [sp_attach_schedule&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql)  
  
-   [sp_detach_schedule &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-detach-schedule-transact-sql)  
  
    > [!NOTE]  
    >  저장 프로시저에서는 요청된 변경 내용을 다운로드 목록에 자동 게시하기 때문에 **sp_update_job** 이나 **sp_delete_job** 을 호출한 다음에 **sp_post_msx_operation**을 호출하지 않아도 됩니다.  
  
 다음은 기업 전체에 걸쳐 업무 관리에 사용하는 공통 태스크입니다.  
  
 **대상 서버의 상태를 점검하려면**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql)  
  
-   [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **작업의 대상 서버를 변경하려면**  
  
-   다른 도구는 [SQL Server Management Studio](modify-the-target-servers-for-a-job.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql)  
  
-   [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **대상 서버의 위치를 변경하려면**  
  
-   다른 도구는 [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
-   [SMO(SQL Server 관리 개체)](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
 **대상 서버 클럭을 동기화하려면**  
  
-   다른 도구는 [SQL Server Management Studio](synchronize-target-server-clocks-sql-server-management-studio.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-resync-targetserver-transact-sql)  
  
 **대상 서버가 마스터 서버를 폴링하도록 설정하려면**  
  
-   다른 도구는 [SQL Server Management Studio](force-a-target-server-to-poll-the-master-server.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql)  
  
## <a name="see-also"></a>관련 항목  
 [이벤트 관리](manage-events.md)  
  
  
