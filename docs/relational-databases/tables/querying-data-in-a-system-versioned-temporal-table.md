---
title: "시스템 버전 임시 테이블의 데이터 쿼리 | Microsoft 문서"
ms.custom: 
ms.date: 03/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2d358c2e-ebd8-4eb3-9bff-cfa598a39125
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5bd4678f0a17e570f089f3c532df5a32e284787d
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="querying-data-in-a-system-versioned-temporal-table"></a>시스템 버전 임시 테이블의 데이터 쿼리
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  temporal 테이블 데이터의 최신(실제) 상태를 가져오려면, 비temporal 테이블 쿼리와 완전히 동일한 방식으로 쿼리할 수 있습니다. PERIOD 열이 숨겨져 있지 않은 경우, 해당 값은 SELECT \* 쿼리에 나타납니다. **PERIOD** 열을 숨김으로 지정하면 해당 값이 SELECT \* 쿼리에 나타나지 않습니다. **PERIOD** 열이 숨겨진 경우 해당 열에 대한 값을 반환하기 위해 특히 SELECT 절의 **PERIOD** 열을 참조합니다.  
  
 모든 유형의 시간 기반 분석을 수행하려면, 4개의 임시 하위 절과 함께 새로운  **FOR SYSTEM_TIME** 절을 사용하여 현재 및 기록 테이블에서 데이터를 쿼리합니다. 이러한 절에 대한 자세한 내용은 [임시 테이블](../../relational-databases/tables/temporal-tables.md) 및 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)을 참조하세요.  
  
-   AS OF <날짜_시간>  
  
-   FROM <시작_날짜_시간> TO <종료_날짜_시간>  
  
-   BETWEEN <시작_날짜_시간> AND <종료_날짜_시간>  
  
-   CONTAINED IN (<시작_날짜_시간> , <종료_날짜_시간>)  
  
-   ALL  
  
 **FOR SYSTEM_TIME** 은 쿼리의 각 테이블에 독립적으로 지정될 수 있습니다. 공용 테이블 식, 테이블 반환 함수, 저장 프로시저 내에 사용될 수 있습니다.  
  
## <a name="query-for-a-specific-time-using-the-as-of-sub-clause"></a>AS OF 하위 절을 사용한 특정 시간의 쿼리  
 과거의 특정 시간으로 데이터의 상태를 다시 구성해야 하는 경우**AS OF** 하위 절을 사용합니다.  **PERIOD** 열 정의에 지정된 datetime2 형식의 자릿수로 데이터를 다시 구성할 수 있습니다.    
**AS OF** 하위 절은 상수 리터럴 또는 시간 조건을 동적으로 지정할 수 있는 변수와 사용될 수 있습니다. 제공된 값은 UTC 시간으로 해석됩니다.  
  
 첫 번째 예는 dbo.Department 테이블의 상태를 과거의 특정 날짜로(AS OF) 반환합니다.  
  
```  
/*State of entire table AS OF specific date in the past*/   
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
 두 번째 예는 행의 하위 집합에 시간의 두 지점 간의 값을 비교합니다.  
  
```  
DECLARE @ADayAgo datetime2   
SET @ADayAgo = DATEADD (day, -1, sysutcdatetime())   
/*Comparison between two points in time for subset of rows*/   
SELECT D_1_Ago.[DeptID], D.[DeptID],   
D_1_Ago.[DeptName], D.[DeptName],   
D_1_Ago.[SysStartTime], D.[SysStartTime],   
D_1_Ago.[SysEndTime], D.[SysEndTime]   
FROM [dbo].[Department] FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago   
JOIN [Department] AS D ON  D_1_Ago.[DeptID] = [D].[DeptID]    
AND D_1_Ago.[DeptID] BETWEEN 1 and 5 ;  
```  
  
### <a name="using-views-with-as-of-sub-clause-in-temporal-queries"></a>임시 쿼리의 AS-OF 하위 절에 뷰 사용  
 복잡한 지정 시간 분석이 필요한 경우 뷰를 사용하면 시나리오에 매우 유용합니다.   
일반적인 예로는 이전 달의 값으로 오늘 비즈니스 보고서를 생성하는 것을 들 수 있습니다.   
일반적으로 고객은 외래 키 관계와 다수의 테이블을 포함하는 정규화된 데이터 모델을 갖습니다. 모든 테이블이 각각의 방식으로 독립적으로 변하기 때문에, 정규화된 모델의 데이터가 과거에 어떻게 보였는지에 대한 질문에 답변하는 것은 매우 어려울 수 있습니다.   
이런 경우, 가장 좋은 방법은 뷰를 만들고 전체 뷰에 **AS OF** 하위 절을 적용하는 것입니다. 이러한 방식을 사용하면 SQL Server가 뷰 정의에 참여하는 모든 temporal 테이블에 **AS OF** 절을 투명하게 적용하기 때문에 데이터 액세스 계층의 모델링을 지정 시간 분석에서 분리할 수 있습니다. 또한, temporal 테이블을 비temporal 테이블과 동일한 뷰에서 결합할 수 있고, **AS OF** 가 temporal 테이블에만 적용됩니다. 뷰가 최소 하나의 temporal 테이블을 참조하지 않으면 임시 쿼리 절 적용에 오류가 발생하면서 실패합니다.  
  
```  
/* Create view that joins three temporal tables: Department, CompanyLocation, LocationDepartments */   
CREATE VIEW [dbo].[vw_GetOrgChart]   
AS   
SELECT   
     [CompanyLocation].LocID  
   , [CompanyLocation].LocName  
   , [CompanyLocation].City  
   , [Department].DeptID  
   , [Department].DeptName    
FROM [dbo].[CompanyLocation]   
LEFT JOIN [dbo].[LocationDepartments]    
   ON [CompanyLocation].LocID = LocationDepartments.LocID   
LEFT JOIN [dbo].[Department]    
   ON LocationDepartments.DeptID = [Department].DeptID ;  
GO   
/* Querying view AS OF */   
SELECT * FROM [vw_GetOrgChart]   
FOR SYSTEM_TIME AS OF '2015-09-01 T10:00:00.7230011' ;  
  
```  
  
## <a name="query-for-changes-to-specific-rows-over-time"></a>시간별 특정 행의 변화에 대한 쿼리  
 임시 하위 절 **FROM...TO**, **BETWEEN...AND** 및 **CONTAINED IN** 은 데이터 감사를 수행하려는 경우 즉, 현재 테이블의 특정 행에 대한 모든 변경 내용이 필요한 경우에 유용합니다.   
처음 두 개의 하위 절은 지정된 기간과 겹치는(즉, 지정된 기간 전에 시작되고 그 후에 종료되는) 행 버전을 반환하는 반면, CONTAINED IN은 지정된 기간 범위 내에 존재하는 것들만 반환합니다.  
  
> [!IMPORTANT]  
>  비현재 행 버전만을 검색하는 경우 **CONTAINED IN** 을 사용하는 것이 좋습니다. 이것은 기록 테이블에서만 작동하고 최고의 쿼리 성능을 냅니다. 아무런 제한 없이 현재 데이터와 기록 데이터를 쿼리해야 하는 경우 **ALL** 을(를) 사용합니다.  
  
```  
/* Query using BETWEEN...AND sub-clause*/  
SELECT   
     [DeptID]  
   , [DeptName]  
   , [SysStartTime]  
   , [SysEndTime]  
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual   
FROM [dbo].[Department]   
FOR SYSTEM_TIME BETWEEN  '2015-01-01' AND '2015-12-31'   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC;   
  
/*  Query using CONTAINED IN sub-clause */  
SELECT [DeptID], [DeptName], [SysStartTime],[SysEndTime]   
FROM [dbo].[Department]   
FOR SYSTEM_TIME CONTAINED IN ('2015-04-01', '2015-09-25')   
WHERE DeptId = 1   
ORDER BY SysStartTime DESC ;  
  
/*  Query using ALL sub-clause */   
SELECT    
     [DeptID]   
   , [DeptName]   
   , [SysStartTime]   
   , [SysEndTime]   
   , IIF (YEAR(SysEndTime) = 9999, 1, 0) AS IsActual    
FROM [dbo].[Department] FOR SYSTEM_TIME ALL   
ORDER BY [DeptID], [SysStartTime] Desc  
  
```  
  
## <a name="did-this-article-help-you-were-listening"></a>이 문서가 도움이 되었나요? 여러분의 의견을 환영합니다.  
 어떤 정보를 찾고 계세요? 정보를 찾으셨나요? 여러분의 의견은 문서의 내용을 개선하는 데 많은 도움이 됩니다. 의견이 있으면 [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Queryinging%20a%20System-Versioned%20Temporal%20Table%20page)  
  
## <a name="see-also"></a>참고 항목  
 [임시 테이블](../../relational-databases/tables/temporal-tables.md)   
 [FROM&#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [시스템 버전 임시 테이블 만들기](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블의 데이터 수정](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블의 스키마 변경](../../relational-databases/tables/changing-the-schema-of-a-system-versioned-temporal-table.md)   
 [시스템 버전 임시 테이블에서 시스템 버전 관리 중지](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)  
  
  
