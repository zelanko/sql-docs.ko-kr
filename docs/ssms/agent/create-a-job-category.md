---
title: 작업 범주 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7a487f7e081d9660f2034d8f6a2e62752bd7bd51
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099597"
---
# <a name="create-a-job-category"></a>작업 범주 만들기
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 관리 개체를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 작업 범주를 만드는 방법에 대해 설명합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에는 기본으로 제공되는 작업 범주가 있으며 이를 사용하여 작업을 할당하거나 작업 범주를 만들어 작업을 할당할 수 있습니다. 작업 범주를 사용하면 작업을 쉽게 필터링하고 그룹화할 수 있게 구성할 수 있습니다. 예를 들어 데이터베이스 유지 관리 범주에 있는 모든 데이터베이스 백업 작업을 구성할 수 있습니다. 사용자 고유의 작업 범주를 만들 수도 있습니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [제한 사항](#Restrictions)  
  
    [보안](#Security)  
  
-   **작업 범주를 만들려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Restrictions"></a>제한 사항  
다중 서버 범주는 마스터 서버에만 존재합니다. 한 마스터 서버에서는 하나의 기본 작업 범주만 사용할 수 있습니다. 즉, [**범주화되지 않음(다중 서버)**] 하나만 있습니다. 다중 서버 작업을 다운로드하면 해당 범주가 대상 서버에서 **MSX의 작업** 으로 변경됩니다.  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-create-a-job-category"></a>작업 범주를 만들려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 작업 범주를 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 폴더를 마우스 오른쪽 단추로 클릭하고 **작업 범주 관리**를 선택합니다.  
  
4.  **작업 범주 관리***server_name* 대화 상자에서 **추가**를 클릭합니다.  
  
5.  새 대화 상자의 **이름** 상자에서 새 작업 범주의 이름을 입력합니다.  
  
6.  **모든 작업 표시** 확인란을 선택합니다. 새 범주에 대한 작업을 해당 확인란을 선택하여 하나 이상 선택합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **작업 범주 관리***server_name* 대화 상자에서 **새로 고침**을 클릭하여 새 작업 범주가 활성 상태인지 확인합니다. 모든 항목이 예상대로 되어 있으면 이 대화 상자를 닫습니다.  
  
이러한 대화 상자에 대한 자세한 내용은 [작업 범주 - 작업 범주 관리](../../ssms/agent/job-categories-manage-job-categories.md) 및 [작업 범주 속성 - 새 작업 범주](../../ssms/agent/job-categories-properties-new-job-category.md)를 참조하세요.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-create-a-job-category"></a>작업 범주를 만들려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
자세한 내용은 [sp_add_category(Transact-SQL)](http://msdn.microsoft.com/6cca32cd-d941-4378-aed6-a7c90cb7520a)를 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업 범주를 만들려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobCategory** 클래스를 호출합니다. 예제 코드를 보려면 [SQL Server 에이전트에서 자동 관리 태스크 예약](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)을 참조하세요.  
  
