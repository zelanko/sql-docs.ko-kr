---
title: "통계 | Microsoft 문서"
ms.custom: 
ms.date: 10/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-statistics
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
caps.latest.revision: 70
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1c55b7b8b39e7b1ec296ee529bc66d2e14256994
ms.openlocfilehash: 59d83fc61c1a595c1ab95515060682269eaf465e
ms.contentlocale: ko-kr
ms.lasthandoff: 10/12/2017

---
# <a name="statistics"></a>통계
  쿼리 최적화 프로그램에서는 통계를 사용하여 쿼리 성능을 향상하는 쿼리 계획을 만듭니다. 대부분의 쿼리에서 쿼리 최적화 프로그램은 고품질의 쿼리 계획에 필요한 통계를 이미 생성하므로 경우에 따라서 최상의 결과를 위해 추가 통계를 만들거나 쿼리 설계를 수정해야 합니다. 이 항목에서는 통계 개념에 대해 설명하고 쿼리 최적화 통계를 효율적으로 사용하기 위한 지침을 제공합니다.  
  
##  <a name="DefinitionQOStatistics"></a> 구성 요소 및 개념  
### <a name="statistics"></a>통계  
 쿼리 최적화 통계는 테이블이나 인덱싱된 뷰에서 하나 이상의 열에 있는 값의 분포에 대한 통계 정보를 포함하는 개체입니다. 쿼리 최적화 프로그램은 이러한 통계를 사용하여 쿼리 결과에서 *카디널리티* 또는 행 수를 계산합니다. 쿼리 최적화 프로그램은 이러한 *카디널리티 예상치*를 통해 고품질의 쿼리 계획을 만듭니다. 예를 들어 조건자에 따라 쿼리 최적화 프로그램은 카디널리티 예상치를 사용하여 리소스를 많이 사용하는 Index Scan 연산자 대신 Index Seek 연산자를 선택할 수 있으며 이렇게 하면 쿼리 성능이 향상됩니다.  
  
 각 통계 개체는 하나 이상의 테이블 열 목록에 대해 작성되며 첫 번째 열의 값 분포를 나타내는 히스토그램을 포함합니다. 여러 열에 대한 통계 개체는 또한 열 사이의 값의 상관 관계에 대한 통계 정보도 저장합니다. 이러한 상관 관계 통계 또는 *밀도*는 열 값의 개별 행 수에서 생성됩니다. 통계 개체에 대한 자세한 내용은 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)를 참조하세요.  
  
### <a name="filtered-statistics"></a>필터링된 통계  
 필터링된 통계는 잘 정의된 데이터의 하위 집합에서 선택하는 쿼리에 대한 쿼리 성능을 높일 수 있습니다. 또한 필터 조건자를 사용하여 통계에 포함되는 데이터의 하위 집합을 선택할 수 있습니다. 잘 디자인된 필터링된 통계는 전체 테이블 통계에 비해 쿼리 실행 계획을 향상시킬 수 있습니다. 필터 조건자에 대한 자세한 내용은 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)를 참조하세요. 필터링된 통계를 작성하는 시기에 대한 자세한 내용은 이 항목의 [통계 작성 시기](#CreateStatistics) 섹션을 참조하십시오.  
  
### <a name="statistics-options"></a>통계 옵션  
 통계가 작성되고 업데이트되는 시기 및 방법에 영향을 주는 다음 세 가지 옵션을 설정할 수 있습니다. 이러한 옵션은 데이터베이스 수준에서만 설정됩니다.  
  
#### <a name="autocreatestatistics-option"></a>AUTO_CREATE_STATISTICS 옵션  
 자동 통계 작성 옵션 AUTO_CREATE_STATISTICS가 ON으로 설정된 경우 쿼리 최적화 프로그램은 필요에 따라 쿼리 조건자의 개별 열에 대한 통계를 작성하므로 쿼리 계획에 대한 카디널리티 예상치의 정확도가 높아집니다. 이러한 단일 열 통계는 기존 통계 개체에 히스토그램이 없는 열에 대해 작성됩니다. AUTO_CREATE_STATISTICS 옵션에서는 인덱스에 대해 통계가 작성되는지 확인하지 않습니다. 이 옵션은 또한 필터링된 통계도 생성하지 않으며 전체 테이블에 대한 단일 열 통계에 엄격하게 적용됩니다.  
  
 쿼리 최적화 프로그램이 AUTO_CREATE_STATISTICS 옵션 사용 결과로 통계를 작성하면 통계 이름이 `_WA`로 시작합니다. 다음 쿼리를 사용하여 쿼리 최적화 프로그램이 쿼리 조건자 열에 대한 통계를 작성했는지 확인할 수 있습니다.  
  
```tsql  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
#### <a name="autoupdatestatistics-option"></a>AUTO_UPDATE_STATISTICS 옵션  
 자동 통계 업데이트 옵션 AUTO_UPDATE_STATISTICS가 ON으로 설정되면 쿼리 최적화 프로그램은 통계가 최신이 아닌 통계가 되는 시점을 확인한 다음, 쿼리에서 사용될 때 이를 업데이트합니다. 삽입, 업데이트, 삭제 또는 병합 작업을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음, 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.  
  
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이하 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 변경된 행 비율에 따라 임계값을 사용합니다. 테이블의 행 수에 관계없이 이러한 방식이 사용됩니다. 임계값은 다음과 같습니다.
    * 통계 평가 시 테이블 카디널리티가 500 이하이면, 500개 수정 사항마다 업데이트합니다.
    * 통계 평가 시 테이블 카디널리티가 500 초과이면, 500+20%의 수정 사항마다 업데이트합니다.

* [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 호환성 수준이 130 미만인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 테이블의 행 수에 따라 조정되는, 감소하는 동적 통계 업데이트 임계값을 사용합니다. 이 값은 1,000의 제곱근에 현재 테이블 카디널리티를 곱한 값으로 계산됩니다. 이러한 변경으로 인해 큰 테이블의 통계 업데이트 빈도가 높아집니다. 그러나 데이터베이스의 호환성 수준이 130 미만이면 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 임계값이 적용됩니다.  
  
쿼리 최적화 프로그램은 쿼리를 컴파일하기 전과 캐시된 쿼리 계획을 실행하기 전에 최신이 아닌 통계가 있는지를 확인합니다. 쿼리 최적화 프로그램은 쿼리를 컴파일하기 전에 쿼리 조건자의 열, 테이블 및 인덱싱된 뷰를 사용하여 어떤 통계가 최신이 아닌지 결정합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 캐시된 쿼리 계획을 실행하기 전에 쿼리 계획에서 최신 통계가 참조되는지 확인합니다.  
  
AUTO_UPDATE_STATISTICS 옵션은 인덱스에 대해 작성된 통계 개체, 쿼리 조건자의 단일 열 및 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문으로 작성된 통계에 적용됩니다. 이 옵션은 또한 필터링된 통계에도 적용됩니다.  
 
AUTO_UPDATE_STATISTICS 제어 방법에 대한 자세한 내용은 [SQL Server의 Autostat(AUTO_UPDATE_STATISTICS) 동작 제어](http://support.microsoft.com/help/2754171)를 참조하세요.
  
#### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC  
 비동기 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS_ASYNC는 쿼리 최적화 프로그램이 동기 또는 비동기 통계 업데이트를 사용하는지를 결정합니다. 기본적으로 비동기 통계 업데이트 옵션은 OFF이며 쿼리 최적화 프로그램은 통계를 동기적으로 업데이트합니다. AUTO_UPDATE_STATISTICS_ASYNC 옵션은 인덱스에 대해 작성된 통계 개체, 쿼리 조건자의 단일 열 및 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문으로 작성된 통계에 적용됩니다.  
 
 > [!NOTE]
 > [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 비동기 통계 업데이트 옵션을 설정하려면 *데이터베이스 속성* 창의 *옵션* 페이지에서 *통계 자동 업데이트* 및 *통계를 비동기적으로 자동 업데이트* 옵션을 둘 다 **True**로 설정해야 합니다.
  
 통계 업데이트는 동기(기본값) 또는 비동기일 수 있습니다. 동기 통계 업데이트의 경우 쿼리는 항상 최신 통계로 컴파일하고 실행합니다. 통계가 최신이 아닌 경우 쿼리를 컴파일하고 실행하기 전에 쿼리 최적화 프로그램에서 업데이트된 통계를 기다립니다. 비동기 통계 업데이트의 경우 쿼리는 기존 통계가 최신 통계가 아닌 경우에도 기존 통계로 컴파일합니다. 쿼리가 컴파일될 때 통계가 오래된 통계인 경우 쿼리 최적화 프로그램은 만족스럽지 못한 쿼리 계획을 선택할 수 있습니다. 비동기 업데이트가 완료된 이후 컴파일된 쿼리는 업데이트된 통계 사용의 이점을 얻을 수 있습니다.  
  
 테이블을 잘라내거나 상당 비율의 행에 대해 대량 업데이트를 수행하는 경우와 같이 데이터 분포를 변경하는 작업을 수행할 때는 동기 통계를 사용하는 것이 좋습니다. 작업을 완료한 후 통계를 업데이트하지 않은 경우 동기 통계를 사용하면 변경된 데이터에 대해 쿼리를 실행하기 전에 통계를 최신 상태로 유지할 수 있습니다.  
  
 다음과 같은 시나리오에서 보다 예상 가능한 쿼리 응답 시간을 얻으려면 비동기 통계를 사용하십시오.  
  
* 응용 프로그램에서 동일한 쿼리, 유사한 쿼리 또는 유사한 캐시된 쿼리 계획을 자주 실행하는 경우. 쿼리 최적화 프로그램은 최신 통계를 기다리지 않고 들어오는 쿼리를 실행할 수 있으므로 동기 통계 업데이트보다는 비동기 통계 업데이트를 사용할 때, 더욱 예상 가능한 쿼리 응답 시간을 얻을 수 있습니다. 이 방법으로 일부 쿼리의 지연을 방지할 수 있습니다.  
  
* 응용 프로그램에서 통계 업데이트를 기다리는 하나 이상의 쿼리로 인해 클라이언트 요청 제한 시간을 초과하는 경우가 있습니다. 동기 통계를 기다리는 경우 엄격한 시간 제한이 있는 응용 프로그램은 실패할 수 있습니다.  
  
#### <a name="incremental-stats"></a>INCREMENTAL STATS  
 ON으로 설정된 경우 파티션 통계별로 통계가 작성됩니다. OFF로 설정된 경우 통계 트리가 삭제되고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 통계를 다시 계산합니다. 기본값은 OFF입니다. 이 설정은 데이터베이스수준 INCREMENTAL 속성을 재정의합니다.  
  
 큰 테이블에 새 파티션이 추가되는 경우 새 파티션을 포함하도록 통계가 업데이트되어야 합니다. 하지만 전체 테이블 검색((FULLSCAN 또는 SAMPLE 옵션)에 걸리는 시간이 꽤 길 수 있습니다. 또한 새 파티션에 대한 통계만 필요한 경우 전체 테이블 검색이 필요하지 않습니다. 증분 옵션은 파티션별로 통계를 작성 및 저장하며 파티션이 업데이트되는 경우 새 통계가 필요한 해당 파티션에 대해서만 통계를 새로 고칩니다.  
  
 파티션별 통계가 지원되지 않는 경우에는 이 옵션이 무시되고 경고가 생성됩니다. 다음 통계 유형에 대해서는 증분 통계가 지원되지 않습니다.  
  
* 기본 테이블을 기준으로 파티션 정렬되지 않은 인덱스를 사용하여 작성된 통계입니다.  
  
* Always On 읽기 가능한 보조 데이터베이스에 대해 작성된 통계입니다.  
  
* 읽기 전용 데이터베이스에 대해 작성된 통계입니다.  
  
* 필터링된 인덱스에 대해 작성된 통계입니다.  
  
* 뷰에 대해 작성된 통계입니다.  
  
* 내부 테이블에 대해 작성된 통계입니다.  
  
* 공간 인덱스 또는 XML 인덱스를 사용하여 작성된 통계입니다.  
  
**적용 대상**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지 
  
## <a name="CreateStatistics"></a> 통계 작성 시기  
 쿼리 최적화 프로그램은 다음과 같은 방법으로 통계를 작성합니다.  
  
1.  인덱스가 만들어진 경우 쿼리 최적화 프로그램에서 테이블 또는 뷰의 인덱스에 대한 통계를 작성합니다. 이러한 통계는 인덱스의 키 열에 대해 만들어집니다. 인덱스가 필터링된 인덱스인 경우 쿼리 최적화 프로그램은 필터링된 인덱스로 지정된 행의 동일한 하위 집합에 대해 필터링된 통계를 작성합니다. 필터링된 인덱스에 대한 자세한 내용은 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md) 및 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)를 참조하세요.  
  
2.  AUTO_CREATE_STATISTICS가 ON이면 쿼리 최적화 프로그램은 쿼리 조건자의 단일 열에 대한 통계를 작성합니다.  
  
대부분의 쿼리에서 통계를 만드는 두 가지 방법을 통해 고품질의 쿼리 계획을 만들 수 있습니다. 경우에 따라서 [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) 문으로 추가 통계를 작성하여 쿼리 계획을 향상시킬 수 있습니다. 인덱스 또는 단일 열에 대해 통계를 작성할 때, 이러한 추가 통계를 통해 쿼리 최적화 프로그램에 설명되지 않은 통계 상관 관계를 캡처할 수 있습니다. 응용 프로그램에 테이블 데이터의 추가 통계 상관 관계를 포함할 수 있으며 이를 통계 개체로 계산하는 경우 쿼리 최적화 프로그램에서 쿼리 계획을 향상하도록 할 수 있습니다. 예를 들어 데이터 행의 하위 집합에 대한 필터링된 통계 또는 쿼리 조건자 열에 대한 여러 열 통계는 쿼리 계획을 향상시킬 수 있습니다.  
  
CREATE STATISTICS 문으로 통계를 만들 때 쿼리 최적화 프로그램에서 쿼리 조건자 열에 대한 단일 열 통계를 계속해서 정기적으로 작성할 수 있도록 AUTO_CREATE_STATISTICS 옵션을 유지하는 것이 좋습니다. 쿼리 조건자에 대한 자세한 내용은 [검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  
  
다음 중 한 가지가 적용되는 경우 CREATE STATISTICS 문으로 통계를 작성하십시오.  

* [!INCLUDE[ssDE](../../includes/ssde-md.md)] 튜닝 관리자가 통계 작성을 제안하는 경우  

* 쿼리 조건자에 동일한 인덱스에 없는 관련된 여러 열이 포함된 경우  

* 쿼리가 데이터 하위 집합에서 선택하는 경우  

* 쿼리에 통계가 누락된 경우  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>쿼리 조건자에 관련된 여러 열이 포함된 경우  
 쿼리 조건자에 열 간 관계 및 종속성을 가지는 여러 열이 포함된 경우 여러 열에 대한 통계를 통해 쿼리 계획을 향상시킬 수 있습니다. 여러 열 통계에는 단일 열 통계에서 사용할 수 없는 *밀도*라고 하는 열 간 상호 관계 통계가 포함됩니다. 쿼리 결과가 여러 행 간 데이터 관계에 종속되는 경우 밀도를 사용하여 카디널리티 예상치 정확도를 높일 수 있습니다.  
  
 열이 이미 동일한 인덱스에 있는 경우 여러 열 통계 개체가 이미 존재하므로 여러 열 통계 개체를 직접 만들 필요가 없습니다. 열이 동일한 인덱스에 없는 경우 CREATE STATISTICS 문을 사용하여 열에 대한 인덱스를 만들어서 여러 열 통계를 작성할 수 있습니다. 통계 개체보다는 인덱스를 유지하는 데 더 많은 시스템 리소스가 필요합니다. 응용 프로그램에 여러 열 인덱스가 필요하지 않은 경우 인덱스를 만들지 않고 통계 개체를 만들어서 시스템 리소스를 절약할 수 있습니다.  
  
 여러 열 통계를 작성할 때 통계 개체 정의에서 열 순서는 카디널리티 예상치를 만들기 위한 밀도 효율성에 영향을 줍니다. 통계 개체는 주요 열의 각 접두사에 대한 밀도를 통계 개체 정의에 저장합니다. 밀도에 대한 자세한 내용은 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)를 참조하세요.  
  
 카디널리티 예상치에 유용한 밀도를 만들려면 쿼리 조건자의 열이 통계 개체 정의에 있는 열의 접두사 중 하나와 일치해야 합니다. 다음 예에서는 `LastName`, `MiddleName`, 및 `FirstName`열에 대한 여러 열 통계 개체를 만듭니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
 이 예에서 통계 개체 `LastFirst`는 열 접두사 `(LastName)`, `(LastName, MiddleName)` 및 `(LastName, MiddleName, FirstName)`에 대한 밀도를 가집니다. `(LastName, FirstName)`에 대한 밀도는 사용할 수 없습니다. 쿼리에서 `LastName` 을 사용하지 않고 `FirstName` 과 `MiddleName`을 사용하는 경우 카디널리티 예상치에 대한 밀도는 사용할 수 없습니다.  
  
### <a name="query-selects-from-a-subset-of-data"></a>쿼리가 데이터 하위 집합에서 선택하는 경우  
 쿼리 최적화 프로그램에서 단일 열 및 인덱스에 대한 통계를 만들 때 모든 행의 값에 대해 통계를 작성합니다. 쿼리가 행의 하위 집합에서 선택하고 행의 해당 하위 집합에서 데이터 분포가 고유한 경우 필터링된 통계는 쿼리 계획을 향상시킬 수 있습니다. CREATE STATISTICS 문을 WHERE 절과 함께 사용하여 필터링된 통계를 만들어 필터 조건자 식을 정의할 수 있습니다.  
  
 예를 들어 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]를 사용하면 `Production.Product` 테이블의 각 제품이 `Production.ProductCategory` 테이블의 4가지 범주인 Bikes, Components, Clothing 및 Accessories 중 하나에 속하게 됩니다. 각 범주의 데이터 배포는 서로 다른 가중치를 가집니다. 자전거 가중치는 13.77에서 30.0이고 구성 요소 가중치는 2.12에서 1050.00이면서 일부 NULL 값을 가지며 의류 가중치는 모두 NULL이고 액세서리 가중치 또한 NULL입니다.  
  
 자전거를 예로 사용할 때 모든 자전거 가중치에 대한 필터링된 통계는 쿼리 최적화 프로그램에 더욱 정확한 통계를 제공하므로 전체 테이블 통계 또는 Weight 열에 대한 존재하지 않는 통계에 비해 쿼리 계획의 품질을 향상할 수 있습니다. 자전거 가중치 열은 필터링된 통계의 경우에는 좋지만 가중치 조회 수가 상대적으로 적을 때 필터링된 인덱스의 경우에는 반드시 좋은 것은 아닙니다. 필터링된 인덱스에서 제공하는 조회 성능의 향상은 장점이지만 필터링된 인덱스를 데이터베이스에 추가하는 것으로 인한 추가 유지 관리 및 저장 비용은 부담이 될 수 있습니다.  
  
 다음 문에서는 Bikes의 모든 하위 범주에 대해 `BikeWeights` 로 필터링된 통계를 작성합니다. 필터링된 조건자 식에서는 `Production.ProductSubcategoryID IN (1,2,3)`비교를 통해 모든 자전거 하위 범주를 열거하는 방법으로 자전거를 정의합니다. Bikes 범주 이름은 Production.ProductCategory 테이블에 저장되고 필터 식의 모든 열은 동일한 테이블에 있어야 하므로 조건자에서 해당 이름을 사용할 수 없습니다.  
  
 [!code-sql[StatisticsDDL#FilteredStats2](../../relational-databases/statistics/codesnippet/tsql/statistics_1.sql)]  
  
 쿼리 최적화 프로그램은 `BikeWeights`로 필터링된 통계를 사용하여 `25`보다 가중치가 높은 모든 자전거를 선택하는 다음 쿼리의 쿼리 계획을 향상합니다.  
  
```tsql  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>쿼리에서 누락된 통계를 확인한 경우  
 오류 또는 기타 이벤트로 인해 쿼리 최적화 프로그램에서 통계를 작성하지 못하는 경우 쿼리 최적화 프로그램은 통계를 사용하지 않고 쿼리 계획을 만듭니다. 쿼리 최적화 프로그램은 통계가 누락된 것으로 표시하며 다음에 쿼리가 다시 실행될 때 통계를 다시 생성하려고 합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 쿼리 실행 계획을 그래픽으로 표시할 때 누락된 통계는 테이블 이름을 빨간 문자열로 나타내어 경고로 표시합니다. 또한 **를 사용하여** Missing Column Statistics [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 이벤트 클래스를 모니터링하면 통계가 누락되는 시기를 나타냅니다. 자세한 내용은 [오류 및 경고 이벤트 범주&#40;데이터베이스 엔진&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md)를 참조하세요.  
  
 통계가 누락된 경우 다음 단계를 수행하십시오.  
  
* AUTO_CREATE_STATISTICS 및 AUTO_UPDATE_STATISTICS가 ON으로 설정되었는지 확인합니다.  
  
* 데이터베이스가 읽기 전용이 아닌지 확인합니다. 데이터베이스가 읽기 전용이면 새 통계 개체를 저장할 수 없습니다.  
  
* CREATE STATISTICS 문을 사용하여 누락된 통계를 작성합니다.  
  
 읽기 전용 데이터베이스 또는 읽기 전용 스냅숏에 대한 통계가 없거나 유효하지 않을 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 **tempdb**에서 임시 통계를 만들어 유지 관리합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 임시 통계를 만드는 경우 통계 이름에 접미사 *_readonly_database_statistic*이 추가되므로 영구적 통계와 임시 통계를 구별할 수 있습니다. 접미사 *_readonly_database_statistic*은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 생성하는 통계용으로 예약되어 있습니다. 읽기/쓰기 데이터베이스에서 임시 통계에 대한 스크립트를 만들어 재현할 수 있습니다. 스크립팅된 경우 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]에서 통계 이름의 접미사를 *_readonly_database_statistic*에서 *_readonly_database_statistic_scripted*로 변경합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서만 임시 통계를 만들고 업데이트할 수 있습니다. 그러나 임시 통계를 삭제하고 통계 속성을 모니터링하는 데는 영구적 통계에 사용하는 것과 동일한 도구를 사용할 수 있습니다.  
  
* [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md) 문으로 작성된 통계에 적용됩니다.  
  
* **sys.stats** 및 **sys.stats_columns** 카탈로그 뷰를 사용하여 통계를 모니터링합니다. **sys_stats** 에는 영구적 통계와 임시 통계를 나타내는 **is_temporary** 열이 포함되어 있습니다.  
  
 임시 통계는 **tempdb**에 저장되므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 다시 시작하면 모든 임시 통계가 사라집니다.  
  
  
## <a name="UpdateStatistics"></a> 통계 업데이트 시기  
 쿼리 최적화 프로그램은 통계가 최신이 아닌 통계가 되는 시점을 확인한 다음, 쿼리 계획에 필요할 때 통계를 업데이트합니다. 경우에 따라 AUTO_UPDATE_STATISTICS를 ON으로 설정할 때보다 더 자주 통계를 업데이트하여 쿼리 계획을 향상시키고 쿼리 성능을 높일 수 있습니다. UPDATE STATISTICS 문 또는 저장 프로시저 sp_updatestats를 사용하여 통계를 업데이트할 수 있습니다.  
  
 통계를 업데이트하면 쿼리가 최신 통계로 컴파일되지만 쿼리도 다시 컴파일됩니다. 쿼리 계획 향상과 쿼리 재컴파일 소요 시간 간의 성능 균형을 유지해야 하므로 통계를 너무 자주 업데이트하지 않는 것이 좋습니다. 구체적인 성능 균형 유지의 정도는 응용 프로그램에 따라 달라집니다.  
  
 UPDATE STATISTICS 또는 sp_updatestats를 사용하여 통계를 업데이트할 때 AUTO_UPDATE_STATISTICS를 ON으로 유지하여 쿼리 최적화 프로그램에서 계속해서 정기적으로 통계를 업데이트하는 것이 좋습니다. 열, 인덱스, 테이블 또는 인덱싱된 뷰에 대한 통계를 업데이트하는 방법은 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)를 참조하세요. 데이터베이스의 모든 사용자 정의 테이블 및 내부 테이블에 대한 통계를 업데이트하는 방법은 저장 프로시저 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)를 참조하세요.  
  
 통계가 마지막으로 업데이트된 시점을 확인하려면 [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) 또는 [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md) 함수를 사용합니다.  
  
 다음과 같은 경우 통계를 업데이트할 것을 고려하십시오.  
  
* 쿼리 실행 시간이 느린 경우  
  
* 삽입 작업이 오름차순 또는 내림차순 키 열에 대해 발생하는 경우  
  
* 유지 관리 작업 이후  
  
### <a name="query-execution-times-are-slow"></a>쿼리 실행 시간이 느린 경우  
 쿼리 응답 시간이 느리거나 예측할 수 없는 경우 추가 문제 해결 단계를 수행하기 전에 쿼리에 최신 통계가 포함되었는지 확인하십시오.  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>삽입 작업이 오름차순 또는 내림차순 키 열에 대해 발생하는 경우  
 IDENTITY 또는 실시간 타임스탬프 열과 같은 오름차순 또는 내림차순 키 열에 대한 통계의 경우, 쿼리 최적화 프로그램이 수행하는 것보다 더 자주 통계를 업데이트해야 할 수도 있습니다. 삽입 작업에서는 새 값을 오름차순 또는 내림차순 열에 추가합니다. 추가된 행 수가 통계 업데이트를 트리거하기에는 너무 작을 수 있습니다. 통계가 최신 통계가 아니고 쿼리가 가장 최근에 추가된 행에서 선택하는 경우 현재 통계는 이러한 새 값에 대한 카디널리티 예상치를 포함하지 않습니다. 이로 인해 카디널리티 예상치가 부정확해지고 쿼리 성능이 저하될 수 있습니다.  
  
 예를 들어 가장 최근의 판매 주문 날짜에 대한 카디널리티 예상치를 포함하도록 통계가 업데이트되지 않은 경우 가장 최근의 판매 주문 날짜에서 선택하는 쿼리는 부정확한 카디널리티 예상치를 포함할 수 있습니다.  
  
### <a name="after-maintenance-operations"></a>유지 관리 작업 이후  
 테이블 삭제와 같이 데이터 분포를 변경하는 유지 관리 작업을 수행한 후 또는 많은 양의 행에 대한 대량 삽입을 수행한 후 통계를 업데이트하십시오. 이렇게 하면 이후에 쿼리에서 자동 통계 업데이트를 기다리는 동안 쿼리 처리에 지연이 생기는 것을 방지할 수 있습니다.  
  
 인덱스 다시 작성, 다시 구성, 조각 모음 등의 작업은 데이터 분포를 변경하지 않습니다. 따라서 ALTER INDEX REBUILD, DBCC REINDEX, DBCC INDEXDEFRAG 또는 ALTER INDEX REORGANIZE 작업을 수행한 후에는 통계를 업데이트할 필요가 없습니다. ALTER INDEX REBUILD 또는 DBCC DBREINDEX를 사용하여 테이블 또는 뷰에 대한 인덱스를 다시 작성하는 경우 쿼리 최적화 프로그램에서 통계를 업데이트하지만, 이 통계 업데이트는 인덱스를 다시 만드는 과정에서 생성됩니다. DBCC INDEXDEFRAG 또는 ALTER INDEX REORGANIZE 작업 이후에는 쿼리 최적화 프로그램에서 통계를 업데이트하지 않습니다. 
 
> [!TIP]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4부터 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) 또는 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)의 PERSIST_SAMPLE_PERCENT 옵션을 사용하여 샘플링 백분율을 명시적으로 지정하지 않는 후속 통계 업데이트에 대해 특정 샘플링 백분율을 설정하고 유지합니다.
  
##  <a name="DesignStatistics"></a> 통계를 효율적으로 사용하는 쿼리  
 쿼리 조건자에서 지역 변수, 복잡한 식 등의 일부 쿼리 구현은 만족스럽지 못한 쿼리 계획을 만들 수 있습니다. 이를 방지하려면 효율적인 통계 사용을 위한 쿼리 설계 지침을 따르는 것이 좋습니다. 쿼리 조건자에 대한 자세한 내용은 [검색 조건&#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md)을 참조하세요.  
  
 쿼리 조건자에 사용된 식, 변수 및 함수에 대한 *카디널리티 예상치* 정확도를 높이기 위해 효율적으로 통계를 사용하는 쿼리 설계 지침을 적용하여 쿼리 계획을 향상시킬 수 있습니다. 쿼리 최적화 프로그램에서 식, 변수 또는 함수 값을 알지 못하는 경우 히스토그램에서 조회할 값을 알 수 없으므로, 히스토그램에서 최상의 카디널리티 예상치를 검색할 수 없습니다. 대신 쿼리 최적화 프로그램은 히스토그램에서 샘플링된 모든 행에 대한 고유한 값마다 평균 행 수에 대한 카디널리티 예상치를 예측합니다. 이로 인해 카디널리티 예상치가 만족스럽지 못하고 쿼리 성능이 저하될 수 있습니다. 히스토그램에 대한 자세한 내용은 [sys.dm_db_stats_histogram](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)을 참조하세요.
  
 다음 지침에서는 카디널리티 예상치 정확도를 높여 쿼리 계획을 향상시킬 수 있도록 쿼리를 작성하는 방법에 대해 설명합니다.  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>식에 대한 카디널리티 예상치 정확도 향상  
식에 대한 카디널리티 예상치 정확도를 높이려면 다음 지침에 따르십시오.  
  
* 가능하면 상수가 포함된 단순한 식을 사용하십시오. 쿼리 최적화 프로그램에서는 카디널리티 예상치를 확인하기 전에 상수가 포함된 모든 함수와 식을 평가하지 않습니다. 예를 들어 `ABS(-100)` 식을 `100`으로 단순화합니다.  
  
* 식에서 여러 변수를 사용하는 경우 식에 대해 계산된 열을 만든 다음 계산된 열에 대해 통계 또는 인덱스를 만드십시오. 예를 들어 `WHERE PRICE + Tax > 100` 식에 대해 계산 열을 만드는 경우 쿼리 조건자 `Price + Tax`은 보다 정확한 카디널리티 예상치를 가질 수 있습니다.  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>변수 및 함수에 대한 카디널리티 예상치 정확도 향상  
변수 및 함수에 대한 카디널리티 예상치 정확도를 높이려면 다음 지침에 따르십시오.  
  
* 쿼리 조건자에서 지역 변수를 사용하는 경우 지역 변수 대신 매개 변수를 사용하여 쿼리를 다시 작성하십시오. 쿼리 최적화 프로그램에서 쿼리 실행 계획을 만들 때 지역 변수 값은 알 수 없습니다. 쿼리에서 매개 변수를 사용할 때 쿼리 최적화 프로그램은 저장 프로시저에 전달되는 첫 번째 실제 매개 변수 값에 대한 카디널리티 예상치를 사용합니다.  
  
* 다중 문 테이블 반환 함수(mstvf)의 결과를 저장하려면 표준 테이블 또는 임시 테이블을 사용합니다. 쿼리 최적화 프로그램은 다중 문 테이블 반환 함수에 대한 통계를 작성하지 않습니다. 이 방법을 사용하는 경우 쿼리 최적화 프로그램은 테이블 열에 대한 통계를 작성하고 이러한 통계를 사용하여 더욱 향상된 쿼리 계획을 만들 수 있습니다.  
  
* 테이블 변수 대신 표준 테이블 또는 임시 테이블을 사용하십시오. 쿼리 최적화 프로그램은 테이블 변수에 대한 통계를 작성하지 않습니다. 이 방법을 사용하는 경우 쿼리 최적화 프로그램은 테이블 열에 대한 통계를 작성하고 이러한 통계를 사용하여 더욱 향상된 쿼리 계획을 만들 수 있습니다. 임시 테이블 사용과 테이블 변수 사용에는 각각 장단점이 있습니다. 저장 프로시저에 테이블 변수를 사용하면 임시 테이블에 비해 저장 프로시저를 다시 컴파일하는 횟수가 줄어듭니다. 응용 프로그램에 따라 테이블 변수 대신 임시 테이블을 사용하면 성능이 향상되지 않을 수도 있습니다.  
  
* 이미 전달된 매개 변수를 사용하는 쿼리가 저장 프로시저에 포함되어 있는 경우 쿼리에서 매개 변수 값을 사용하기 전에 저장 프로시저 내의 매개 변수 값을 변경하지 마십시오. 쿼리에 대한 카디널리티 예상치는 업데이트된 값이 아닌 이미 전달된 매개 변수 값을 기준으로 합니다. 매개 변수 값이 변경되지 않도록 두 개의 저장 프로시저를 사용하여 쿼리를 다시 작성할 수 있습니다.  
  
     예를 들어 `@date`가 NULL인 경우 다음 `Sales.GetRecentSales` 저장 프로시저에서는 `@date` 매개 변수의 값을 변경합니다.  
  
    ```tsql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date IS NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     `Sales.GetRecentSales` 저장 프로시저에 대한 첫 번째 호출에서 NULL을 `@date` 매개 변수에 전달하면 쿼리 조건자가 `@date = NULL`과 함께 호출되지 않은 경우에도 쿼리 최적화 프로그램에서 `@date = NULL`에 대한 카디널리티 예상치와 함께 저장 프로시저를 컴파일합니다. 실제 쿼리 결과에서 이 카디널리티 예상치는 행 수와 많이 다를 수 있습니다. 그 결과 쿼리 최적화 프로그램에서 만족스럽지 못한 쿼리 계획을 선택할 수 있습니다. 이를 방지하기 위해 다음과 같이 저장 프로시저를 두 개의 프로시저로 다시 작성할 수 있습니다.  
  
    ```tsql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>쿼리 힌트를 사용하여 카디널리티 예상치 정확도 향상  
 지역 변수에 대한 카디널리티 예상치 정확도를 높이기 위해 RECOMPILE과 함께 `OPTIMIZE FOR <value>` 또는 `OPTIMIZE FOR UNKNOWN` 쿼리 힌트를 사용할 수 있습니다. 자세한 내용은 [쿼리 힌트&#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)를 참조하세요.  
  
 일부 응용 프로그램의 경우 쿼리를 실행할 때마다 다시 컴파일하는 데 너무 많은 시간이 걸릴 수 있습니다. `RECOMPILE` 옵션을 사용하지 않는 경우에도 `OPTIMIZE FOR` 쿼리 힌트가 도움이 될 수 있습니다. 예를 들어 특정 날짜를 지정하기 위해 `OPTIMIZE FOR` 옵션을 Sales.GetRecentSales 저장 프로시저에 추가할 수 있습니다. 다음 예에서는 `OPTIMIZE FOR` 옵션을 Sales.GetRecentSales 프로시저에 추가합니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>계획 지침을 사용하여 카디널리티 예상치 정확도 향상  
 일부 응용 프로그램의 경우 쿼리를 변경할 수 없거나 RECOMPILE 쿼리 힌트 사용으로 인해 너무 많은 컴파일이 필요해서 통계 설계 지침이 적용되지 않을 수 있습니다. 응용 프로그램 공급업체와 함께 응용 프로그램 변경 내용을 조사하는 동안 쿼리 동작을 제어할 수 있도록 계획 지침을 사용하여 USE PLAN과 같은 기타 힌트를 지정할 수 있습니다. 계획 지침에 대한 자세한 내용은 [Plan Guides](../../relational-databases/performance/plan-guides.md)를 참조하십시오.  
  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [UPDATE STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DROP STATISTICS&#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [필터링된 인덱스 만들기](../../relational-databases/indexes/create-filtered-indexes.md)   
 [SQL Server의 Autostat(AUTO_UPDATE_STATISTICS) 동작 제어](http://support.microsoft.com/help/2754171)
  
 

