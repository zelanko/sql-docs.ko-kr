---
title: SQL 메모리 내 OLTP용 하드웨어 | Microsoft 문서
description: SQL Server의 메모리 내 OLTP 성능에 대한 하드웨어 고려 사항을 알아봅니다. 메모리 내 OLTP는 메모리 및 디스크를 디스크 기반 테이블과 다른 방식으로 사용합니다.
ms.custom: ''
ms.date: 03/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 09483122764de51b565693d85c3ae8efa9a8c570
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465354"
---
# <a name="hardware-considerations-for-in-memory-oltp-in-sql-server"></a>SQL Server의 메모리 내 OLTP에 대한 하드웨어 고려 사항

메모리 내 OLTP는 메모리 및 디스크를 기존 디스크 기반 테이블과 다른 방식으로 사용합니다. 사용하는 하드웨어에 따라 메모리 내 OLTP의 성능이 향상되는 수준이 달라집니다. 이 블로그 게시물에서는 다양한 일반 하드웨어 고려 사항을 설명하고, 하드웨어를 메모리 내 OLTP에 사용하기 위한 일반 지침을 제공합니다.

> [!NOTE]
> 이 문서는 Microsoft SQL Server 2014 팀이 2013년 8월 1일에 올린 블로그 게시물입니다. 블로그 웹 페이지가 제거됩니다.
>
> [SQL Server 메모리 내 OLTP](./in-memory-oltp-in-memory-optimization.md)

<!--
    Here was the link to the blog. This blog was captured into this new article on 2018/11/30, by GeneMi (MightyPen).
    https://cloudblogs.microsoft.com/sqlserver/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014/
    At least one pre-existing article that contained the obsolete blog link was:
        relational-databases\in-memory-oltp\sample-database-for-in-memory-oltp.md
-->

## <a name="cpu"></a>CPU

메모리 내 OLTP는 고성능 서버가 없어도 처리량이 높은 OLTP 워크로드를 지원할 수 있습니다. CPU 소켓이 2개인 중급 서버를 권장합니다. 메모리 내 OLTP 덕분에 처리량이 향상되었기 때문에 소켓 2개면 고객의 비즈니스 요구 사항을 해결하기에 충분할 것입니다.

메모리 내 OLTP를 사용하고 하이퍼 스레딩을 켤 것을 권장합니다. 일부 OLTP 워크로드에서 하이퍼 스레딩을 사용하여 성능이 최대 40%까지 향상된 것을 목격했습니다.

## <a name="memory"></a>메모리

모든 메모리 최적화 테이블은 완전히 메모리에 상주합니다. 따라서 테이블 자체 및 데이터베이스에 대해 실행되는 워크로드를 유지하는 데 사용할 실제 메모리가 충분해야 합니다. 실제로 필요한 메모리 양은 워크로드에 따라 달라지지만, 대부분의 고객은 데이터 크기의 2배에 해당하는 메모리 양으로 시작하는 것이 일반적입니다. 워크로드가 기존 디스크 기반 테이블에서도 작동하는 경우를 대비하여 버퍼 풀에 사용할 메모리도 충분히 있어야 합니다.

지정된 메모리 최적화 테이블에서 메모리를 얼마나 사용하는지 확인하려면 다음 쿼리를 실행합니다.

```sql
select object_name(object_id), * from sys.dm_db_xtp_table_memory_stats;
```

결과를 보면 메모리 최적화 테이블과 해당 인덱스에 사용되는 메모리 양을 알 수 있습니다. 테이블 데이터에는 사용자 데이터뿐 아니라 실행 중인 트랜잭션에 필요하거나 시스템에서 아직 정리하지 않은 이전 행 버전이 포함됩니다. 해시 인덱스에서 사용하는 메모리는 상수이며 테이블의 행 수에 종속되지 않습니다.

메모리 내 OLTP를 사용할 때 데이터베이스 전체가 메모리에 맞아야 할 필요는 없습니다. 데이터베이스 크기가 테라바이트 단위이더라도 핫 데이터(예: 메모리 최적화 테이블)의 크기가 256GB를 넘지만 않으면 여전히 메모리 내 OLTP에서 이점을 얻을 수 있습니다. SQL Server가 단일 데이터베이스에 대해 관리할 수 있는 검사점 데이터 파일은 최대 4000개이고, 각 파일 크기는 128MB입니다. 이론적으로 가능한 최대 크기는 512GB지만, SQL Server가 검사점 파일 병합을 처리하고 4000개 파일 제한에 도달하지 않도록 256GB까지만 지원하는 것입니다. 이 제한은 메모리 최적화 테이블에만 적용되며, 동일한 SQL Server 데이터베이스에 있는 기존 디스크 기반 테이블에는 이러한 크기 제한이 없습니다.

NDT(비영구 메모리 최적화 테이블), 즉, DURABILITY=SCHEMA_ONLY인 메모리 최적화 테이블은 디스크에 보존되지 않습니다. NDT는 검사점 파일 수의 제약을 받지 않지만, 256GB만 지원됩니다. 데이터가 메모리에만 존재하므로 이 게시물의 나머지 부분에서 다루는 로그 및 데이터 드라이브에 대한 고려 사항은 비영구 테이블에 적용되지 않습니다.

## <a name="log-drive"></a>로그 드라이브

메모리 최적화 테이블에 관련된 로그 레코드는 다른 SQL Server 로그 레코드와 함께 데이터베이스 트랜잭션 로그에 기록됩니다.

트랜잭션이 너무 오래 대기하지 않도록, 그리고 로그 IO에서 경합을 방지할 수 있도록 항상 대기 시간이 짧은 드라이브에 로그 파일을 배치해야 합니다. 시스템은 가장 느린 구성 요소의 속도에 맞춰 실행됩니다(암달의 법칙). 메모리 내 OLTP를 실행할 때 로그 IO 디바이스에서 병목 현상이 발생하지 않도록 주의해야 합니다. 대기 시간이 짧은 스토리지 디바이스, 적어도 SSD를 사용하는 것이 좋습니다.

메모리 최적화 테이블은 인덱스 작업을 기록하지 않고 실행 취소 레코드를 기록하지 않기 때문에 디스크 기반 테이블보다 로그 대역폭을 적게 사용합니다. 따라서 로그 IO 경합을 완화하는 데 도움이 됩니다.

## <a name="data-drive"></a>데이터 드라이브

검사점 파일을 사용하는 메모리 최적화 테이블의 보존에는 스트리밍 IO가 사용됩니다. 따라서 이러한 파일은 대기 시간이 짧은 드라이브 또는 고속 임의 IO가 필요하지 않습니다. 대신 이러한 드라이브의 주요 요인은 순차 IO의 속도와 HBA(호스트 버스 어댑터)의 대역폭입니다. 그러므로 SSD를 검사점 파일에 사용할 필요가 없으며, 순차 IO가 요구 사항을 충족하는 한 고성능 스핀들(즉, SAS)에 배치할 수 있습니다.

속도 요구 사항을 결정하는 데 있어서 가장 큰 요인은 서버 재시작 시 RTO[복구 시간 목표]입니다. 데이터베이스를 복구하는 동안 메모리 최적화 테이블의 모든 데이터를 디스크에서 메모리로 읽어 들여야 합니다. 데이터베이스 복구는 IO 하위 시스템의 순차적 읽기 속도로 진행됩니다. 디스크는 병목을 유발합니다.

엄격한 RTO 요구 사항을 충족하려면 MEMORY_OPTIMIZED_DATA 파일 그룹에 여러 컨테이너를 추가하여 검사점 파일을 여러 디스크에 확산하는 것이 좋습니다. SQL Server는 여러 드라이브에서 검사점 파일을 병렬로 로드하는 것을 지원하여, 복구는 드라이브의 합산 속도로 진행됩니다.

디스크 용량 측면에서는 메모리 최적화 테이블의 2-3배 크기를 권장합니다.

## <a name="see-also"></a>참고 항목

[메모리 내 OLTP에 대한 예제 데이터베이스](sample-database-for-in-memory-oltp.md)