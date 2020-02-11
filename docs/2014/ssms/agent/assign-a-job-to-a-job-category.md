---
title: 작업 범주에 작업 할당 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], assigning
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- SQL Server Agent jobs, assigning
- assigning job to category
ms.assetid: a9ea65a2-1d73-4582-a335-63adeb450cb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab7695b6a80772ddcd01996e783fffd806447c59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62473204"
---
# <a name="assign-a-job-to-a-job-category"></a>작업 범주에 작업 할당
  이 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 항목에서는, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 SQL Server 관리 개체를 사용 하 여에서 작업 범주에 에이전트 작업을 할당 하는 방법에 대해 설명 합니다.  
  
 작업 범주를 사용하면 작업을 쉽게 필터링하고 그룹화할 수 있게 구성할 수 있습니다. 예를 들어 데이터베이스 유지 관리 범주에 있는 모든 데이터베이스 백업 작업을 구성할 수 있습니다. 작업을 기본 제공 작업 범주에 할당하거나 사용자 정의 작업 범주를 만든 다음 여기에 작업을 할당할 수 있습니다.  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [SQL Server 에이전트 보안 구현](implement-sql-server-agent-security.md)을 참조하세요.  
  
  
  
##  <a name="SSMS"></a> SQL Server Management Studio 사용  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>작업 범주에 작업을 할당하려면  
  
1.  
  **개체 탐색기**에서 더하기 기호를 클릭하여 작업을 작업 범주에 할당하려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **작업** 폴더를 확장합니다.  
  
4.  편집할 작업을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 선택합니다.  
  
5.  **작업 속성-**_Job_name_ 대화 상자의 **범주** 목록에서 작업에 할당 하려는 작업 범주를 선택 합니다.  
  
6.  **확인**을 클릭합니다.  
  
  
##  <a name="TSQL"></a> Transact-SQL 사용  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>작업 범주에 작업을 할당하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 자세한 내용은 [sp_update_job &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)를 참조 하세요.  
  
  
  
##  <a name="SMO"></a>SQL Server 관리 개체 사용  
 **작업 범주에 작업을 할당 하려면**  
  
 Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 `JobCategory` 클래스를 사용합니다.  
  
  
  
  
