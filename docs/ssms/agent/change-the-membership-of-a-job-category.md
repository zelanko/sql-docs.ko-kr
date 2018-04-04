---
title: 작업 범주의 멤버 자격 변경 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06189f368c3d84bf701f72b376c9f1c878461ad8
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[tsql](../../includes/tsql_md.md)]에서 작업 범주의 멤버 자격을 변경하는 방법에 대해 설명합니다.  
  
작업 범주를 사용하면 작업을 쉽게 필터링하고 그룹화할 수 있게 구성할 수 있습니다. 사용자 고유의 작업 범주를 만들 수 있습니다. 또한 작업 범주에서 Microsoft SQL Server 에이전트 작업 멤버 자격을 변경할 수도 있습니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **작업 범주의 멤버 자격을 변경하려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>작업 범주의 멤버를 변경하려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 작업 범주를 편집하려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업** 폴더를 마우스 오른쪽 단추로 클릭하고 **작업 범주 관리**를 선택합니다.  
  
4.  **작업 범주 관리***server_name* 대화 상자에서 편집하려는 작업 범주를 선택한 다음, **작업 보기**를 클릭합니다.  
  
5.  **모든 작업 표시** 확인란을 선택합니다.  
  
6.  범주에 작업을 추가하려면 주 표 형태의 **선택** 열에서 해당 작업에 대한 확인란을 선택합니다. 범주에서 작업을 제거하려면 해당 확인란의 선택을 취소합니다. 완료되었으면 **확인**을 클릭합니다.  
  
7.  **작업 범주 관리***server_name* 대화 상자를 닫습니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>작업 범주의 멤버를 변경하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
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
  
자세한 내용은 [sp_update_job(Transact-SQL)](http://msdn.microsoft.com/en-us/cbdfea38-9e42-47f3-8fc8-5978b82e2623)을 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업 범주의 멤버를 변경하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobCategory** 클래스를 사용합니다.  
  
