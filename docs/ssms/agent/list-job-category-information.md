---
title: "작업 범주 정보 나열 | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6707983f3fe707a5253ff6722adb190579bd1d48
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="list-job-category-information"></a>작업 범주 정보 나열
이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 또는 SQL Server 관리 개체를 사용하여 [!INCLUDE[tsql](../../includes/tsql_md.md)] 에서 작업 범주 정보를 나열하는 방법에 대해 설명합니다.  
  
-   **시작하기 전에:**  
  
    [보안](#Security)  
  
-   **다음을 사용하여 작업 범주 정보를 나열하려면**  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 관리 개체](#SMO)  
  
## <a name="BeforeYouBegin"></a>시작하기 전에  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-list-job-category-information"></a>작업 범주 정보를 나열하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
자세한 내용은 [sp_help_category(Transact-SQL)](http://msdn.microsoft.com/en-us/8cad1dcc-b43e-43bd-bea0-cb0055c84169)를 참조하세요.  
  
## <a name="SMO"></a>SQL Server 관리 개체 사용  
**작업 범주 정보를 나열하려면**  
  
Visual Basic, Visual C#, PowerShell 등 선택한 프로그래밍 언어를 사용하여 **JobCategory** 클래스를 사용합니다.  
  

