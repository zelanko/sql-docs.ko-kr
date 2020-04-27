---
title: 쿼리 계획 마이그레이션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66f1f8f57dca3ad2edba3f4b63100b2de3ae5659
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779115"
---
# <a name="migrate-query-plans"></a>쿼리 계획 마이그레이션
  데이터베이스를 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하면 대부분의 경우 쿼리 성능이 향상됩니다. 그러나 성능 향상을 위해 세심하게 튜닝된 중요한 쿼리의 경우 업그레이드하기 전에 각 쿼리에 대한 계획 지침을 만들어 쿼리 계획을 보존할 수 있습니다. 업그레이드 후에 쿼리 최적화 프로그램에서 한 개 이상의 쿼리에 대해 효율성이 낮은 계획이 선택된 경우 계획 지침을 사용하여 쿼리 최적화 프로그램에서 업그레이드 전 계획이 사용되도록 지정할 수 있습니다.  
  
 업그레이드 전에 계획 지침을 만들려면 다음 단계를 수행하십시오.  
  
1.  [Sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) 저장 프로시저를 사용 하 고 use plan 쿼리 힌트에 쿼리 계획을 지정 하 여 각 업무상 중요 한 쿼리에 대 한 현재 계획을 기록 합니다.  
  
2.  계획 지침이 쿼리에 적용되었는지 확인합니다.  
  
3.  데이터베이스를 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드합니다.  
  
     이러한 계획은 업그레이드된 계획 지침 데이터베이스에 보관되며 업그레이드 후 계획을 되돌려야 할 경우에 대체 계획으로 사용됩니다.  
  
     업그레이드 후에는 새로운 릴리스에서 제공되는 향상된 계획이나 업데이트된 통계에 따른 유용한 다시 컴파일을 활용할 수 있도록 계획 지침을 사용하지 않는 것이 좋습니다.  
  
4.  업그레이드 후에 효율성이 떨어지는 계획이 선택되면 계획 지침을 일부 또는 모두 활성화하여 새 계획을 덮어씁니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 계획 지침을 만들어 쿼리에 대한 업그레이드 전 계획을 기록하는 방법을 보여 줍니다.  
  
### <a name="step-1-collect-the-plan"></a>1 단계: 계획 수집  
 계획 지침에 기록되는 쿼리 계획은 XML 형식이어야 합니다. 다음과 같은 방법으로 XML 형식의 쿼리 계획을 생성할 수 있습니다.  
  
-   [SET SHOWPLAN_XML](/sql/t-sql/statements/set-showplan-xml-transact-sql)  
  
-   [SET STATISTICS XML](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
-   [Dm_exec_query_plan](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql) 동적 관리 함수의 query_plan 열을 쿼리 하는 중입니다.  
  
-   실행 계획 [xml](../../relational-databases/event-classes/showplan-xml-event-class.md), 실행 [계획 xml 통계 프로필](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)및 실행 [계획 xml For Query Compile](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md) 이벤트 클래스 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]  
  
 다음 예에서는 동적 관리 뷰를 쿼리하여 `SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;` 문에 대한 쿼리 계획을 수집합니다.  
  
```  
USE AdventureWorks;  
GO  
SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%';  
GO  
```  
  
### <a name="step-2-create-the-plan-guide-to-force-the-plan"></a>2 단계: 계획을 적용 하는 계획 지침 만들기  
 앞에서 설명한 방법 중 하나로 만든 XML 형식의 쿼리 계획을 계획 지침에 사용하려면 sp_create_plan_guide의 OPTION 절에 지정된 USE PLAN 쿼리 힌트 안에 쿼리 계획을 문자열 리터럴로 복사하고 붙여 넣습니다.  
  
 계획 지침을 만들기 전에 XML 계획 내에 표시된 따옴표(')에 두 번째 따옴표를 추가하여 이스케이프 처리합니다. 예를 들어 `WHERE A.varchar = 'This is a string'`이 포함된 계획에서 코드를 `WHERE A.varchar = ''This is a string''`으로 수정하여 이스케이프 처리해야 합니다.  
  
 다음 예에서는 1단계에서 수집된 쿼리 계획에 대한 계획 지침을 만들고 `@hints` 매개 변수에 쿼리에 대한 XML 실행 계획을 삽입합니다. 간단하게 나타내기 위해 이 예에는 실행 계획 중 일부만 포함되어 있습니다.  
  
```  
EXECUTE sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',  
@type = N'SQL',  
@module_or_batch = NULL,  
@params = NULL,  
@hints = N'OPTION(USE PLAN N''<ShowPlanXML xmlns=''''https://schemas.microsoft.com/sqlserver/2004/07/showplan''''   
    Version=''''0.5'''' Build=''''9.00.1116''''>  
    <BatchSequence><Batch><Statements><StmtSimple>  
    ...  
    </StmtSimple></Statements></Batch>  
    </BatchSequence></ShowPlanXML>'')';  
GO  
```  
  
### <a name="step-3-verify-that-the-plan-guide-is-applied-to-the-query"></a>3 단계: 계획 지침이 쿼리에 적용 되는지 확인  
 쿼리를 다시 실행하고 생성되는 쿼리 계획을 확인합니다. 생성된 계획이 계획 지침에 지정한 계획과 일치하는 것을 볼 수 있을 것입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_create_plan_guide &#40;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Transact-sql&#41;&#40;쿼리 힌트](/sql/t-sql/queries/hints-transact-sql-query)   
 [계획 지침](../../relational-databases/performance/plan-guides.md)  
  
  
