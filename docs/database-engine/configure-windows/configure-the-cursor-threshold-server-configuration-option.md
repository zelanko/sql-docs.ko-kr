---
title: cursor threshold 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 243798abec1a00d3c5ea3a9426449c3bd42e462b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012747"
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>cursor threshold 서버 구성 옵션 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 커서 임계값 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **커서 임계값** 옵션은 커서 키 집합이 비동기적으로 생성되는 커서 집합의 행 수를 지정합니다. 커서에서 결과 집합에 대해 키 집합을 생성할 때 쿼리 최적화 프로그램은 해당 결과 집합으로 반환될 행 개수를 계산합니다. 쿼리 최적화 프로그램의 계산 결과, 반환된 행 개수가 이 임계값보다 크면 커서가 계속 채워지는 동안 사용자가 커서에서 행을 인출할 수 있도록 커서가 비동기적으로 생성됩니다. 그렇지 않으면 커서가 동기적으로 생성되어 모든 행이 반환될 때까지 쿼리가 기다립니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **커서 임계값 옵션을 설정하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [커서 임계값 옵션을 구성한 후](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 키 집합 커서 또는 정적 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서를 비동기식으로 생성할 수 없습니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서 작업은 일괄 처리되므로 [!INCLUDE[tsql](../../includes/tsql-md.md)] 커서를 비동기식으로 생성하지 않아도 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 각 커서 작업의 클라이언트 왕복 때문에 짧은 대기 시간 OPEN이 문제가 되는 비동기 키 집합 기반 또는 정적 API(애플리케이션 프로그래밍 인터페이스) 서버 커서를 계속 지원합니다.  
  
-   키 집합의 예상 행 개수를 결정하는 최적화 프로그램의 정확도는 커서에 있는 각 테이블 통계의 통용성에 따라 다릅니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전문가만이 변경해야 합니다.  
  
-   **커서 임계값** 을 -1로 설정하면 모든 키 집합이 동기적으로 생성되므로 작은 커서 집합에 유리합니다. **cursor threshold** 를 0으로 설정하면 모든 커서 키 집합이 비동기적으로 생성됩니다. 다른 값을 사용하면 쿼리 최적화 프로그램이 커서 집합에 있는 예상 행 개수를 비교하여 이 값이 **cursor threshold**에 설정된 수를 초과하면 비동기적으로 키 집합을 작성합니다. 결과 집합이 작을수록 동기적 작성 성능이 향상되므로 **커서 임계값** 를 너무 낮게 설정하지 않는 것이 좋습니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>커서 임계값 옵션을 설정하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **고급** 노드를 클릭합니다.  
  
3.  **기타**에서 **커서 임계값** 옵션을 원하는 값으로 변경합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>커서 임계값 옵션을 설정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예제에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 통해 `cursor threshold` 옵션을 `0` 으로 설정하여 커서 키 집합이 비동기적으로 생성되도록 만드는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="follow-up-after-you-configure-the-cursor-threshold-option"></a><a name="FollowUp"></a> 후속 작업: 커서 임계값 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [@@CURSOR_ROWS&#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)  
  
  
