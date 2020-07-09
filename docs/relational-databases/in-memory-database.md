---
title: 메모리 내 데이터베이스 시스템 기능 및 기술
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory systems
- in-memory technologies
- in-memory features
- database, in-memory database
- system, in-memory system
- features, in-memory features
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
ms.openlocfilehash: 0c71bda5a459c7993de824cdb6665978ba57166f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892465"
---
# <a name="in-memory-database-systems-and-technologies"></a>메모리 내 데이터베이스 시스템 및 기술

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

이 페이지는 SQL Server의 메모리 내 기능 및 기술에 대한 참조 페이지로 작성되었습니다. 메모리 내 데이터베이스 시스템의 개념은 최신 데이터베이스 시스템에서 사용할 수 있는 큰 메모리 용량을 활용하도록 설계된 데이터베이스 시스템을 가리킵니다. 메모리 내 데이터베이스는 본질적으로 관계형 또는 비관계형일 수 있습니다.

메모리 내 데이터베이스 시스템의 성능 이점은 대체로 사용 가능한 가장 빠른 디스크 하위 시스템에 있는 데이터보다 메모리에 상주하는 데이터에 액세스하는 속도가 몇 배나 더 빠르기 때문으로 간주되는 경우가 많습니다. 그러나 대부분의 SQL Server 워크로드는 전체 작업 세트를 사용 가능한 메모리에 맞출 수 있습니다. 많은 메모리 내 데이터베이스 시스템은 데이터를 디스크에 저장할 수 있으며, 전체 데이터 세트가 사용 가능한 메모리에 모두 들어가지 않을 수도 있습니다.

상당히 느리지만, 내구성이 있는 미디어 앞에 배치된 빠른 휘발성 캐시가 관계형 데이터베이스 워크로드에 주로 사용되었습니다. 이 때문에 워크로드 관리에 대한 특정 접근 방법이 필요합니다. 더 빠른 메모리 전송 속도, 더 많은 용량 또는 영구 메모리가 제공하는 기회는 새로운 기능과 기술의 개발을 가능하게 하며, 관계형 데이터베이스 워크로드 관리에 대한 새로운 접근 방법을 촉진할 수 있습니다.

## <a name="hybrid-buffer-pool"></a>하이브리드 버퍼 풀

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

[하이브리드 버퍼 풀](../database-engine/configure-windows/hybrid-buffer-pool.md)은 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 사용하여 Windows 및 Linux 플랫폼에 대해 바이트 주소 지정 가능한 영구 메모리 스토리지 디바이스에 있는 데이터베이스 파일의 버퍼 풀을 확장합니다.

## <a name="memory-optimized-tempdb-metadata"></a>메모리 최적화 `tempdb` 메타데이터

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 [메모리 최적화 tempdb 메타데이터](./databases/tempdb-database.md#memory-optimized-tempdb-metadata)인 새로운 기능을 도입하여 일부 경합 병목 현상을 효과적으로 제거하고 tempdb-heavy 워크로드를 위한 새로운 수준의 확장성을 구현합니다.

## <a name="in-memory-oltp"></a>메모리 내 OLTP

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/applies-to-version/sqlserver.md)]

[메모리 내 OLTP](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md)는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../includes/sssds-md.md)]에서 트랜잭션 처리, 데이터 수집, 데이터 로드 및 일시적인 데이터 시나리오의 성능을 최적화하기 위해 사용할 수 있는 데이터베이스 기술입니다.

## <a name="configuring-persistent-memory-support-for-linux"></a>Linux에 대해 영구 메모리 지원 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)]에서는 `ndctl` 유틸리티 [영구 메모리](../linux/sql-server-linux-configure-pmem.md)를 사용하여 PMEM(영구 메모리)을 구성하는 방법을 설명합니다.

## <a name="persisted-log-buffer"></a>지속형 로그 버퍼

[!INCLUDE[ssSQL16](../includes/sssql16-md.md)] 서비스 팩 1에서는 WRITELOG wait를 통해 바인딩된, 쓰기 사용이 많은 워크로드에 대한 성능 최적화가 도입되었습니다. 영구 메모리를 사용하여 로그 버퍼를 저장합니다. 이 버퍼는 작기 때문에(사용자 데이터베이스당 20MB), 트랜잭션 로그에 기록된 트랜잭션을 확정하기 위해 버퍼를 디스크로 플러시해야 합니다. 쓰기 사용 OLTP 워크로드의 경우 이 플러시 메커니즘으로 인해 병목 상태가 발생할 수 있습니다. 영구 메모리에 로그 버퍼를 저장하면 로그를 확정하는 데 필요한 작업 수가 줄어들어 전반적인 트랜잭션 시간이 개선되고 워크로드 성능이 향상됩니다. 이 프로세스는 [비상 로그 캐싱]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)으로 도입되었습니다. 그러나 [비상 로그 백업](./backup-restore/tail-log-backups-sql-server.md) 및 비상 로그가 확정되었지만, 아직 백업되지 않은 트랜잭션 로그 부분이라는 기존의 이해와 충돌하는 경우가 발견되었습니다. 공식적인 기능 이름이 지속형 로그 버퍼이므로 여기서는 해당 이름을 사용합니다.

[데이터베이스에 지속형 로그 버퍼 추가](./databases/add-persisted-log-buffer.md)를 참조하세요.
