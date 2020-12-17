---
description: Disable or Reactivate an Alert
title: Disable or Reactivate an Alert
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], reactivating
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- alerts [SQL Server], disabling
- reactivating alerts
- removing alerts
ms.assetid: 4cb37dc6-1134-405d-8590-58b44dcf63b2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 7008a6bb91e1d3976f76bcd3e22e3881de424fd7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97423846"
---
# <a name="disable-or-reactivate-an-alert"></a>Disable or Reactivate an Alert
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 문서에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 경고를 비활성화하거나 다시 활성화하는 방법에 대해 설명합니다.  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
기본적으로 **sysadmin** 고정 서버 역할의 멤버가 경고의 정보를 편집할 수 있습니다. 다른 사용자는 **msdb** 데이터베이스의 **SQLAgentOperatorRole** 고정 데이터베이스 역할을 부여 받아야 합니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-disable-or-reactivate-an-alert"></a>경고를 비활성화하거나 다시 활성화하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 비활성화하거나 다시 활성화하려는 경고가 포함된 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **SQL Server 에이전트** 를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **경고** 폴더를 확장합니다.  
  
4.  활성화하려는 경고를 마우스 오른쪽 단추로 클릭하고 **사용** 을 선택합니다. 경고를 비활성화하려면 비활성화하려는 경고를 마우스 오른쪽 단추로 클릭하고 **사용 안 함** 을 선택합니다.  
  
5.  프로세스의 상태를 나타내는 **경고 비활성화** 또는 **경고 활성화** 대화 상자가 표시됩니다. 완료되면 **닫기** 를 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-disable-or-reactivate-an-alert"></a>경고를 비활성화하거나 다시 활성화하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    -- changes the enabled setting of Test Alert to 0  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_alert  
        @name = N'Test Alert',  
        @enabled = 0 ;  
    GO  
    ```  
  
자세한 내용은 [sp_update_alert(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)를 참조하세요.  
