---
title: query governor cost limit 서버 구성 옵션 구성 | Microsoft Docs
description: 쿼리 관리자 비용 제한 옵션에 대해 알아봅니다. 이 옵션을 사용하여 쿼리 실행을 제한하는 방법을 확인해보세요.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], time to execute
- query governor cost limit option [SQL Server]
- time [SQL Server], query run time
ms.assetid: e7b8f084-1052-4133-959b-cebf4add790f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02b34ab8d3c0a3efd79d7d136bf26401ba92fdf4
ms.sourcegitcommit: bf8cf755896a8c964774a438f2bd461a2a648c22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2020
ms.locfileid: "88216733"
---
# <a name="configure-the-query-governor-cost-limit-server-configuration-option"></a>query governor cost limit 서버 구성 옵션 구성
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 쿼리 관리자 비용 제한 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. 비용 제한 옵션은 지정된 쿼리를 실행하는 데 허용되는 예상 비용의 상한을 지정합니다. 쿼리 비용은 CPU 시간, 메모리, 디스크 IO 등 예상 실행 요구 사항을 기반으로 쿼리 최적화 프로그램에서 결정되는 추상 수치입니다. 특정 하드웨어 구성에서 쿼리를 완료하는 데 필요한 예상 경과 시간(초)입니다. 이러한 개략적 수치는 실행 중인 인스턴스에서 쿼리를 완료하는 데 필요한 시간과는 다릅니다. 상대적 측정값으로 취급되어야 합니다. 이 옵션의 기본값은 0이며, 이 값은 쿼리 관리자 설정을 해제합니다. 값을 0으로 설정하면 모든 쿼리를 시간 제한 없이 실행할 수 있습니다. 0이나 음수가 아닌 값을 지정하면 쿼리 관리자가 그 값을 초과하는 예상 비용을 갖는 쿼리의 실행을 허용하지 않습니다.   
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **쿼리 관리자 비용 제한 옵션을 구성하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [쿼리 관리자 비용 제한 옵션을 구성한 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전문가만이 변경해야 합니다.  
  
-   각 연결에 대한 쿼리 관리자 비용 제한 값을 변경하려면 [SET QUERY_GOVERNOR_COST_LIMIT](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md) 문을 사용하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-query-governor-cost-limit-option"></a>쿼리 관리자 비용 제한 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **연결** 페이지를 클릭합니다.  
  
3.  **쿼리 관리자를 사용하여 장기 실행 쿼리 방지** 확인란을 선택하거나 선택을 취소합니다.  
  
     이 확인란을 선택하는 경우 아래 입력란에 양수 값을 입력합니다. 쿼리 관리자는 이 값을 사용하여 예상 비용이 해당 값을 초과하는 쿼리는 실행을 허용하지 않습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-query-governor-cost-limit-option"></a>쿼리 관리자 비용 제한 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 사용하여 `query governor cost limit` 옵션의 값을 `120`의 예상 쿼리 비용 상한으로 설정하는 방법을 보여 줍니다.
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'query governor cost limit', 120 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="follow-up-after-you-configure-the-query-governor-cost-limit-option"></a><a name="FollowUp"></a> 후속 작업: 쿼리 관리자 비용 제한 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [SET QUERY_GOVERNOR_COST_LIMIT&#40;Transact-SQL&#41;](../../t-sql/statements/set-query-governor-cost-limit-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
