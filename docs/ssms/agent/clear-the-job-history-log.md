---
title: 작업 기록 로그 지우기 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], history
- clearing job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 34b9398a-c409-4040-8ea1-0deceb18f961
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dcddf45b8d528954118bff1415ab8aa62db8d502
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="clear-the-job-history-log"></a>Clear the Job History Log
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] [!INCLUDE[tsql](../../includes/tsql_md.md)] or SQL Server Management Objects.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **다음을 사용하여 작업 기록 로그를 지웁니다.**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-clear-the-job-history-log"></a>작업 기록 로그를 지우려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장한 다음 **작업**을 확장합니다.  
  
3.  작업을 마우스 오른쪽 단추로 클릭한 다음 **기록 보기**를 클릭합니다.  
  
4.  **로그 파일 뷰어**에서 기록을 삭제할 작업을 선택한 후 다음 중 하나를 수행합니다.  
  
    -   **삭제**를 클릭한 다음 **기록 삭제** 대화 상자에서 **모든 기록 삭제** 를 클릭합니다. 모든 작업 기록 또는 지정된 날짜 이전의 기록만 삭제할 수 있습니다. 모든 작업 기록을 제거하려면 **모든 기록 삭제**를 클릭합니다. 이전 작업 기록 로그만 제거하려면 **다음 날짜 이전의 기록 삭제**를 클릭한 다음 날짜를 지정합니다.  
  
    -   다중 서버 작업의 기록 로그를 지우려면 **작업 상태** 를 클릭합니다. **작업**, 작업 이름, **원격 작업 기록 보기**를 차례로 클릭합니다.  
  
5.  **삭제**를 클릭합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-clear-the-job-history-log"></a>작업 기록 로그를 지우려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- example removes the history for a job named NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_purge_jobhistory  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업 기록 로그를 지우려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobServer** 클래스의 **PurgeJobHistory** 메서드를 사용합니다. 자세한 내용은 [SMO(SQL Server 관리 개체)](http://msdn.microsoft.com/library/ms162169.aspx)를 참조하세요.  
  
