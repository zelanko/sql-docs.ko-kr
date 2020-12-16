---
description: 가속 데이터베이스 복구
title: 가속 데이터베이스 복구 | Microsoft Docs
ms.date: 05/20/2020
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- accelerated database recovery [SQL Server], recovery-only
- database recovery [SQL Server]
author: mashamsft
ms.author: mathoma
ms.reviewer: kfarlee
monikerRange: '>=sql-server-ver15'
ms.openlocfilehash: fc56c4baae161570f3167323bf7c6b9d26d6beb1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483745"
---
# <a name="accelerated-database-recovery"></a>가속 데이터베이스 복구

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

ADR(가속 데이터베이스 복구)은 특히 장기 실행 트랜잭션이 있는 경우 SQL 데이터베이스 엔진 복구 프로세스를 다시 설계하여 데이터베이스 가용성을 향상시킵니다. ADR은 SQL Server 2019의 새로운 기능입니다. 

Azure SQL Database, Azure SQL Managed Instance, Azure Synapse SQL의 데이터베이스에도 ADR을 사용할 수 있습니다. SQL Database 및 SQL Managed Instance에서는 ADR이 기본적으로 사용되며, 사용하지 않도록 설정할 수 없습니다. 

## <a name="overview"></a>개요

ADR의 주요 이점은 다음과 같습니다.

- **빠르고 일관된 데이터베이스 복구**

  ADR을 사용하면 장기 실행 트랜잭션이 전체 복구 시간에 영향을 주지 않으므로 시스템의 활성 트랜잭션 수 또는 크기에 관계없이 빠르고 일관된 데이터베이스 복구를 사용할 수 있습니다.

- **즉시 트랜잭션 롤백**

  ADR을 사용하면 트랜잭션이 활성 상태인 시간 또는 수행된 업데이트 수와 관계없이 트랜잭션 롤백이 즉시 수행됩니다.

- **적극적인 로그 잘림**

  ADR을 사용하면 활성 장기 실행 트랜잭션이 있는 경우에도 트랜잭션 로그가 적극적으로 잘리고 제어를 사용할 수 없게 됩니다.

## <a name="the-current-database-recovery-process"></a>현재 데이터베이스 복구 프로세스

ADR을 사용하지 않으면 SQL Server의 데이터베이스 복구는 [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf) 복구 모델을 따르며 다음 다이어그램에 설명되어 있는 세 단계로 구성됩니다. 이에 대한 자세한 내용은 다이어그램 뒤에 자세히 설명되어 있습니다.

![현재 복구 프로세스](./media/accelerated-database-recovery-concepts/current-recovery-process.png)

- **분석 단계**

  SQL Server는 마지막으로 성공한 검사점(또는 가장 오래된 더티 페이지 LSN)의 시작 부분에서 트랜잭션 로그의 전방 검색을 수행하여 SQL Server가 중지된 시점에 각 트랜잭션의 상태를 확인합니다.

- **다시 실행 단계**

  SQL Server는 종료될 때까지 커밋되지 않은 가장 오래된 트랜잭션에서 트랜잭션 로그를 검색하여 모든 커밋된 작업을 다시 실행하는 방법으로 데이터베이스를 작동 중단 상태로 가져올 수 있습니다.

- **실행 취소 단계**

  작동 중단 시 활성 상태였던 각 트랜잭션에 대해 SQL Server는 로그를 역방향으로 순회하여 이 트랜잭션이 수행한 작업을 실행 취소합니다.

이 디자인을 기반으로 데이터베이스 엔진이 예기치 않게 다시 시작되는 것을 복구하는 데 걸리는 시간은 충돌 시 시스템에서 가장 오래된 활성 트랜잭션의 크기에 비례합니다. 복구하려면 불완전한 모든 트랜잭션을 롤백해야 합니다. 필요한 시간은 트랜잭션이 수행한 작업과 활성 상태였던 시간에 비례합니다. 따라서 장기 실행 트랜잭션이 있을 때는 SQL Server 복구 프로세스가 오래 걸릴 수 있습니다(예: 큰 테이블에 대한 대량 삽입 작업 또는 인덱스 작성 작업).

또한 이 디자인을 기반으로 하는 대량 트랜잭션은 위의 설명처럼 동일한 실행 취소 복구 단계를 사용할 때처럼 오래 걸릴 수 있습니다.

또한 장기 트랜잭션이 있는 경우에는 해당 로그 레코드가 복구 및 롤백 프로세스에 필요하므로 데이터베이스 엔진이 트랜잭션 로그를 잘라낼 수 없습니다. 따라서 일부 트랜잭션 로그는 매우 커지고 많은 양의 드라이브 공간을 사용하게 됩니다.

## <a name="the-accelerated-database-recovery-process"></a>가속 데이터베이스 복구 프로세스

ADR은 데이터베이스 엔진 복구 프로세스를 완전히 다시 디자인하여 위의 문제를 해결합니다.

- 가장 오래된 활성 트랜잭션의 시작 부분에서 로그를 검색할 필요가 없도록 하여 시간/인스턴트를 일정하게 만듭니다. ADR을 사용하는 경우 트랜잭션 로그는 마지막으로 성공한 검사점(또는 가장 오래된 더티 페이지 LSN(로그 시퀀스 번호))에서만 처리됩니다. 따라서 복구 시간은 장기 실행 트랜잭션의 영향을 받지 않습니다.
- 전체 트랜잭션에 대한 로그를 더 이상 처리할 필요가 없기 때문에 필요한 트랜잭션 로그 공간을 최소화합니다. 결과적으로 트랜잭션 로그는 검사점 및 백업이 발생될 때 적극적으로 잘릴 수 있습니다.

상위 수준에서 ADR은 모든 물리적 데이터베이스 수정의 버전을 관리하고 제한적이면서 거의 즉시 실행 취소할 수 있는 논리 연산만 실행 취소하여 빠른 데이터베이스 복구를 달성합니다. 충돌 시 활성 상태였던 모든 트랜잭션은 중단된 것으로 표시되므로 동시 사용자 쿼리에서는 이러한 트랜잭션에 의해 생성된 모든 버전을 무시할 수 있습니다.

ADR 복구 프로세스는 현재 복구 프로세스와 동일한 3단계로 이루어져 있습니다. 다음 다이어그램에서는 이러한 단계가 ADR에서 작동하는 방식에 대해 설명합니다.

![ADR 복구 프로세스](./media/accelerated-database-recovery-concepts/adr-recovery-process.png)

- **분석 단계**

  이 프로세스는 현재와 동일하며, 버전이 없는 작업의 경우 sLog를 다시 작성하고 로그 레코드를 복사하는 단계가 추가되었습니다.
  
- **다시 실행** 단계

  두 하위 단계로 나뉩니다.
  - 하위 단계 1

      sLog(마지막 검사점까지 가장 오래된 커밋되지 않은 트랜잭션)에서 다시 실행합니다. 다시 실행은 sLog에서 몇 개의 레코드만 처리하면 되므로 빠른 작업입니다.

  - 하위 단계 2

     트랜잭션 로그에서 다시 실행은 마지막 검사점(커밋되지 않은 가장 오래된 트랜잭션 대신)에서 시작됩니다.
     
- **실행 취소 단계**

   ADR을 사용하는 실행 취소 단계는 sLog를 사용하여 작업을 실행 취소하고 논리적 되돌리기를 사용하여 PVS(지속형 버전 저장소)를 실행하여 행 수준 버전 기반 실행 취소를 수행하여 거의 즉시 완료됩니다.

가속화된 데이터베이스 복구에 대해 설명하는 8분 분량의 다음 동영상을 시청할 수도 있습니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Advanced-Database-Recovery--Data-Exposed/player?WT.mc_id=dataexposed-c9-niner]

## <a name="adr-recovery-components"></a>ADR 복구 구성 요소

ADR의 네 가지 주요 구성 요소는 다음과 같습니다.

- **PVS(지속형 버전 저장소)**

  지속형 버전 저장소는 기존의 `tempdb` 버전 저장소 대신 데이터베이스 자체에 생성된 행 버전을 유지하기 위한 데이터베이스 엔진 메커니즘입니다. PVS는 리소스 격리를 사용할 수 있도록 하며 읽기 가능한 보조 복제본의 가용성을 개선합니다.

- **논리적 되돌리기**

  논리적 되돌리기는 모든 버전의 작업에 대해 즉시 트랜잭션 롤백 및 실행 취소를 제공하는 행 수준 버전 기반 실행 취소를 수행하는 비동기 프로세스입니다.

  - 중단된 모든 트랜잭션을 추적합니다.
  - 모든 사용자 트랜잭션에 대해 PVS를 사용하여 롤백을 수행합니다.
  - 트랜잭션이 중단된 직후 모든 잠금을 해제합니다.

- **sLog**

  sLog는 버전이 없는 작업(예: 메타데이터 캐시 무효화, 잠금 획득 등)에 대한 로그 레코드를 저장하는 보조 메모리 내 로그 스트림입니다. sLog는 다음과 같습니다.

  - 적은 볼륨 및 메모리 내
  - 검사점 프로세스 중에 직렬화되어 디스크에 유지됩니다.
  - 트랜잭션이 커밋될 때 정기적으로 잘립니다.
  - 버전이 없는 작업만 처리하여 다시 실행 및 실행 취소를 가속화합니다.  
  - 필요한 로그 레코드만 유지하여 적극적인 트랜잭션 로그 잘림을 가능하게 합니다.

- **클리너**

  클리너는 정기적으로 절전 모드를 해제하고 필요하지 않은 페이지 버전을 정리하는 비동기 프로세스입니다.

## <a name="who-should-consider-accelerated-database-recovery"></a>가속 데이터베이스 복구를 고려해야 하는 경우

ADR 사용을 고려해야 할 고객은 다음과 같습니다.

- 장기 실행 트랜잭션이 있는 워크로드를 가진 고객
- 활성 트랜잭션이 트랜잭션 로그를 크게 증가시키는 경우가 있는 고객  
- SQL Server 장기 실행 복구(예: 예기치 않은 SQL Server 다시 시작 또는 수동 트랜잭션 롤백)로 인해 장기간 데이터베이스를 사용하지 못한 경험이 있는 고객.

>[!IMPORTANT]
>ADR은 데이터베이스 미러링에 등록된 데이터베이스에 대해 지원되지 않습니다.

## <a name="see-also"></a>참고 항목  

[가속 데이터베이스 복구 관리](accelerated-database-recovery-management.md)
