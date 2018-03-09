---
title: "계획 지침 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TEMPLATE plan guide
- SQL plan guides
- OPTIMIZE FOR query hint
- RECOMPILE query hint
- OBJECT plan guide
- plan guides [SQL Server], about plan guides
- OPTION clause
- plan guides [SQL Server]
- USE PLAN query hint
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f6b2bd
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a0414a27a14e937e7c58ca6ba74de3b6bfd6a2b0
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="plan-guides"></a>계획 지침
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 실제 쿼리의 텍스트를 직접 변경할 수 없거나 직접 변경하지 않으려는 경우 계획 지침에 따라 쿼리 성능을 최적화할 수 있습니다. 계획 지침은 쿼리 힌트 또는 고정 쿼리 계획을 연결하여 쿼리 최적화에 영향을 줍니다. 계획 안내는 타사 공급업체에서 제공된 데이터베이스 응용 프로그램의 일부 쿼리 하위 집합이 올바른 성능을 내지 못하는 경우에 유용합니다. 계획 지침에서 최적화하려는 Transact-SQL 문을 지정하고 사용할 쿼리 힌트가 들어 있는 OPTION 절이나 쿼리를 최적화하는 데 사용할 특정 쿼리 계획을 지정합니다. 쿼리가 실행하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 Transact-SQL 문을 계획 지침과 대응시키고 런타임에 쿼리에 OPTION 절을 추가하거나 지정된 쿼리 계획을 사용합니다.  
  
 만들 수 있는 총 계획 지침 수는 사용 가능한 시스템 리소스에 의해서만 제한됩니다. 그러나 계획 지침은 성능 향상이나 안정화를 목적으로 하는 중요 업무용 쿼리로 제한되어야 합니다. 배포된 응용 프로그램의 쿼리 로드 대부분에 영향을 주기 위해 계획 지침을 사용하면 안 됩니다.  
  
> [!NOTE]  
>  계획 지침은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 일부 버전에서 사용할 수 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요. 계획 지침은 모든 버전에 표시됩니다. 계획 지침이 포함된 데이터베이스를 모든 버전에 추가할 수 있습니다. 업그레이드된 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 데이터베이스를 복원하거나 첨부해도 계획 지침은 그대로 유지됩니다.  
  
## <a name="types-of-plan-guides"></a>계획 지침의 유형  
 다음과 같은 계획 지침 유형을 만들 수 있습니다.  
  
 ### <a name="object-plan-guide"></a>OBJECT 계획 지침  
 OBJECT 계획 지침은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저, 사용자 정의 스칼라 함수, 다중 문 사용자 정의 테이블 반환 함수 및 DML 트리거의 컨텍스트에서 실행되는 쿼리와 일치합니다.  
  
 `@Country_region` 데이터베이스에 대해 배포되는 데이터베이스 응용 프로그램에 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 매개 변수를 가져오는 다음 저장 프로시저가 있다고 가정합니다.  
  
```sql  
CREATE PROCEDURE Sales.GetSalesOrderByCountry (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h, Sales.Customer AS c,   
        Sales.SalesTerritory AS t  
    WHERE h.CustomerID = c.CustomerID  
        AND c.TerritoryID = t.TerritoryID  
        AND CountryRegionCode = @Country_region  
END;  
```  
  
 이 저장 프로시저가 `@Country_region = N'AU'`(오스트레일리아)에 맞게 컴파일되고 최적화되었다고 가정합니다. 그러나 오스트레일리아에서 발주되는 판매 주문이 비교적 적기 때문에 판매 주문이 더 많은 국가의 매개 변수 값을 사용하여 쿼리를 실행할 경우 성능이 저하됩니다. 미국이 판매 주문을 가장 많이 내므로 `@Country_region = N'US'` 매개 변수의 가능한 모든 값에 대해 `@Country_region` 에 대해 생성된 쿼리 계획이 더 잘 수행될 가능성이 높습니다.  
  
 저장 프로시저를 수정하여 `OPTIMIZE FOR` 쿼리 힌트를 쿼리에 추가하면 이 문제를 해결할 수 있습니다. 그러나 저장 프로시저가 배포된 응용 프로그램 안에 있기 때문에 응용 프로그램 코드를 직접 수정할 수 없습니다. 대신 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 다음 계획 지침을 만들 수 있습니다.  
  
```sql  
sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT *FROM Sales.SalesOrderHeader AS h,  
        Sales.Customer AS c,  
        Sales.SalesTerritory AS t  
        WHERE h.CustomerID = c.CustomerID   
            AND c.TerritoryID = t.TerritoryID  
            AND CountryRegionCode = @Country_region',  
@type = N'OBJECT',  
@module_or_batch = N'Sales.GetSalesOrderByCountry',  
@params = NULL,  
@hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
 `sp_create_plan_guide` 문에 지정되어 있는 쿼리가 실행되면 `OPTIMIZE FOR (@Country = N''US'')` 절을 포함하도록 최적화 이전에 쿼리가 수정됩니다.  
  
 ### <a name="sql-plan-guide"></a>SQL 계획 지침  
 SQL 계획 지침은 데이터베이스 개체의 일부가 아닌 독립 실행형 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 일괄 처리의 컨텍스트에서 실행되는 쿼리와 일치합니다. SQL 기반 계획 지침은 지정된 형식으로 매개 변수화되는 쿼리와 일치되도록 하는 데도 사용될 수 있습니다. SQL 계획 지침은 독립 실행형 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 및 일괄 처리에 적용됩니다. 이러한 문은 종종 응용 프로그램에서 [sp_executesql](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) 시스템 저장 프로시저를 사용하여 제출됩니다. 예를 들어 다음 독립 실행형 일괄 처리를 생각해 보십시오.  
  
```sql  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 병렬 실행 계획이 이 쿼리에서 생성되지 않도록 하려면 다음 계획 지침을 만들고 `MAXDOP` 쿼리 힌트를 `1` 매개 변수의 `@hints` 로 설정합니다.  
  
```sql  
sp_create_plan_guide   
@name = N'Guide2',   
@stmt = N'SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC',  
@type = N'SQL',  
@module_or_batch = NULL,   
@params = NULL,   
@hints = N'OPTION (MAXDOP 1)';  
```  
  
> [!IMPORTANT]  
>  `@module_or_batch` 문의 `@params` 및 `sp_create_plan guide` 인수에 대해 제공되는 값은 실제 쿼리에서 전송되는 해당 텍스트와 일치해야 합니다. 자세한 내용은 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) 문의 [SQL Server Profiler를 사용하여 계획 지침 작성 및 테스트](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)에서 실제 쿼리의 텍스트를 직접 변경할 수 없거나 직접 변경하지 않으려는 경우 계획 지침에 따라 쿼리 성능을 최적화할 수 있습니다.  
  
 PARAMETERIZATION 데이터베이스 옵션을 FORCED로 설정했거나 쿼리 클래스를 매개 변수화하도록 지정하는 TEMPLATE 계획 지침을 만든 경우에 같은 형식으로 매개 변수화된 쿼리에 대해서도 SQL 계획 지침을 만들 수 있습니다.  
  
 ### <a name="template-plan-guide"></a>TEMPLATE 계획 지침  
 TEMPLATE 계획 지침은 지정된 형식으로 매개 변수화되는 독립 실행형 쿼리와 일치합니다. 이 계획 지침은 쿼리 클래스에 대한 데이터베이스의 현재 PARAMETERIZATION 데이터베이스 SET 옵션을 대체하는 데 사용됩니다.  
  
 다음과 같은 경우 TEMPLATE 계획 지침을 만들 수 있습니다.  
  
-   PARAMETERIZATION 데이터베이스 옵션이 FORCED로 설정되었지만 [단순 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) 규칙에 따라 컴파일하려는 쿼리가 있는 경우  
  
-   PARAMETERIZATION 데이터베이스 옵션이 SIMPLE(기본 설정)로 설정되었지만 쿼리 클래스에 대해 [강제 매개 변수화](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 시도하려는 경우  
  
## <a name="plan-guide-matching-requirements"></a>계획 지침 일치 요구 사항  
 계획 지침의 범위는 이 지침이 생성되는 데이터베이스입니다. 따라서 쿼리를 실행할 때 현재 데이터베이스에 있는 계획 지침만 쿼리에 일치시킬 수 있습니다. 예를 들어 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 가 현재 데이터베이스이면 다음 쿼리가 실행됩니다.  
  
 ```sql
 SELECT FirstName, LastName FROM Person.Person;
 ```  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스의 계획 지침만 이 쿼리에 일치될 수 있습니다. 그러나 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 가 현재 데이터베이스이면 다음 문이 실행됩니다.  
  
 ```sql
 USE DB1; 
 SELECT FirstName, LastName FROM Person.Person;
 ```  
  
 쿼리가 `DB1` 컨텍스트에서 실행되므로 `DB1`의 계획 지침만 쿼리에 일치됩니다.  
  
 SQL 또는 TEMPLATE 기반 계획 지침을 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 두 값의 문자를 비교하여 @module_or_batch 및 @params 인수의 값을 일치시킵니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 실제 일괄 처리에서 수신한 것과 똑같이 텍스트를 제공해야 합니다.  
  
 @type이 'SQL'이고 @module_or_batch가 NULL로 설정된 경우 @module_or_batch 값은 @stmt 값으로 설정됩니다. 이는 *statement_text* 의 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 전송된 것과 문자 수준까지 같은 형식으로 제공되어야 함을 의미합니다. 이 일치 작업을 더 효과적으로 처리하기 위해 내부 변환은 수행되지 않습니다.  
  
 일반(SQL 또는 OBJECT) 계획 지침 및 TEMPLATE 계획 지침 모두 문에 적용할 수 있을 경우 일반 계획 지침만 사용됩니다.  
  
> [!NOTE]  
>  계획 지침을 만들려는 문이 포함된 일괄 처리는 USE *database* 문을 포함할 수 없습니다.  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>계획 캐시의 계획 지침 효과  
 모듈에 대한 계획 지침을 만들면 계획 캐시에서 해당 모듈에 대한 쿼리 계획이 제거되고, 일괄 처리에 OBJECT 또는 SQL 유형의 계획 지침을 만들면 같은 해시 값을 가진 일괄 처리에 대한 쿼리 계획이 제거되며, TEMPLATE 유형의 계획 지침을 만들면 해당 데이터베이스 내의 계획 캐시에서 단일 문 일괄 처리가 모두 제거됩니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크|항목|  
|----------|-----------|  
|계획 지침을 만드는 방법에 대해 설명합니다.|[새 계획 지침 만들기](../../relational-databases/performance/create-a-new-plan-guide.md)|  
|매개 변수가 있는 쿼리에 대한 계획 지침을 만드는 방법에 대해 설명합니다.|[매개 변수가 있는 쿼리를 위한 계획 지침 만들기](../../relational-databases/performance/create-a-plan-guide-for-parameterized-queries.md)|  
|계획 지침을 사용하여 쿼리 매개 변수화 동작을 제어하는 방법에 대해 설명합니다.|[계획 지침을 사용하여 쿼리 매개 변수화 동작 지정](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)|  
|계획 지침에 고정 쿼리를 포함하는 방법에 대해 설명합니다.|[계획 지침에 정해진 쿼리 계획 적용](../../relational-databases/performance/apply-a-fixed-query-plan-to-a-plan-guide.md)|  
|계획 지침에서 쿼리 힌트를 지정하는 방법에 대해 설명합니다.|[계획 지침에 쿼리 힌트 연결](../../relational-databases/performance/attach-query-hints-to-a-plan-guide.md)|  
|계획 지침 속성을 보는 방법에 대해 설명합니다.|[계획 지침 속성 보기](../../relational-databases/performance/view-plan-guide-properties.md)|  
|SQL Server Profiler를 사용하여 계획 지침을 작성 및 테스트하는 방법에 대해 설명합니다.|[SQL Server Profiler를 사용하여 계획 지침 작성 및 테스트](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)|  
|계획 지침의 유효성을 검사하는 방법에 대해 설명합니다.|[업그레이드 후 계획 지침의 유효성 검사](../../relational-databases/performance/validate-plan-guides-after-upgrade.md)|  
  
## <a name="see-also"></a>참고 항목  
 [sp_create_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sp_control_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [sys.fn_validate_plan_guide&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)  
  
  
