---
title: 통계 속성 보기 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.statistics.details.f1
helpviewer_keywords:
- viewing statistics properties
- statistics [SQL Server], viewing properties
ms.assetid: 0eaa2101-006e-4015-9979-3468b50e0aaa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 021129bca0e72d32128c72c108bf2a03009c4d30
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551233"
---
# <a name="view-statistics-properties"></a>통계 속성 보기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 테이블 또는 인덱싱된 뷰에 대한 현재 쿼리 최적화 통계를 표시할 수 있습니다. 통계 개체에는 통계에 대한 메타데이터가 있는 헤더, 통계 개체의 첫 번째 키 열에 있는 값의 분포에 대한 히스토그램, 그리고 열 간 상관 관계를 측정하는 밀도 벡터가 포함됩니다. 히스토그램 및 밀도 벡터에 대한 자세한 내용은 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)를 참조하세요.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 통계 속성을 보려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 통계 개체를 보려면 테이블의 소유자이거나 **sysadmin** 고정 서버 역할, **db_owner** 고정 데이터베이스 역할 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-statistics-properties"></a>통계 속성을 보려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 새 통계를 만들 데이터베이스를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **테이블** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 통계 속성을 보려는 테이블을 확장합니다.  
  
4.  더하기 기호를 클릭하여 **통계** 폴더를 확장합니다.  
  
5.  속성을 보려는 통계 개체를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
6.  **통계 속성 -** *statistics_name* 대화 상자의 **페이지 선택** 창에서 **자세히**를 선택합니다.  
  
     **통계 속성 -**  **statistics_name** *statistics_name* 페이지에 다음 속성이 표시됩니다.  
  
     **테이블 이름**  
     통계에서 설명하는 테이블 이름을 표시합니다.  
  
     **통계 이름**  
     통계가 저장되는 데이터베이스 개체 이름을 표시합니다.  
  
     **인덱스 statistics_name에 대한 통계**  
     이 텍스트 상자에는 통계 개체에서 반환되는 속성이 표시됩니다. 이 속성은 통계 헤더, 밀도 벡터 및 히스토그램의 세 가지 섹션으로 이루어져 있습니다.  
  
     다음 정보는 통계 헤더의 결과 집합에 반환되는 열에 대한 설명입니다.  
  
     **이름**  
     통계 개체의 이름입니다.  
  
     **업데이트**  
     통계가 마지막으로 업데이트된 날짜와 시간입니다.  
  
     **행**  
     통계가 마지막으로 업데이트되었을 때 테이블 또는 인덱싱된 뷰의 전체 행 수입니다. 통계가 필터링되거나 필터링된 인덱스에 해당하는 경우 행 수가 테이블의 행 수보다 적을 수 있습니다.  
  
     **샘플링한 행**  
     통계 계산을 위해 샘플링된 전체 행 수입니다. 샘플링된 행 수가 전체 행 수보다 적은 경우 표시되는 히스토그램과 밀도 결과는 샘플링된 행을 기준으로 하는 예상치입니다.  
  
     **단계**  
     히스토그램의 총 단계 수입니다. 각 단계의 범위는 열 값에서 상한 열 값까지입니다. 히스토그램 단계는 통계의 첫 번째 키 열에 정의됩니다. 최대 단계 수는 200개입니다.  
  
     **밀도**  
     히스토그램 경계 값을 제외하고 통계 개체의 첫 번째 키 열에 있는 모든 값에 대해 1/ *고유 값* 으로 계산됩니다. 이 밀도 값은 쿼리 최적화 프로그램에서 사용되지 않으며 SQL Server 2008 이전 버전과의 호환성을 위해 표시됩니다.  
  
     **평균 키 길이**  
     통계 개체의 키 열에 있는 모든 값에 대한 값당 평균 바이트 수입니다.  
  
     **문자열 인덱스**  
     '예'는 통계 개체에 LIKE 연산자를 사용하는 쿼리 조건자(예: `WHERE ProductName LIKE '%Bike'`)의 카디널리티 예상치 정확도를 높이기 위한 문자열 요약 통계가 있음을 나타냅니다. 문자열 요약 통계는 히스토그램과는 별도로 저장되며 통계 개체에서 **char**, **varchar**, **nchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **text**또는 **ntext**형식인 첫 번째 키 열에 생성됩니다.  
  
     **필터 식**  
     통계 개체에 포함된 테이블 행의 하위 집합에 대한 조건자입니다. NULL = 필터링되지 않은 통계입니다.  
  
     **필터링되지 않은 행**  
     필터 식을 적용하기 전 테이블에 있는 전체 행 수입니다. 필터 식이 NULL이면 필터링되지 않은 행과 행이 동일합니다.  
  
     다음 정보는 밀도 벡터의 결과 집합에 반환되는 열에 대한 설명입니다.  
  
     **모든 밀도**  
     밀도는 1/ *고유 값*입니다. 결과에는 통계 개체에 있는 각 열 접두사의 밀도가 한 행씩 표시됩니다. 고유 값은 행별 및 열 접두사별 열 값의 고유한 목록입니다. 예를 들어 통계 개체가 키 열 (A, B, C)를 포함하는 경우 결과에서 밀도는 이러한 각 열 접두사의 고유 값 목록인 (A), (A,B) 및 (A, B, C)로 보고됩니다. 접두사 (A, B, C)를 사용하면 이러한 각 목록은 고유 값 목록 (3, 5, 6), (4, 4, 6), (4, 5, 6), (4, 5, 7)입니다. 접두사 (A, B)를 사용하면 동일한 열 값은 고유 값 목록 (3, 5), (4, 4) 및 (4, 5)입니다.  
  
     **평균 길이**  
     열 접두사의 열 값 목록을 저장하기 위한 평균 길이(바이트)입니다. 예를 들어 목록 (3, 5, 6)의 각 값에 4바이트가 필요한 경우 길이는 12바이트입니다.  
  
     **열**  
     모든 밀도 및 평균 길이가 표시되는 접두사의 열 이름입니다.  
  
     다음 정보는 히스토그램의 결과 집합에 반환되는 열에 대한 설명입니다.  
  
     **RANGE_HI_KEY**  
     히스토그램 단계의 상한 열 값입니다. 열 값은 키 값이라고도 합니다.  
  
     **RANGE_ROWS**  
     상한을 제외한 히스토그램 단계 내에 열 값이 있는 예상 행 수입니다.  
  
     **EQ_ROWS**  
     히스토그램 단계에서 상한과 열 값이 동일한 예상 행 수입니다.  
  
     **DISTINCT_RANGE_ROWS**  
     상한을 제외한 히스토그램 단계 내에 고유한 열 값이 있는 예상 행 수입니다.  
  
     **AVG_RANGE_ROWS**  
     상한을 제외한 히스토그램 단계 내에 중복 열 값이 있는 평균 행 수입니다(DISTINCT_RANGE_ROWS > 0인 경우 RANGE_ROWS/DISTINCT_RANGE_ROWS).  
  
7.  **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-statistics-properties"></a>통계 속성을 보려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example displays all statistics information for the AK_Address_rowguid index of the Person.Address table.   
    DBCC SHOW_STATISTICS ("Person.Address", AK_Address_rowguid);   
    GO  
    ```  
  
 자세한 내용은 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)를 참조하세요.  
  
#### <a name="to-find-all-of-the-statistics-on-a-table-or-view"></a>테이블 또는 뷰에서 모든 통계를 찾으려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Gets the following information: name and ID of the statistics, whether the statistics were created automatically or by the user, whether the statistics were created with the NORECOMPUTE option, and whether the statistics have a filter and, if so, what that filter is.  
    */  
    SELECT name AS statistics_name  
        ,stats_id  
        ,auto_created  
        ,user_created  
        ,no_recompute  
        ,has_filter  
        ,filter_definition  
    -- using the sys.stats catalog view  
    FROM sys.stats  
    -- for the Sales.SpecialOffer table  
    WHERE object_id = OBJECT_ID('Sales.SpecialOffer');  
    GO  
    ```  
  
 자세한 내용은 [sys.stats&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)를 참조하세요.  
  
  
