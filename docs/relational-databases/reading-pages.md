---
title: 페이지 읽기 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- pages
ms.assetid: f8da760e-aacb-4661-9f3a-2578d8c11e4e
caps.latest.revision: 3
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 34fc49117e2d406b58a8dce9731b8fdf89634c52
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="reading-pages"></a>페이지 읽기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server [!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스의 I/O에는 논리적 읽기 수 및 물리적 읽기 수가 포함되어 있습니다. 논리적 읽기는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 [버퍼 캐시](../relational-databases/memory-management-architecture-guide.md)에서 페이지를 요청할 때마다 발생합니다. 페이지가 현재 버퍼 캐시에 없는 경우 물리적 읽기가 먼저 디스크의 페이지를 캐시로 복사합니다.

[!INCLUDE[ssDE](../includes/ssde-md.md)] 인스턴스로 생성된 읽기 요청은 관계형 엔진에 의해 제어되고 저장소 엔진에 의해 최적화됩니다. 관계형 엔진은 테이블 검색, 인덱스 검색 또는 키 사용 읽기와 같은 가장 효과적인 액세스 방법을 결정합니다. 저장소 엔진의 액세스 방법 및 버퍼 관리자 구성 요소는 수행할 일반적인 읽기 패턴을 결정하고 액세스 방법을 구현하는 데 필요한 읽기를 최적화합니다. 일괄 처리를 실행하는 스레드는 읽기 일정을 계획합니다.

## <a name="read-ahead"></a>미리 읽기
[!INCLUDE[ssDE](../includes/ssde-md.md)] 은 미리 읽기라고 하는 성능 최적화 메커니즘을 지원합니다. 미리 읽기는 쿼리 실행 계획을 수행하는 데 필요한 데이터 및 인덱스 페이지를 예상하고 페이지가 쿼리에서 실제로 사용되기 전에 해당 페이지를 버퍼 캐시로 가져옵니다. 이렇게 하면 계산과 I/O가 동시에 수행되어 CPU와 디스크를 모두 충분히 활용할 수 있습니다. 

미리 읽기 메커니즘을 통해 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서는 한 파일에서 연속하는 최대 64페이지(512KB)를 읽을 수 있습니다. 읽기는 버퍼 캐시에서 연속되지 않은 적절한 수의 버퍼에 대해 단일 분산 수집 읽기로 수행됩니다. 해당 범위의 페이지 중 버퍼 캐시에 이미 존재하는 페이지가 있을 경우 읽기가 완료된 후 읽기에서 해당 페이지가 삭제됩니다. 해당 페이지가 캐시에 이미 있을 경우 완료 후 페이지 범위가 "잘릴" 수도 있습니다.

미리 읽기에는 데이터 페이지 읽기와 인덱스 페이지 읽기가 있습니다.

### <a name="reading-data-pages"></a>데이터 페이지 읽기
[!INCLUDE[ssDE](../includes/ssde-md.md)]에서는 데이터 페이지를 읽을 때 테이블 검색을 사용하면 매우 효율적입니다. SQL Server Database에 있는 IAM(Index Allocation Map) 페이지에 테이블 또는 인덱스에서 사용하는 익스텐트가 나열됩니다. 저장소 엔진은 IAM을 읽어서 읽어야 하는 정렬된 디스크 주소 목록을 작성할 수 있습니다. 이렇게 하면 저장소 엔진이 디스크에서의 I/O 위치를 기반으로 하여 순서대로 수행되는 대형 순차 읽기로 해당 I/O를 최적화할 수 있습니다. IAM 페이지에 대한 자세한 내용은 [개체에서 사용하는 공간 관리](../relational-databases/pages-and-extents-architecture-guide.md)를 참조하세요.

### <a name="reading-index-pages"></a>인덱스 페이지 읽기
저장소 엔진은 인덱스 페이지를 키 순서로 읽습니다. 예를 들어 다음 그림은 키 집합을 포함하는 리프 페이지 집합을 간단히 보여 주고 리프 페이지를 매핑하는 중간 인덱스 노드를 보여 줍니다. 인덱스 페이지의 구조에 대한 자세한 내용은 [클러스터형 인덱스 구조](../relational-databases/pages-and-extents-architecture-guide.md)를 참조하세요.

![Reading_Pages](../relational-databases/media/reading-pages.gif)

저장소 엔진은 리프 수준 위의 중간 인덱스 페이지에 있는 정보를 사용하여 키를 포함하는 페이지의 직렬 미리 읽기를 예약합니다. ABC에서 DEF까지의 모든 키에 대해 요청이 수행된 경우 저장소 엔진은 리프 페이지 위의 인덱스 페이지를 먼저 읽습니다. 그러나 504페이지에서 556페이지까지(지정된 범위의 키를 포함하는 마지막 페이지) 순서대로 각 데이터 페이지를 단순히 읽지는 않습니다. 대신 저장소 엔진은 중간 인덱스 페이지를 검색하고 읽어야 하는 리프 페이지 목록을 작성합니다. 그런 다음 저장소 엔진은 키 순서대로 모든 읽기를 예약합니다. 또한 저장소 엔진은 페이지 504/505 및 527/528이 인접해 있다고 인식하고 단일 분산 읽기를 수행하여 단일 작업으로 인접한 페이지들을 검색합니다. 직렬 작업에서 검색할 페이지가 많으면 저장소 엔진은 한 번에 읽을 블록을 예약합니다. 이러한 읽기 하위 집합이 완료되면 저장소 엔진은 읽어야 할 모든 내용이 예약될 때까지 같은 수의 새 읽기를 예약합니다.

저장소 엔진은 사전 인출을 사용하여 비클러스터형 인덱스의 기본 테이블 조회 속도를 향상시킵니다. 비클러스터형 인덱스의 리프 행은 각각의 특정 키 값을 포함하는 데이터 행에 대한 포인터를 포함합니다. 저장소 엔진이 비클러스터형 인덱스의 리프 페이지를 읽을 때 포인터가 이미 검색된 데이터 행에 대한 비동기 읽기도 예약하기 시작합니다. 이를 통해 저장소 엔진은 비클러스터형 인덱스의 검색이 완료되기 전에 기본 테이블의 데이터 행을 검색할 수 있습니다. 사전 인출은 테이블에 클러스터형 인덱스가 포함되었는지 여부에 관계없이 사용됩니다. SQL Server Enterprise에서는 다른 버전의 SQL Server보다 많은 사전 인출을 사용하므로 더 많은 페이지를 미리 읽을 수 있습니다. 사전 인출 수준은 어느 버전에서도 구성할 수 없습니다. 비클러스터형 인덱스에 대한 자세한 내용은 [비클러스터형 인덱스 구조](../relational-databases/pages-and-extents-architecture-guide.md)를 참조하세요.

## <a name="advanced-scanning"></a>고급 검색
SQL Server Enterprise의 고급 검색 기능을 사용하여 여러 태스크에서 전체 테이블 검색을 공유할 수 있습니다. Transact-SQL 문의 실행 계획이 테이블의 데이터 페이지 검색을 요구하고 [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 테이블이 이미 다른 실행 계획에 대해 검색되고 있음을 감지하는 경우 [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 두 번째 검색의 현재 위치에서 두 번째 검색을 첫 번째 실행 계획에 조인합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 각 페이지를 한 번 읽고 각 페이지의 행을 두 실행 계획에 전달합니다. 이 작업은 테이블 끝에 도달할 때까지 계속됩니다. 

테이블 끝에서 첫 번째 실행 계획에 완전한 검색 결과가 포함되지만 두 번째 실행 계획은 진행 중인 검색을 조인하기 전에 읽어오는 데이터 페이지를 계속 검색해야 합니다. 그런 다음 두 번째 실행 계획 검색은 테이블의 첫 번째 데이터 페이지로 다시 넘어가고 첫 번째 검색을 조인한 지점까지 검색이 진행됩니다. 이런 방식으로 원하는 수만큼 검색을 결합할 수 있습니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 모든 검색을 완료할 때까지 데이터 페이지를 계속 루핑합니다. 이 메커니즘은 ORDER BY 절 없이 SELECT 문에서 반환된 결과의 순서를 보장할 수 없기 때문에 "회전목마(merry-go-round) 검색"이라고도 합니다. 

예를 들어 500,000개의 페이지를 포함하는 테이블이 있다고 합시다. UserA는 테이블의 검색을 요청하는 Transact-SQL 문을 실행합니다. 해당 검색이 100,000개의 페이지를 처리할 때 UserB가 동일한 테이블을 검색하는 다른 Transact-SQL 문을 실행합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 100,001페이지 이후의 페이지에 대해 하나의 읽기 요청 집합을 예약하고 각 페이지의 행을 두 검색에 다시 전달합니다. 200,000번째 페이지를 검색할 때 UserC가 동일한 테이블을 검색하는 다른 Transact-SQL 문을 실행합니다. 200,001페이지부터 [!INCLUDE[ssDE](../includes/ssde-md.md)] 은 읽고 있는 각 페이지의 행을 세 가지 검색에 모두 다시 전달합니다. 500,000번째 행을 읽고 나면 UserA에 대한 검색이 완료되고 UserB 및 UserC에 대한 검색이 다시 시작되며 1페이지부터 다시 읽기 시작합니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 이 100,000페이지에 도달하면 UserB의 검색이 완료됩니다. 그런 다음 200,000페이지를 읽을 때까지 UserC에 대한 검색이 계속됩니다. 이 페이지가 되면 모든 검색이 완료됩니다. 

고급 검색을 사용하지 않는 경우 각 사용자는 버퍼 공간을 최대한 사용하려고 하며 이로 인해 디스크 충돌 경합이 발생합니다. 그러면 같은 페이지를 여러 사용자가 한 번에 읽고 공유하는 대신 각 사용자가 한 번씩 읽게 되므로 성능이 저하되고 리소스 처리 시간이 소모됩니다.

## <a name="see-also"></a>참고 항목
[페이지 및 익스텐트 아키텍처 가이드](../relational-databases/pages-and-extents-architecture-guide.md)   
 [페이지 쓰기](../relational-databases/writing-pages.md)
