---
title: 작업 활동 보기 | Microsoft 문서
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
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eed58dde1580a4e05fa6f2c2103661747563c114
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981065"
---
# <a name="view-job-activity"></a>작업 활동 보기
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database 관리되는 인스턴스](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database 관리되는 인스턴스 T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] 에서 [!INCLUDE[tsql](../../includes/tsql_md.md)]에이전트 작업의 런타임 상태를 보는 방법에 대해 설명합니다.  
  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 시작할 때 새 세션이 만들어지고 **sysjobactivity** 데이터베이스의 **sysjobactivity** 테이블에 기존에 정의된 작업이 표시됩니다. 이 테이블은 현재 작업 활동과 상태를 기록합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트의 작업 활동 모니터를 사용하여 작업의 현재 상태를 볼 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 에이전트 서비스가 예기치 않게 종료되는 경우 **sysjobactivity** 테이블을 참조하여 서비스 종료 시 어떤 작업이 실행 중이었는지 확인할 수 있습니다.  
  
**항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
    [보안](#Security)  
  
-   **작업 활동을 보려면:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
  
### <a name="Security"></a>보안  
자세한 내용은 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)을 참조하세요.  
  
## <a name="SSMS"></a>SQL Server Management Studio 사용  
  
#### <a name="to-view-job-activity"></a>작업 활동을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
  
2.  **SQL Server 에이전트**를 확장합니다.  
  
3.  **작업 활동 모니터** 를 마우스 오른쪽 단추로 클릭한 다음 **작업 활동 보기**를 클릭합니다.  
  
4.  **작업 활동 모니터**에서 이 서버에 정의되어 있는 각 작업에 대한 정보를 볼 수 있습니다.  
  
5.  작업을 시작하거나 중지하거나, 활성화하거나 비활성화하거나, 작업 활동 모니터에 표시된 작업 상태를 새로 고치거나, 작업을 삭제하거나 작업의 기록 또는 속성을 보려면 작업을 마우스 오른쪽 단추로 클릭합니다.  여러 작업을 시작하거나 중지하거나, 활성화하거나 비활성화하거나 새로 고치려면 작업 활동 모니터에서 여러 행을 선택한 다음 선택 사항을 마우스 오른쪽 단추로 클릭합니다.  
  
6.  작업 활동 모니터를 업데이트하려면 **새로 고침**을 클릭합니다. 더 적은 수의 행을 보려면 **필터** 를 클릭하고 필터 매개 변수를 입력합니다.  
  
## <a name="TSQL"></a>Transact-SQL 사용  
  
#### <a name="to-view-job-activity"></a>작업 활동을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
자세한 내용은 [sp_help_jobactivity(Transact-SQL)](http://msdn.microsoft.com/d344864f-b4d3-46b1-8933-b81dec71f511)를 참조하세요.  
  
