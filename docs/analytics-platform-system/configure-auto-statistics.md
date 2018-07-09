---
title: 자동 통계 (분석 플랫폼 시스템)
description: 분석 플랫폼 시스템 AU7에 도입 된 자동 통계 기능을 설명 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 000a31f76118a3f2acaf702ce5c74c1dd5703422
ms.sourcegitcommit: 3e5f1545e5c6c92fa32e116ee3bff1018ca946a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37107141"
---
# <a name="configure-auto-statistics"></a>자동 통계 다시 계산 구성

만들고 자동으로 통계를 업데이트 하기 위한 자동 통계를 사용 하는 병렬 데이터 웨어하우스를 구성 하는 방법에 알아봅니다.  이 기능을 사용 하면 쿼리 계획을 향상 하 고 쿼리 성능을.

**적용 대상:** AP (2016 AU7부터 시작)

## <a name="what-are-statistics"></a>통계란 무엇입니까?
쿼리 최적화 통계는 테이블의 하나 이상의 열에서 값의 분포에 대 한 통계 정보를 포함 하는 개체입니다. 쿼리 최적화 프로그램은 이러한 통계를 사용 하 여 카디널리티를 추정 또는 쿼리에서 행 개수 결과입니다. 이러한 카디널리티 예상치는 쿼리 최적화 프로그램은 고품질 쿼리 계획을 만들려면 사용 합니다. 예를 들어, AP에서 순서 섞기 또는 이렇게 및 join 절에 사용 되는 두 테이블 중 더 작은 숫자를 복제 하도록 선택할 카디널리티 예상치 MPP 쿼리 최적화 프로그램에서는 쿼리 성능이 향상 됩니다.  자세한 내용은 [통계](../relational-databases/statistics/statistics.md) 고 [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)

## <a name="what-are-auto-statistics"></a>자동 통계란 무엇입니까?
자동 통계는 통계는 쿼리 최적화 프로그램을 만들어이 쿼리 계획을 개선 하는 자동으로 업데이트 합니다. 통계 로드 후에 만료 될 수 있습니다, 삽입, 업데이트 및 삭제 작업을 수행 합니다. 자동 통계가 없는 열 필요한 통계 및 통계를 업데이트 해야 하는 경우를 이해 하려면 고유한 분석을 수행 해야 합니다.

자동 통계에는 다음 세 가지 설정이 포함 됩니다. 

### <a name="autocreatestatistics"></a>AUTO_CREATE_STATISTICS
자동 통계 작성 옵션, AUTO_CREATE_STATISTICS가 ON 경우 쿼리 최적화 프로그램이 쿼리 계획에 대 한 카디널리티 예상치 정확도 높이려면 필요에 따라 쿼리 조건자의 개별 열에 통계를 만듭니다. 이러한 단일 열 통계는 기존 통계 개체에 히스토그램이 없는 열에 대해 작성됩니다.

### <a name="autoupdatestatistics"></a>AUTO_UPDATE_STATISTICS 
자동 통계 업데이트 옵션 AUTO_UPDATE_STATISTICS가 ON으로 설정되면 쿼리 최적화 프로그램은 통계가 최신이 아닌 통계가 되는 시점을 확인한 다음 쿼리에서 사용될 때 이를 업데이트합니다. 작업 삽입, 업데이트, 삭제 또는 병합을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

### <a name="autoupdatestatisticsasync"></a>AUTO_UPDATE_STATISTICS_ASYNC
비동기 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS_ASYNC는 쿼리 최적화 프로그램이 동기 또는 비동기 통계 업데이트를 사용하는지를 결정합니다. AP에 대 한 비동기 통계 업데이트 옵션을 기본적으로 켜져 및 쿼리 최적화 프로그램 통계를 비동기적으로 업데이트 합니다. AUTO_UPDATE_STATISTICS_ASYNC 옵션은 인덱스에 대해 작성된 통계 개체, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문으로 작성된 통계에 적용됩니다.

## <a name="configuration-settings-for-system-administrators"></a>시스템 관리자에 대 한 구성 설정
AP AU7로 업그레이드 한 후 자동 통계 기능을 기본적으로 설정 됩니다. 시스템 관리자가 사용 하 여 자동 통계를 사용할지 수는 [기능 스위치가](appliance-feature-switch.md) 어플라이언스 Configuration Manager의 옵션입니다.  사용 하도록 설정 하면 데이터베이스 별로 통계 설정을 변경할 수 있습니다.
기능 스위치 값을 변경 AP에 서비스를 다시 시작을 해야 합니다.

## <a name="change-auto-statistics-settings-on-a-database"></a>데이터베이스에서 자동 통계 설정 변경
자동 통계 다시 계산을 시스템 관리자가 사용 하는 경우 사용할 수 [ALTER DATABASE (병렬 데이터 웨어하우스)](/sql/t-sql/statements/alter-database-parallel-data-warehouse) 데이터베이스에서 통계 설정을 변경할 수 있습니다. 자동 통계 기능 스위치를 시스템 관리자가 사용 하는 경우 AU7로 업그레이드 한 후에 만들어진 새 데이터베이스는 자동 통계 사용 하도록 설정 해야 합니다. AU7로 업그레이드 하기 전에 있던 모든 데이터베이스에는 자동 통계 사용 하지 않도록 설정 합니다. 다음 예제에서는 기존 데이터베이스 myPDW에 대 한 자동 통계.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
AUTO_UPDATE STATISTICS_ASYNC 옵션 AUTO_UPDATE_STATISTICS가 ON입니다. 경우에 작동 합니다.  따라서 통계 업데이트 되지 않습니다 AUTO_UPDATE_STATISTICS가 OFF 및 AUTO_UPDATE_STATISTICS_ASYNC가 ON입니다. 

### <a name="error-messages"></a>오류 메시지
"이이 옵션은 PDW에서 지원 되지 않습니다" 오류 메시지가 나타날 수 있습니다.  이 오류는 시스템 관리자가 자동 통계를 활성화 하지에서 ALTER DATABASE의 자동 통계 옵션을 설정 하려고 할 때 발생 합니다. 

### <a name="limitations-and-restrictions"></a>제한 사항
자동 통계는 외부 테이블에는 작동 하지 않습니다. 

### <a name="check-the-current-values"></a>현재 값을 확인
다음 쿼리는 모든 데이터베이스에 대해 자동 통계 설정의 현재 값을 반환합니다.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

반환 값이 1 이면 설정에 켜져이 고 0 이면 설정은 해제 되어 있습니다. 

## <a name="next-steps"></a>다음 단계
쿼리를 수행 하는 방법을 참조 하세요 [활성 쿼리 모니터링](monitoring-active-queries.md)
