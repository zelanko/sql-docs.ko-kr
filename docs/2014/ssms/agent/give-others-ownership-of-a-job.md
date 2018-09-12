---
title: 작업의 소유권을 다른 사용자에게 제공 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], owners
- owners [SQL Server], jobs
- SQL Server Agent jobs, owners
ms.assetid: 2ded5e9c-4251-4fb1-a047-99f13d150b61
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0481fe11ece555ef5a2f38a7eb73f202556aaf42
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808709"
---
# <a name="give-others-ownership-of-a-job"></a>Give Others Ownership of a Job
  이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업의 소유권을 다른 사용자에게 다시 할당하는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Restrictions), [보안](#Security)  
  
-   **작업의 소유권을 다른 사용자에게 제공하려면:**  
  
     [SQL Server Management Studio](#SSMSProc2)  
  
     [Transact-SQL](#TsqlProc2)  
  
     [SQL Server 관리 개체](#SMOProc2)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
 작업을 만들려면 사용자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할이나 **sysadmin** 고정 서버 역할 중 하나의 멤버여야 합니다. 작업은 소유자나 **sysadmin** 역할의 멤버만 편집할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 고정 데이터베이스 역할에 대한 자세한 내용은 [SQL Server 에이전트 고정 데이터베이스 역할](sql-server-agent-fixed-database-roles.md)을 참조하세요.  
  
 작업 소유자를 변경하려면 시스템 관리자여야 합니다.  
  
 다른 로그인에 작업을 할당한다고 해서 새 소유자가 작업을 성공적으로 실행할 수 있는 충분한 권한을 가진다고 보장할 수 없습니다.  
  
###  <a name="Security"></a> 보안  
 보안을 위해 작업 소유자나 **sysadmin** 역할의 멤버만 작업 정의를 변경할 수 있습니다. **sysadmin** 고정 서버 역할의 멤버만 작업 소유권을 다른 사용자에게 할당할 수 있으며 작업 소유자가 아니어도 모든 작업을 실행할 수 있습니다.  
  
> [!NOTE]  
>  **sysadmin** 고정 서버 역할의 멤버가 아닌 사용자로 작업 소유권을 변경하고 이 작업이 프록시 계정을 필요로 하는 작업 단계를 실행 중이면(예: [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지 실행) 사용자가 해당 프록시 계정에 액세스할 수 있어야 작업이 실패하지 않습니다.  
  
####  <a name="Permissions"></a> Permissions  
 자세한 내용은 [Implement SQL Server Agent Security](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="SSMSProc2"></a> SQL Server Management Studio 사용  
 **작업의 소유권을 다른 사람에게 주려면**  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **소유자** 목록에서 로그인을 선택합니다. 작업 소유자를 변경하려면 시스템 관리자여야 합니다.  
  
     다른 로그인에 작업을 할당한다고 해서 새 소유자가 작업을 성공적으로 실행할 수 있는 충분한 권한을 가진다고 보장할 수 없습니다.  
  
##  <a name="TsqlProc2"></a> Transact-SQL 사용  
 **작업의 소유권을 다른 사람에게 주려면**  
  
1.  개체 탐색기에서 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  쿼리 창에서 사용 하는 다음 문을 입력 합니다 [sp_manage_jobs_by_login &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-manage-jobs-by-login-transact-sql) 시스템 저장 프로시저입니다. 다음 예에서는 `danw` 의 모든 작업을 `françoisa`에 다시 할당합니다.  
  
    ```  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_manage_jobs_by_login  
        @action = N'REASSIGN',  
        @current_owner_login_name = N'danw',  
        @new_owner_login_name = N'françoisa' ;  
    GO  
    ```  
  
##  <a name="SMOProc2"></a> SQL Server 관리 개체를 사용 하 여  
 **작업의 소유권을 다른 사람에게 주려면**  
  
1.  호출 된 `Job` Visual Basic, Visual C# 또는 PowerShell 등 선택한 프로그래밍 언어를 사용 하 여 클래스입니다. 예제 코드를 보려면 [SQL Server 에이전트에서 자동 관리 태스크 예약](sql-server-agent.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [작업 구현](implement-jobs.md)   
 [작업 만들기](create-jobs.md)  
  
  
