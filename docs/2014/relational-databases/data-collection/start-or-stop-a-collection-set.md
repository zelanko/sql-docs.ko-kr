---
title: 컬렉션 집합 시작 또는 중지 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- collection sets [SQL Server], stopping
- collection sets [SQL Server], starting
ms.assetid: 48a7b2fe-6bc3-4278-a7ec-1babc1290345
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e37d4b2edcd7a6e048c405b072bcbf9b1fef78c6
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970433"
---
# <a name="start-or-stop-a-collection-set"></a>컬렉션 집합 시작 또는 중지
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 컬렉션 집합을 시작 또는 중지하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 컬렉션 집합을 시작하거나 중지합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   데이터 수집기 저장 프로시저와 카탈로그 뷰는 **msdb** 데이터베이스에 저장됩니다.  
  
-   일반적인 저장 프로시저와 달리 데이터 수집기 저장 프로시저에 대한 매개 변수는 형식이 엄격하게 지정되어 있으며 데이터 형식 자동 변환을 지원하지 않습니다. 이러한 매개 변수를 인수 설명에 지정된 올바른 입력 매개 변수 데이터 형식으로 호출하지 않으면 저장 프로시저가 오류를 반환합니다.  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
  
-   SQL Server 에이전트가 시작되어야 합니다.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   컬렉션 집합에 대한 정보를 얻으려면 [syscollector_collection_sets](/sql/relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql) 카탈로그 뷰를 쿼리합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 **dc_operator** 고정 데이터베이스 역할의 멤버 자격이 필요합니다. 컬렉션 집합에 프록시 계정이 없는 경우에는 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다. 예  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-start-a-collection-set"></a>컬렉션 집합을 시작하려면  
  
1.  개체 탐색기에서 **관리** 노드, **데이터 컬렉션**, **시스템 데이터 컬렉션 집합**을 차례로 확장합니다.  
  
2.  시작할 컬렉션 집합을 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 집합 시작**을 클릭합니다.  
  
     메시지 상자에 이 동작의 결과가 표시되며, 컬렉션 집합의 아이콘에 초록색 화살표가 표시되어 컬렉션 집합이 시작되었음을 나타냅니다.  
  
#### <a name="to-stop-a-collection-set"></a>컬렉션 집합을 중지하려면  
  
1.  개체 탐색기에서 **관리** 노드, **데이터 컬렉션**, **시스템 데이터 컬렉션 집합**을 차례로 확장합니다.  
  
2.  중지할 컬렉션 집합을 마우스 오른쪽 단추로 클릭한 다음 **데이터 컬렉션 집합 중지**를 클릭합니다.  
  
     메시지 상자에 이 동작의 결과가 표시되며, 컬렉션 집합의 아이콘에 빨간색 원이 표시되어 컬렉션 집합이 중지되었음을 나타냅니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-start-a-collection-set"></a>컬렉션 집합을 시작하려면  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_syscollector_start_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql) 를 사용하여 ID가 `1`인 컬렉션 집합을 시작합니다.  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
#### <a name="to-stop-a-collection-set"></a>컬렉션 집합을 중지하려면  
  
1.  [!INCLUDE[ssDE](../../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예제에서는 [sp_syscollector_start_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql) 를 사용하여 ID가 `1`인 컬렉션 집합을 중지합니다.  
  
```sql  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 수집기 뷰&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/data-collector-views-transact-sql)   
 [데이터 컬렉션](data-collection.md)  
  
  
