---
title: remote query timeout 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time limit for remote queries [SQL Server]
- remote query timeout option
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 715479a8995426645e4faba7b3da1bad8ae1710b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231923"
---
# <a name="configure-the-remote-query-timeout-server-configuration-option"></a>remote query timeout 서버 구성 옵션 구성
  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 원격 쿼리 제한 시간 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **원격 쿼리 제한 시간** 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제한 시간이 초과될 때까지 원격 작업을 수행할 수 있는 시간(초)을 지정합니다. 이 옵션의 기본값은 600이며, 10분 동안 대기할 수 있습니다. 이 값은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 시작된 나가는 연결에 원격 쿼리로 적용됩니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 수신된 쿼리에는 이 값이 적용되지 않습니다. 제한 시간을 사용하지 않으려면 값을 0으로 설정합니다. 쿼리는 완료될 때까지 대기합니다.  
  
 유형이 다른 쿼리의 경우 **원격 쿼리 제한 시간** 은 DBPROP_COMMANDTIMEOUT 행 집합 속성을 사용하여 명령 개체에서 초기화한 쿼리 시간이 초과되기 전에 원격 공급자가 결과 집합을 기다리는 시간(초)을 지정합니다. 이 값은 또한 원격 공급자에서 지원하는 경우 DBPROP_GENERALTIMEOUT을 설정하는 데 사용됩니다. 이로 인해 지정한 시간이 지난 다음 다른 작업의 시간이 초과됩니다.  
  
 원격 저장 프로시저의 경우 **원격 쿼리 제한 시간** 은 원격 `EXEC` 문을 전달한 다음 원격 저장 프로시저 시간이 초과되기 전까지의 시간(초)을 지정합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **원격 쿼리 제한 시간 옵션을 구성하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [원격 쿼리 제한 시간 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   이 값을 설정하려면 먼저 원격 서버 연결이 가능해야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-remote-query-timeout-option"></a>원격 쿼리 제한 시간 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **연결** 노드를 클릭합니다.  
  
3.  **원격 서버 연결**의 **원격 쿼리 제한 시간** 상자에 0부터 2,147,483,647 사이의 값을 입력하거나 선택하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제한 시간이 초과되기 전까지 대기할 최대 시간(초)을 설정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-remote-query-timeout-option"></a>원격 쿼리 제한 시간 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 통해 `remote query timeout` 옵션 값을 `0` 으로 설정하여 제한 시간을 사용하지 않도록 설정하는 방법을 보여 줍니다.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 원격 쿼리 제한 시간 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [행 집합 속성 및 동작](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
