---
title: 작업 수정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0d25830ad119a1f5f344a4dcf318c35bee5f86ca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062193"
---
# <a name="modify-a-job"></a>Modify a Job
  이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , 또는 SQL Server 관리 개체를 사용 하 여에서 에이전트 작업의 속성을 변경 하는 방법에 대해 설명 합니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:** ,  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **작업을 수정하려면:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server 관리 개체](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 마스터 작업은 로컬 및 원격 서버 모두에서 대상이 될 수 없습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 **sysadmin** 고정 서버 역할의 멤버가 아닌 경우 자신이 소유한 작업만 수정할 수 있습니다. 자세한 내용은 [SQL Server 에이전트 보안 구현](implement-sql-server-agent-security.md)을 참조하세요.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-modify-a-job"></a>작업을 수정하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결한 다음, 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**, **작업**을 차례로 확장한 다음 수정할 작업을 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
3.  **작업 속성** 대화 상자에서 해당 페이지를 사용하여 작업의 속성, 단계, 일정, 경고 및 알림을 업데이트합니다.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-modify-a-job"></a>작업을 수정하려면  
  
1.  개체 탐색기에서 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  쿼리 창에서 다음 시스템 저장 프로시저를 사용하여 작업을 수정합니다.  
  
    -   [Transact-sql&#41;&#40;sp_update_job](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) 을 실행 하 여 작업의 특성을 변경 합니다.  
  
    -   [Transact-sql&#41;&#40;sp_update_schedule](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql) 을 실행 하 여 작업 정의에 대 한 일정 정보를 변경 합니다.  
  
    -   [Transact-sql&#41;&#40;sp_add_jobstep](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) 를 실행 하 여 새 작업 단계를 추가 합니다.  
  
    -   [Transact-sql&#41;&#40;sp_update_jobstep](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) 실행 하 여 기존 작업 단계를 변경 합니다.  
  
    -   [Transact-sql&#41;&#40;sp_delete_jobstep](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql) 을 실행 하 여 작업에서 작업 단계를 제거 합니다.  
  
    -   SQL Server 에이전트 마스터 작업을 수정하는 추가 저장 프로시저:  
  
        -   [Transact-sql&#41;&#40;sp_delete_jobserver](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql) 를 실행 하 여 현재 작업과 연결 된 서버를 삭제 합니다.  
  
        -   [Transact-sql&#41;&#40;sp_add_jobserver](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql) 를 실행 하 여 현재 작업과 서버를 연결 합니다.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>SQL Server 관리 개체 사용  
 **작업을 수정하려면**  
  
 Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 `Job` 클래스를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](https://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
  
