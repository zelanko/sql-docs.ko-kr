---
title: index create memory 서버 구성 옵션 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- index create memory option
ms.assetid: 3d722d9b-bada-4bf5-a9d7-bfc556bb4915
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 280d4edef062429304d5c6e1d6c65ea63fac2eee
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534085"
---
# <a name="configure-the-index-create-memory-server-configuration-option"></a>index create memory 서버 구성 옵션 구성
  이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 인덱스 생성 메모리 [!INCLUDE[tsql](../../includes/tsql-md.md)]서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **인덱스 생성 메모리** 옵션은 인덱스를 만들기 위해 처음으로 할당되는 최대 메모리 양을 제어합니다. 이 옵션의 기본값은 0(자체 구성)입니다. 나중에 인덱스 생성에 메모리가 더 필요하고 해당 메모리를 사용할 수 있는 경우 서버가 이 옵션의 설정 값을 초과하여 메모리를 사용하게 됩니다. 추가 메모리를 사용할 수 없는 경우 이미 할당된 메모리를 계속 사용하여 인덱스가 생성됩니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **인덱스 생성 메모리 옵션을 구성하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [인덱스 생성 메모리 옵션을 구성한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   **쿼리당 최소 메모리** 옵션의 설정이 **인덱스 생성 메모리** 옵션보다 우선합니다. 두 옵션을 변경할 때 **인덱스 생성 메모리** 가 **쿼리당 최소 메모리**보다 적은 경우 경고 메시지가 나타나지만 값은 설정됩니다. 쿼리를 실행하는 동안 유사한 경고가 발생합니다.  
  
-   분할된 테이블 및 인덱스를 사용할 때 분할된 인덱스가 정렬되지 않았고 병렬 처리 수준이 높은 경우 인덱스를 만드는 데 필요한 최소 메모리 요구 사항이 상당히 증가될 수 있습니다. 이 옵션에 따라 단일 인덱스 생성 작업에서 모든 인덱스 파티션에 할당된 초기 총 메모리 양이 결정됩니다. 이 옵션으로 설정된 양이 쿼리 실행에 필요한 최소 양보다 적은 경우 오류 메시지가 나타나면서 쿼리가 종료됩니다.  
  
-   이 옵션의 실행 값은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실행 중인 운영 체제와 하드웨어 플랫폼에 사용할 수 있는 실제 메모리 양을 초과하지 않습니다. 32비트 운영 체제에서 실행 값은 3GB 미만입니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
-   **index create memory** 옵션은 자체 구성되므로 대부분 조정이 필요하지 않습니다. 그러나 인덱스를 만드는 데 문제가 있으면 이 옵션의 값을 변경합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 RECONFIGURE 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 ALTER SETTINGS 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 ALTER SETTINGS 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-configure-the-index-create-memory-option"></a>index create memory 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **메모리** 노드를 클릭합니다.  
  
3.  **Index creation memory**에서 원하는 index create memory 옵션 값을 입력하거나 선택합니다.  
  
     **index create memory** 옵션을 사용하여 인덱스 생성 정렬에 사용하는 메모리 양을 제어할 수 있습니다. **index create memory** 옵션은 자체 구성이므로 대부분 조정이 필요하지 않습니다. 그러나 인덱스를 만드는 데 문제가 있으면 이 옵션의 값을 변경합니다. 쿼리 정렬은 **쿼리당 최소 메모리** 옵션을 통해 제어됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-index-create-memory-option"></a>index create memory 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 다음 예에서는 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 를 사용하여 `index create memory` 옵션의 값을 `4096`(으)로 설정하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
EXEC sp_configure 'index create memory', 4096  
GO  
RECONFIGURE;  
GO  
```  
  
 자세한 내용은 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)서버 구성 옵션을 보거나 구성하는 방법에 대해 설명합니다.  
  
##  <a name="FollowUp"></a> 후속 작업: 인덱스 생성 메모리 옵션을 구성한 후  
 이 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.configurations&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-configurations-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 메모리 서버 구성 옵션](server-memory-server-configuration-options.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
