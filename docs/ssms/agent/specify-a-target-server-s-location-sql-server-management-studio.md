---
description: 대상 서버 위치 지정
title: 대상 서버 위치 지정
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 3e09fbc094ddf75a56b2b4c48eac4ecb23b47b7e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482158"
---
# <a name="specify-a-target-server39s-location"></a>대상 서버 위치 지정
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance)에서는 SQL Server 에이전트 기능이 대부분 지원됩니다. 자세한 내용은 [SQL Server와 Azure SQL Managed Instance 간의 T-SQL 차이점](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 다중 서버 관리 구성에서 대상 서버의 위치를 지정하는 방법을 설명합니다.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>시작하기 전 주의 사항  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>제한 사항  
이 동작을 수행하면 레지스트리가 편집됩니다. 레지스트리를 잘못 변경하면 시스템에 심각한 구성 문제를 일으키기 때문에 레지스트리를 수동으로 편집하는 것은 좋지 않습니다. 숙련된 사용자만 레지스트리 편집기 프로그램을 사용하여 레지스트리를 편집해야 합니다. 자세한 내용은 Microsoft Windows 설명서를 참조하세요.  
  
### <a name="security"></a><a name="Security"></a>보안  
  
#### <a name="permissions"></a><a name="Permissions"></a>권한  
**sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>SQL Server Management Studio 사용  
  
#### <a name="to-specify-a-target-servers-location"></a>대상 서버의 위치를 지정하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 대상 서버 위치를 지정하려는 마스터 서버를 확장합니다.  
  
2.  **SQL Server 에이전트** 를 마우스 오른쪽 단추로 클릭하고 **다중 서버 관리** 를 가리킨 다음 **대상 서버 관리** 를 선택합니다.  
  
3.  대상 서버를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
4.  **위치** 상자에 서버의 위치를 입력한 다음 **확인** 을 클릭합니다.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Transact-SQL 사용  
  
#### <a name="to-specify-a-target-servers-location"></a>대상 서버의 위치를 지정하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde_md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
자세한 내용은 [sp_msx_enlist(Transact-SQL)](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)를 참조하세요.  
