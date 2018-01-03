---
title: "작업 기록 보기 | Microsoft 문서"
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
helpviewer_keywords:
- jobs [SQL Server Agent], history
- viewing job history
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
- displaying job history
ms.assetid: 3bbd1556-abdb-48a3-b249-546eace76343
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f319bd3a2299d2815df4ace5298dad8878182344
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="view-the-job-history"></a>View the Job History
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], [!INCLUDE[tsql](../../includes/tsql_md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 작업 기록 로그를 보는 방법에 대해 설명합니다.  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **작업 기록 로그를 보려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-view-the-job-history-log"></a>작업 기록 로그를 보려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장한 다음 **작업**을 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭한 다음 **기록 보기**를 클릭합니다.  
  
4.  로그 파일 뷰어에서 작업 기록을 봅니다.  
  
5.  작업 기록을 업데이트하려면 **새로 고침**을 클릭합니다. 행을 적게 표시하려면 **필터** 단추를 클릭하고 필터 매개 변수를 입력합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-view-the-job-history-log"></a>작업 기록 로그를 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- lists all job information for the NightlyBackups job.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobhistory   
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
자세한 내용은 [sp_help_jobhistory(Transact-SQL)](http://msdn.microsoft.com/en-us/a944d44e-411b-4735-8ce4-73888d4262d7)를 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업 기록 로그를 보려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **Job** 클래스의 **EnumHistory** 메서드를 호출합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](http://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
