---
title: 자동 통계
description: 분석 플랫폼 시스템 AU7에 도입 된 자동 통계 기능을 설명 합니다.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
monikerRange: '>= aps-pdw-2016-au7 || = sqlallproducts-allversions'
ms.openlocfilehash: 7071c9cb46bde6e2d353293cec9f01451c0b4f67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401281"
---
# <a name="configure-auto-statistics"></a>자동 통계 구성

통계를 자동으로 만들고 업데이트 하기 위해 자동 통계를 사용 하도록 병렬 데이터 웨어하우스를 구성 하는 방법에 대해 알아봅니다.  이 기능을 사용 하 여 쿼리 계획을 향상 시킬 수 있으므로 쿼리 성능이 향상 됩니다.

**적용 대상:** APS (2016-AU7로 시작)

## <a name="what-are-statistics"></a>통계 란?
쿼리 최적화에 대 한 통계는 하나 이상의 테이블 열에 있는 값의 분포에 대 한 통계 정보를 포함 하는 개체입니다. 쿼리 최적화 프로그램은 이러한 통계를 사용하여 쿼리 결과에서 카디널리티 또는 행 수를 계산합니다. 쿼리 최적화 프로그램은 이러한 카디널리티 예상치를 통해 고품질의 쿼리 계획을 만듭니다. 예를 들어 APS에서 MPP 쿼리 최적화 프로그램은 카디널리티 예상치를 사용 하 여 조인 절에 사용 되는 두 테이블 중 작은 것을 순서 대로 또는 복제 하 여 쿼리 성능을 향상 시 키도 록 선택 합니다.  자세한 내용은 [Statistics](../relational-databases/statistics/statistics.md) and [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) 를 참조 하세요.

## <a name="what-are-auto-statistics"></a>자동 통계 란?
자동 통계는 쿼리 최적화 프로그램이 자동으로 만들고 업데이트 하 여 쿼리 계획을 향상 시키는 통계입니다. 통계는 로드, 삽입, 업데이트 및 삭제 작업 후에 만료 될 수 있습니다. 자동 통계를 사용 하지 않을 경우 통계를 업데이트할 열과 통계를 업데이트 해야 하는 시간을 이해 하기 위해 고유한 분석을 수행 해야 합니다.

자동 통계는 다음 세 가지 설정을 포함 합니다. 

### <a name="auto_create_statistics"></a>AUTO_CREATE_STATISTICS
자동 통계 작성 옵션인 AUTO_CREATE_STATISTICS가 ON으로 설정된 경우 쿼리 최적화 프로그램은 필요에 따라 쿼리 조건자의 개별 열에 대한 통계를 작성하므로 쿼리 계획에 대한 카디널리티 예상치의 정확도가 높아집니다. 이러한 단일 열 통계는 기존 통계 개체에 히스토그램이 없는 열에 대해 작성됩니다.

### <a name="auto_update_statistics"></a>AUTO_UPDATE_STATISTICS 
자동 통계 업데이트 옵션 AUTO_UPDATE_STATISTICS가 ON으로 설정되면 쿼리 최적화 프로그램은 통계가 최신이 아닌 통계가 되는 시점을 확인한 다음 쿼리에서 사용될 때 이를 업데이트합니다. 작업 삽입, 업데이트, 삭제 또는 병합을 통해 테이블이나 인덱싱된 뷰의 데이터 분포가 변경되면 통계 내용이 더 이상 최신이 아니게 됩니다. 쿼리 최적화 프로그램은 마지막 통계 업데이트 이후 데이터 수정 개수를 계산한 다음 이 수를 임계값과 비교하여 통계가 최신이 아니게 된 시점을 결정합니다. 임계값은 테이블 또는 인덱싱된 뷰의 행 수를 기준으로 합니다.

### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC
비동기 통계 업데이트 옵션인 AUTO_UPDATE_STATISTICS_ASYNC는 쿼리 최적화 프로그램이 동기 또는 비동기 통계 업데이트를 사용하는지를 결정합니다. APS의 경우 비동기 통계 업데이트 옵션은 기본적으로 설정 되어 있으며 쿼리 최적화 프로그램은 통계를 비동기식으로 업데이트 합니다. AUTO_UPDATE_STATISTICS_ASYNC 옵션은 인덱스에 대해 작성된 통계 개체, 쿼리 조건자의 단일 열 및 CREATE STATISTICS 문으로 작성된 통계에 적용됩니다.

## <a name="configuration-settings-for-system-administrators"></a>시스템 관리자에 대 한 구성 설정
APS AU7로 업그레이드 한 후에는 자동 통계가 기본적으로 사용 하도록 설정 됩니다. 시스템 관리자는 어플라이언스 Configuration Manager의 [기능 스위치](appliance-feature-switch.md) 옵션을 사용 하 여 자동 통계를 사용 하거나 사용 하지 않도록 설정할 수 있습니다.  사용 하도록 설정 하면 사용자가 데이터베이스당 통계 설정을 변경할 수 있습니다.
기능 스위치 값을 변경 하려면 AP에서 서비스를 다시 시작 해야 합니다.

## <a name="change-auto-statistics-settings-on-a-database"></a>데이터베이스에서 자동 통계 설정 변경
시스템 관리자가 자동 통계를 사용 하도록 설정한 경우 [ALTER database (병렬 데이터 웨어하우스)](../t-sql/statements/alter-database-transact-sql.md?tabs=sqlpdw) 를 사용 하 여 데이터베이스에 대 한 통계 설정을 변경할 수 있습니다. 시스템 관리자가 자동 통계 기능 스위치를 사용 하도록 설정한 경우 AU7로 업그레이드 한 후 생성 된 모든 새 데이터베이스는 자동 통계를 사용 하도록 설정 됩니다. AU7로 업그레이드 하기 전에 있던 모든 데이터베이스는 자동 통계를 사용할 수 없습니다. 다음 예에서는 기존 데이터베이스 myPDW에 대 한 자동 통계를 사용 하도록 설정 합니다.

```sql
ALTER DATABASE myPDW SET AUTO_CREATE_STATISTICS ON
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS ON 
ALTER DATABASE myPDW SET AUTO_UPDATE_STATISTICS_ASYNC ON
```
 
AUTO_UPDATE STATISTICS_ASYNC 옵션은 AUTO_UPDATE_STATISTICS가 설정 된 경우에만 작동 합니다.  따라서 AUTO_UPDATE_STATISTICS OFF이 고 AUTO_UPDATE_STATISTICS_ASYNC ON 이면 통계가 업데이트 되지 않습니다. 

### <a name="error-messages"></a>오류 메시지
"이 옵션은 PDW에서 지원 되지 않습니다." 라는 오류 메시지가 표시 될 수 있습니다.  이 오류는 시스템 관리자가 자동 통계를 사용 하도록 설정 하지 않은 상태에서 ALTER DATABASE의 auto statistics 옵션을 설정 하려고 할 때 발생 합니다. 

### <a name="limitations-and-restrictions"></a>제한 사항
자동 통계는 외부 테이블에서 작동 하지 않습니다. 

### <a name="check-the-current-values"></a>현재 값 확인
다음 쿼리는 모든 데이터베이스에 대 한 자동 통계 설정의 현재 값을 반환 합니다.

```sql
SELECT NAME
    , IS_AUTO_CREATE_STATS_ON 
    , IS_AUTO_UPDATE_STATS_ON
    , IS_AUTO_UPDATE_STATS_ASYNC_ON
FROM
    sys.databases;
```

반환 값이 1 이면 설정이 on이 고 0은 설정이 off 임을 의미 합니다. 

## <a name="next-steps"></a>다음 단계
쿼리를 수행 하는 방법을 보려면 [활성 쿼리 모니터링](monitoring-active-queries.md) 을 참조 하세요.
