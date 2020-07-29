---
title: Delete an Alert
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], deleting
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- removing alerts
ms.assetid: c982b208-e2d1-4d34-8cee-940b9baf6586
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ec1bd2f87702f0ab2352d0a3e9e6b8ae66b6fbd9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775071"
---
# <a name="delete-an-alert"></a>Delete an Alert
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[msCoName](../../includes/msconame_md.md)] 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] 에이전트 경고를 삭제하는 방법에 대해 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
경고를 제거하면 해당 경고와 연관된 모든 알림도 함께 제거됩니다.  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
기본적으로 **sysadmin** 고정 서버 역할의 멤버만 경고를 삭제할 수 있습니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-delete-an-alert"></a>경고를 삭제하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 삭제하려는 SQL Server 에이전트 경고가 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트**를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **경고** 폴더를 확장합니다.  
  
4.  삭제할 경고를 마우스 오른쪽 단추로 클릭하고 **삭제**를 선택합니다.  
  
5.  **개체 삭제** 대화 상자에서 올바른 경고를 선택했는지 확인한 다음 **확인**을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-delete-an-alert"></a>경고를 삭제하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    -- deletes the SQL Server Agent alert called 'Test Alert.'  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_alert  
       @name = N'Test Alert' ;  
    GO  
    ```  
  
자세한 내용은 [sp_delete_alert(Transact-SQL)](https://msdn.microsoft.com/a831315e-793d-41c4-8333-b324bb2bc614)를 참조하세요.  
  
