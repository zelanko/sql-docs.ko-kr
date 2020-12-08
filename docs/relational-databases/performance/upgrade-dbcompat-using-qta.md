---
title: 쿼리 튜닝 길잡이를 사용하여 데이터베이스 업그레이드
description: 쿼리 튜닝 길잡이는 SQL Server의 최신 버전으로 업그레이드하는 동안 성능 안정성을 유지하기 위해 사용자에게 권장된 워크플로를 안내합니다.
ms.custom: seo-dt-2019
ms.date: 02/13/2019
ms.prod: sql
ms.reviewer: wiassaf
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.querytuning.f1
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
- query profiling
- lightweight query profiling
- lightweight profiling
ms.assetid: 07f8f594-75b4-4591-8c29-d63811e7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 31cdd59e519437f679cd738ef1dc959919b86667
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504937"
---
# <a name="upgrading-databases-by-using-the-query-tuning-assistant"></a>쿼리 튜닝 길잡이를 사용하여 데이터베이스 업그레이드

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 이상 버전으로 마이그레이션할 때, 그리고 사용 가능한 최신 상태로 [데이터베이스 호환성 수준을 업그레이드](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)할 때는 워크로드가 성능 저하 위험에 노출될 수 있습니다. 또한 이는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]와 최신 버전 간에 업그레이드하는 경우에도 발생할 수 있습니다.

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]부터 새 버전을 사용할 때마다 쿼리 최적화 프로그램의 모든 변경 내용이 최신 데이터베이스 호환성 수준에 연결되므로 실행 계획이 업그레이드 시점에 즉시 변경되지 않고 사용자가 `COMPATIBILITY_LEVEL` 데이터베이스 옵션을 최신 상태로 변경할 때 변경됩니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에 도입된 쿼리 최적화 프로그램 변경 사항에 대한 자세한 내용은 [카디널리티 평가기](../../relational-databases/performance/cardinality-estimation-sql-server.md)를 참조하세요. 호환성 수준 및 업그레이드에 미치는 영향에 대한 자세한 내용은 [호환성 수준 및 데이터베이스 엔진 업그레이드](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)를 참조하세요.

데이터베이스 호환성 수준에서 제공되는 이 제한 기능은 쿼리 저장소와 함께 업그레이드가 아래에 나와 있는 권장 워크플로를 따를 경우 업그레이드 프로세스의 쿼리 성능에 대한 상당한 수준의 제어를 제공합니다. 호환성 수준 업그레이드를 위해 권장되는 워크플로에 대한 자세한 내용은 [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)을 참조하세요. 

![쿼리 저장소를 사용한 권장되는 데이터베이스 업그레이드 워크플로](../../relational-databases/performance/media/query-store-usage-5.png "쿼리 저장소를 사용한 권장되는 데이터베이스 업그레이드 워크플로") 

이 업그레이드에 대한 제어는 [자동 튜닝](../../relational-databases/automatic-tuning/automatic-tuning.md)이 도입된 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]를 통해 더 개선되었으며, 위에 나온 권장되는 워크플로의 마지막 단계를 자동화할 수 있습니다.

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18부터 새로운 [쿼리 저장소 사용 시나리오](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)의 *SQL Server의 최신 버전으로 업그레이드하는 동안 성능 안정성 유지* 섹션에 설명된 대로 새로운 **QTA(쿼리 튜닝 길잡이)** 기능은 최신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전으로 업그레이드하는 동안 성능 안정성을 유지하기 위해 사용자에게 권장되는 워크플로를 안내합니다. 그러나 QTA는 권장 워크플로의 마지막 단계에 나와 있는 대로 이전에 알려진 좋은 계획으로 롤백되지 않습니다. 대신에, QTA는 [쿼리 저장소 **회귀된 쿼리**](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed) 보기에 있는 회귀를 추적하고 새롭고 더 나은 계획을 생성할 수 있도록 적용 가능한 최적화 모델 변형의 가능한 순열을 반복합니다.

> [!IMPORTANT]
> QTA는 사용자 워크로드를 생성하지 않습니다. 애플리케이션에서 사용되지 않는 환경에서 QTA를 실행하는 경우 대상 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 다른 방법으로 대표 테스트 워크로드를 계속 실행할 수 있는지 확인합니다.

## <a name="the-query-tuning-assistant-workflow"></a>쿼리 튜닝 길잡이 워크플로

QTA를 시작할 때 이전 버전 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스가 [CREATE DATABASE ... FOR ATTACH](../..//relational-databases/databases/attach-a-database.md) 또는 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)를 통해 최신 버전의 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]로 이동되었으며 업그레이드하기 전에 데이터베이스 호환성 수준이 즉시 변경되지 않는다고 가정합니다. QTA는 다음 단계를 안내합니다.

1. 사용자가 설정한 워크로드 기간(일)에 대한 권장된 설정에 따라 쿼리 저장소를 구성합니다. 일반적인 비즈니스 주기에 맞는 워크로드 기간을 고려합니다.
2. 필요한 워크로드 시작을 요청하여 해당 쿼리 저장소가 워크로드 데이터의 기준을 수집할 수 있도록 합니다(아직 사용할 수 없는 경우).
3. 사용자가 선택한 대상 데이터베이스 호환성 수준으로 업그레이드합니다.
4. 비교 및 회귀 탐지를 위해 워크로드 데이터의 두 번째 전달을 수집할 것을 요청합니다.
5. [쿼리 저장소 **회귀된 쿼리**](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed) 보기에 따라 검색된 모든 회귀를 반복하고, 적용 가능한 최적화 도구 모델 변형에 대한 가능한 영구 구성에서 런타임 통계를 수집하여 검사하고, 결과를 측정합니다. 
6. 측정된 개선 사항에 대해 보고하고 선택적으로 [계획 지침](../../relational-databases/performance/plan-guides.md)을 사용하여 이러한 변경 사항을 지속하도록 허용합니다.

데이터베이스 연결에 대한 자세한 내용은 [데이터베이스 분리 및 연결](../../relational-databases/databases/database-detach-and-attach-sql-server.md#AttachDb)을 참조하세요.

아래에서 QTA가 위에 나온 쿼리 저장소를 사용하여 호환성 수준을 업그레이드하기 위해 권장되는 워크플로의 마지막 단계만 변경하는 방법을 참조하세요. QTA는 현재 미숙한 실행 계획과 마지막으로 알려진 우수 실행 계획 중에서 선택할 수 있는 옵션을 갖는 대신, 선택된 회귀된 쿼리에 특정한 조정 옵션을 제공하여 조정된 실행 계획으로 새로 개선된 상태를 만듭니다.

![QTA를 사용한 권장되는 데이터베이스 업그레이드 워크플로](../../relational-databases/performance/media/qta-usage.png "QTA를 사용한 권장되는 데이터베이스 업그레이드 워크플로")

### <a name="qta-tuning-internal-search-space"></a>QTA 튜닝 내부 검색 공간

QTA는 쿼리 저장소에서 실행할 수 있는 `SELECT` 쿼리만 대상으로 지정합니다. 컴파일된 매개 변수를 알고 있는 경우 매개 변수가 있는 쿼리가 적합합니다. 임시 테이블 또는 테이블 변수와 같은 런타임 구문에 의존하는 쿼리는 현재 적합하지 않습니다.

QTA는 [CE(카디널리티 평가기)](../../relational-databases/performance/cardinality-estimation-sql-server.md) 버전의 변경으로 인해 쿼리 회귀의 알려진 가능한 패턴을 대상으로 지정합니다. 예를 들어, 데이터베이스를 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 및 데이터베이스 호환성 수준 110에서 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] 및 데이터베이스 호환성 수준 140으로 업그레이드하는 경우 특별히 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 존재하는 CE 버전(CE 70)으로 작업하도록 설계되었으므로 일부 쿼리가 회귀될 수 있습니다. CE 140에서 CE 70으로 회귀하는 것이 유일한 옵션이라는 뜻은 아닙니다. 최신 버전의 특정 변경 사항만 회귀에 도입하는 경우 쿼리가 새로운 CE 버전의 모든 개선 사항을 활용하는 동시에, 특정 쿼리에 더 잘 작동했던 이전 CE 버전의 관련 부분만 사용한다는 점을 의미할 수 있습니다. 또한 새로운 CE 개선 사항의 혜택을 누리도록 회귀되지 않은 워크로드의 다른 쿼리도 허용합니다.

QTA에서 검색된 CE 패턴은 다음과 같습니다.

- **독립성 대 상관 관계**: 독립성 가정이 특정 쿼리에 대해 더 나은 예상치를 제공하는 경우 쿼리 힌트 `USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES')`로 인해 상관 관계를 설명하는 필터에 `AND` 조건자를 예상할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 최소 선택을 사용하여 실행 계획을 생성합니다. 자세한 내용은 [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint) 및 [CE의 버전](../../relational-databases/performance/cardinality-estimation-sql-server.md#versions-of-the-ce)을 참조하세요.
- **단순 포함 대 기본 포함**: 다른 조인 포함이 특정 쿼리에 대해 더 나은 예상치를 제공하는 경우 쿼리 힌트 `USE HINT ('ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS')`로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 기본값인 기본 포함 가정 대신 단순 포함 가정을 사용하여 실행 계획을 생성합니다. 자세한 내용은 [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint) 및 [CE의 버전](../../relational-databases/performance/cardinality-estimation-sql-server.md#versions-of-the-ce)을 참조하세요.
- **MSTVF(다중 명령문 테이블 반환 함수) 고정 카디널리티 추정** 100개 행 대 1개 행: 100개 행의 TVF에 대한 기본 고정 예상치가 1개 행([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 및 이전 버전의 쿼리 최적화 CE 모델 아래의 기본값에 해당)의 TVF에 대한 고정 예상치를 사용하는 것에 비해 더 효율적인 계획으로 이어지지 않는 경우 실행 계획을 생성하는 데 쿼리 힌트 `QUERYTRACEON 9488`이 사용됩니다. MSTVF에 대한 자세한 내용은 [사용자 정의 함수 만들기(데이터베이스 엔진)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)를 참조하세요.

> [!NOTE]
> 마지막 수단으로, 좁은 범위의 힌트가 적합한 쿼리 패턴에 대해 충분한 결과를 산출하지 못하는 경우 쿼리 힌트 `USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')`을 사용하여 실행 계획을 생성하는 방법으로 CE 70의 전체 사용도 고려합니다.

> [!IMPORTANT]
> 어느 힌트든 향후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트에서 해결될 수도 있는 특정 동작을 강제로 적용합니다. 다른 옵션이 없고 모든 새 업그레이드를 사용하여 힌트 코드를 다시 확인하려는 경우에만 힌트를 적용하는 것이 좋습니다. 동작을 강제로 적용하면 워크로드가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 새로운 버전에 도입된 개선 사항의 이점을 활용하지 못할 수도 있습니다.

## <a name="starting-query-tuning-assistant-for-database-upgrades"></a>데이터베이스 업그레이드를 위한 쿼리 튜닝 길잡이 시작

QTA는 세션이 처음으로 만들어진 사용자 데이터베이스의 `msqta` 스키마에 세션 상태를 저장하는 세션 기반 기능입니다. 시간이 지남에 따라 단일 데이터베이스에 여러 튜닝 세션이 생성될 수 있으나, 지정된 데이터베이스에 대한 활성 세션은 단 하나만 존재할 수 있습니다.

### <a name="creating-a-database-upgrade-session"></a>데이터베이스 업그레이드 세션 만들기

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.

2. 데이터베이스 호환성 수준을 업그레이드하려는 데이터베이스의 경우 데이터베이스 이름을 마우스 오른쪽 단추로 선택하고, **작업** 을 선택하고, **데이터베이스 업그레이드** 를 선택한 후, **새 데이터베이스 업그레이드 세션** 을 선택합니다.

3. QTA 마법사 창에서 세션을 구성하려면 다음과 같은 두 단계가 필요합니다.

    1. **설치** 창에서 분석 및 조정할 전체 비즈니스 주기 하나에 해당하는 워크로드 데이터를 캡처하도록 쿼리 저장소를 구성합니다.
        - 예상되는 워크로드 기간을 일 단위로 입력합니다(최솟값은 1일). 이는 전체 기준을 임시로 수집할 수 있도록 허용하는 권장되는 쿼리 저장소 설정을 제안하는 데 사용됩니다. 데이터베이스 호환성 수준을 변경한 후 발견된 모든 회귀된 쿼리가 분석될 수 있도록 하려면 적합한 기준을 캡처하는 것이 중요합니다. 
        - QTA 워크플로가 완료된 후 사용자 데이터베이스가 있어야 하는 대상 데이터베이스 호환성 수준을 설정합니다.
        완료되면 **다음** 을 선택합니다.

       ![새 데이터베이스 업그레이드 세션 설정 창](../../relational-databases/performance/media/qta-new-session-setup.png "새 데이터베이스 업그레이드 설정 창")  
  
    2. **설정** 창에서 두 개의 열에는 대상 데이터베이스에 있는 쿼리 저장소의 **현재** 상태가 **권장** 설정과 함께 표시됩니다. 
        - 권장 설정은 기본적으로 선택되어 있지만, 현재 열 위에 있는 라디오 단추를 선택하면 현재 설정이 수락되며, 현재 쿼리 저장소 구성을 미세 조정할 수도 있습니다.
        - 제안된 *부실 쿼리 임계값* 설정은 예상되는 워크로드 기간(일)의 두 배입니다. 쿼리 저장소가 기준 워크로드 및 데이터베이스 업그레이드 후 워크로드에 대한 정보를 유지해야 하기 때문입니다.
        완료되면 **다음** 을 선택합니다.

       ![새 데이터베이스 업그레이드 설정 창](../../relational-databases/performance/media/qta-new-session-settings.png "새 데이터베이스 업그레이드 설정 창")

       > [!IMPORTANT]
       > 제안된 *최대 크기* 는 짧은 시간 워크로드에 적합할 수 있는 임의의 값입니다.
       > 그러나 매우 집약적인 워크로드, 즉 여러 다른 계획이 생성되는 경우 기준 및 데이터베이스 업그레이드 후 워크로드에 대한 정보를 유지하는 것은 부족할 수 있다는 점을 염두에 두십시오.
       > 이러한 상황이 예상되는 경우에는 적절한 더 높은 값을 입력합니다.

4. **튜닝** 창에서 세션 구성이 완료되며, 세션을 열고 계속하기 위한 다음 단계가 안내됩니다. 완료되면 **마침** 을 선택합니다.

    ![새 데이터베이스 업그레이드 튜닝 창](../../relational-databases/performance/media/qta-new-session-tuning.png "새 데이터베이스 업그레이드 튜닝 창")

> [!NOTE]
> 가능한 대체 시나리오는 데이터베이스가 이미 권장 데이터베이스 호환성 업그레이드 워크플로를 거쳤던 프로덕션 서버에서 테스트 서버로 데이터베이스 백업을 복원하는 것으로 시작됩니다.

### <a name="executing-the-database-upgrade-workflow"></a>데이터베이스 업그레이드 워크플로 실행

1. 데이터베이스 호환성 수준을 업그레이드하려는 데이터베이스의 경우 데이터베이스 이름을 마우스 오른쪽 단추로 선택하고, **작업** 을 선택하고, **데이터베이스 업그레이드** 를 선택한 후, **세션 모니터링** 을 선택합니다.

2. **세션 관리** 페이지에는 해당 범위의 데이터베이스에 대한 현재 및 과거 세션이 나열됩니다. 원하는 세션을 선택하고 **세부 정보** 를 선택합니다.

    > [!NOTE]
    > 현재 세션이 표시되지 않았으면 **새로 고침** 단추를 선택합니다.

    목록에는 다음과 같은 정보가 포함됩니다.
    - **세션 ID**
    - **세션 이름**: 데이터베이스 이름, 세션을 만든 날짜 및 시간으로 구성된 시스템에서 생성된 이름입니다.
    - **상태**: 세션의 상태입니다(활성 또는 닫힘).
    - **설명**: 사용자가 선택한 대상 데이터베이스 호환성 수준 및 비즈니스 주기 워크로드에 대한 일 수로 구성된 시스템에서 생성된 항목입니다.
    - **시작 시간**: 세션이 만들어진 날짜와 시간입니다.

    ![QTA 세션 관리 페이지](../../relational-databases/performance/media/qta-session-management.png "QTA 세션 관리 페이지")

    > [!NOTE]
    > **세션 삭제** 는 선택한 세션에 대해 저장된 데이터를 삭제합니다.
    > 단, 닫힌 세션을 삭제해도 이전에 배포된 계획 지침은 삭제되지 **않습니다**.
    > 배포된 계획 지침이 있는 세션을 삭제하는 경우 QTA를 사용하여 롤백할 수 없습니다.
    > 대신 [sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) 시스템 테이블을 사용하여 계획 지침을 검색하고 [sp_control_plan_guide](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)를 사용하여 수동으로 삭제합니다.
  
3. 새 세션에 대한 진입점은 **데이터 컬렉션** 단계입니다.

    > [!NOTE]
    > **세션** 단추는 활성 세션을 유지한 채 **세션 관리** 페이지로 돌아갑니다.

    이 단계에는 세 개의 하위 단계에 있습니다.

    1. **기준 데이터 수집** 은 쿼리 저장소가 기준을 수집할 수 있도록 대표적인 워크로드 주기를 실행할 것을 사용자에게 요청합니다. 워크로드가 완료되면 **워크로드 실행 완료** 를 선택하고 **다음** 을 선택합니다.

        > [!NOTE]
        > 워크로드를 실행하는 동안 QTA 창을 닫을 수 있습니다. 나중에 활성 상태로 유지되어 있는 세션으로 돌아가면 세션이 중단되었던 동일한 단계부터 다시 시작됩니다. 

        ![QTA 2단계 하위 1단계](../../relational-databases/performance/media/qta-step2-substep1.png "QTA 2단계 하위 1단계")

    2. **데이터베이스 업그레이드** 에서는 데이터베이스 호환성 수준을 원하는 대상으로 업그레이드하는 데 필요한 권한에 대한 메시지가 표시됩니다. 다음 하위 단계를 진행하려면 **예** 를 선택합니다.

        ![QTA 2단계 하위 2단계 - 데이터베이스 호환성 수준 업그레이드](../../relational-databases/performance/media/qta-step2-substep2-prompt.png "QTA 2단계 하위 2단계 - 데이터베이스 호환성 수준 업그레이드")

        다음 페이지는 데이터베이스 호환성 수준이 성공적으로 업그레이드되었음을 확인합니다.

        ![QTA 2단계 하위 2단계](../../relational-databases/performance/media/qta-step2-substep2.png "QTA 2단계 하위 2단계")

    3. **데이터 수집 관찰** 에서는 해당 쿼리 저장소가 최적화 기회를 검색하는 데 사용할 비교 기준을 수집할 수 있도록 대표적인 워크로드 주기를 다시 실행할 것을 사용자에게 요청합니다. 워크로드가 실행되면 **새로 고침** 단추를 사용하여 발견된 경우 회귀된 쿼리의 목록을 계속 업데이트합니다. **표시할 쿼리** 값을 변경하여 표시되는 쿼리의 수를 제한합니다. 목록의 순서는 **메트릭**(기간 또는 CpuTime) 및 **집계**(평균이 기본값)의 영향을 받습니다. 또한 **표시할 쿼리** 의 수를 선택합니다. 워크로드가 완료되면 **워크로드 실행 완료** 를 선택하고 **다음** 을 선택합니다.

        ![QTA 2단계 하위 3단계](../../relational-databases/performance/media/qta-step2-substep3.png "QTA 2단계 하위 3단계")

        목록에는 다음과 같은 정보가 포함됩니다.
        - **쿼리 ID** 
        - **쿼리 텍스트**: **...** 단추를 선택하여 확장할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.
        - **실행**: 전체 워크로드 컬렉션에 대해 쿼리하는 실행 횟수를 표시합니다.
        - **기준선 메트릭**: 데이터베이스 호환성 업그레이드 전에 기준 데이터 수집을 위한 ms 단위의 선택한 메트릭(기간 또는 CpuTime)입니다.
        - **관찰된 메트릭**: 데이터베이스 호환성 업그레이드 후에 데이터 수집을 위한 ms 단위의 선택한 메트릭(기간 또는 CpuTime)입니다.
        - **변경률(%)** : 데이터베이스 호환성 업그레이드 전후 사이의 선택한 메트릭에 대한 변경률을 백분율로 표시한 것입니다. 음수는 쿼리에 대한 측정된 회귀의 양을 나타냅니다.
        - **튜닝 가능**: 쿼리가 실험에 적합한지 여부에 따라 *True* 또는 *False* 입니다.

4. **분석 보기** 를 사용하면 실험할 쿼리를 선택하고 최적화 기회를 찾을 수 있습니다. **표시할 쿼리** 값은 실험에 적합한 쿼리의 범위가 됩니다. 원하는 쿼리가 확인되면 **다음** 을 선택하여 실험을 시작합니다.

    > [!NOTE]
    > 튜닝 가능이 False인 쿼리는 실험에 선택할 수 없습니다.

    > [!IMPORTANT]
    > QTA가 실험 단계로 이동되면 분석 보기 페이지로 돌아갈 수 없다는 메시지가 표시됩니다.   
    > 실험 단계로 이동하기 전에 적합한 쿼리를 모두 선택하지 않으면 나중에 새 세션을 만들고 워크플로를 반복해야 합니다. 이렇게 하려면 데이터베이스 호환성 수준을 이전 값으로 다시 설정해야 합니다.

    ![QTA 3단계](../../relational-databases/performance/media/qta-step3.png "QTA 3단계")

5. **결과 보기** 를 사용하면 제안된 최적화를 계획 지침으로 배포할 쿼리를 선택할 수 있습니다. 

    목록에는 다음과 같은 정보가 포함됩니다.
    - **쿼리 ID**
    - **쿼리 텍스트**: **...** 단추를 선택하여 확장할 수 있는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다.
    - **상태**: 쿼리에 대한 현재 실험 상태를 표시합니다.
    - **기준 메트릭**: **2단계 하위 3단계** 에서 실행한 대로 쿼리를 위한 ms 단위의 선택한 메트릭(기간 또는 CpuTime)으로 데이터베이스 호환성 업그레이드 후에 회귀된 쿼리를 표시합니다.
    - **관찰된 메트릭**: 충분히 적합한 제안된 최적화를 위해 실험 후 쿼리를 위한 ms 단위의 선택한 메트릭(기간 또는 CpuTime)입니다.
    - **변경률(%)** : 실험 단계 전후 사이의 선택한 메트릭에 대한 변경률을 백분율로 표시한 것입니다. 제안된 최적화를 사용한 쿼리에 대해 측정된 개선 사항의 양을 표시합니다.
    - **쿼리 옵션**: 쿼리 실행 메트릭을 개선하는 제안된 힌트로 연결됩니다.
    - **배포 가능**: 제안된 쿼리 최적화를 계획 지침으로 배포할 수 있는지 여부에 따라 *True* 또는 *False* 입니다.

    ![QTA 4단계](../../relational-databases/performance/media/qta-step4.png "QTA 4단계")

6. **확인** 은 이 세션에 대해 이전에 선택한 쿼리의 배포 상태를 보여줍니다. 이 페이지의 목록은 **배포 가능** 열을 **롤백 가능** 으로 변경하여 이전 페이지와는 다릅니다. 이 열은 배포된 쿼리 최적화를 롤백할 수 있는지 여부와 해당 계획 지침을 제거했는지 여부에 따라 *True* 또는 *False* 가 될 수 있습니다.

    ![QTA 5단계](../../relational-databases/performance/media/qta-step5.png "QTA 5단계")

    나중에 제안된 최적화에서 롤백해야 하는 경우 관련 쿼리를 선택하고 **롤백** 을 선택합니다. 해당 쿼리 계획 지침이 제거되고 롤백된 쿼리를 제거하기 위해 목록이 업데이트됩니다. 아래 그림에서는 해당 쿼리 8이 제거되었습니다.

    ![QTA 5단계 - 롤백](../../relational-databases/performance/media/qta-step5-rollback.png "QTA 5단계 - 롤백")

    > [!NOTE]
    > 닫힌 세션을 삭제해도 이전에 배포된 계획 지침은 삭제되지 **않습니다**.
    > 배포된 계획 지침이 있는 세션을 삭제하는 경우 QTA를 사용하여 롤백할 수 없습니다.
    > 대신 [sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) 시스템 테이블을 사용하여 계획 지침을 검색하고 [sp_control_plan_guide](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)를 사용하여 수동으로 삭제합니다.
  
## <a name="permissions"></a>사용 권한

**db_owner** 역할의 멤버 자격이 필요합니다.
  
## <a name="see-also"></a>참고 항목

- [호환성 수준 및 업그레이드 데이터베이스 엔진](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)
- [성능 모니터링 및 튜닝 도구](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)
- [쿼리 저장소를 사용하여 성능 모니터링](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [데이터베이스 호환성 모드 변경 및 쿼리 저장소 사용](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)
- [추적 플래그](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)
- [USE HINT 쿼리 힌트](../../t-sql/queries/hints-transact-sql-query.md#use_hint)
- [카디널리티 평가기](../../relational-databases/performance/cardinality-estimation-sql-server.md)
- [자동 조정](../../relational-databases/automatic-tuning/automatic-tuning.md)   
- [SQL Server 쿼리 튜닝 길잡이 사용](https://docs.microsoft.com/learn/modules/use-sql-server-query-tuning-assistant/)
