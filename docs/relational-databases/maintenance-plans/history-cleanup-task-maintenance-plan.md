---
title: "기록 정리 태스크(유지 관리 계획) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbf4cfd2254dbe3e5f482e603ca7535682102d80
ms.lasthandoff: 04/11/2017

---
# <a name="history-cleanup-task-maintenance-plan"></a>기록 정리 태스크(유지 관리 계획)
  **기록 정리 태스크** 대화 상자를 사용하여 msdb 데이터베이스의 테이블에서 오래된 기록 정보를 삭제할 수 있습니다. 이 태스크는 백업 및 복원 기록, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 기록 및 유지 관리 계획 기록의 삭제를 지원합니다.  
  
 이 문은 **sp_purge_jobhistory** 문과 **sp_delete_backuphistory** 문을 사용합니다.  
  
## <a name="uielement-list"></a>UIElement 목록  
 **연결**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. **새 연결** 대화 상자는 뒷부분에서 설명합니다.  
  
 **백업 및 복원 기록**  
 최근 백업을 만들었을 당시의 기록을 보존하면 데이터베이스를 복원하려고 할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 복구 계획을 만드는 데 도움이 될 수 있습니다. 보존 기간은 적어도 전체 데이터베이스 백업 빈도만큼 되어야 합니다.  
  
 **SQL Server 에이전트 작업 기록**  
 이 기록을 사용하면 실패한 작업의 문제를 해결하거나 데이터베이스 동작의 발생 이유를 확인하는 데 도움이 됩니다.  
  
 **유지 관리 계획 기록**  
 이 기록을 사용하면 실패한 유지 관리 계획 동작의 문제를 해결하거나 데이터베이스 작업의 발생 이유를 확인하는 데 도움이 됩니다.  
  
 **다음보다 오래된 기록 데이터 제거**  
 삭제할 항목의 보존 기간을 지정합니다.  
  
 **T-SQL 보기**  
 선택한 옵션을 기반으로 서버에 대해 수행한 이 태스크의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
> [!NOTE]  
>  영향을 받은 개체 수가 많은 경우에는 표시하는 데 시간이 오래 걸릴 수 있습니다.  
  
## <a name="new-connection-dialog-box"></a>새 연결 대화 상자  
 **연결 이름**  
 새 연결의 이름을 입력합니다.  
  
 **서버 이름 선택 또는 입력**  
 이 태스크를 수행할 때 연결할 서버를 선택합니다.  
  
 **새로 고침**  
 사용할 수 있는 서버 목록을 새로 고칩니다.  
  
 **서버 로그온 정보 입력**  
 서버에 대한 인증 방법을 지정합니다.  
  
 **Windows NT 통합 보안 사용**  
 Microsoft Windows 인증을 사용하여 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
 SQL Server 인증을 사용하여 SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sp_purge_jobhistory&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [sp_delete_backuphistory&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)  
  
  
