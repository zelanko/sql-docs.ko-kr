---
title: 메모리 내 데이터베이스 | Microsoft Docs
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- in-memory database
- feature, in-memory database
- in-memory
ms.assetid: 11f8017e-5bc3-4bab-8060-c16282cfbac1
author: briancarrig
ms.author: brcarrig
manager: amitban
ms.openlocfilehash: e4e0e6622a2a313b85dfa00df8c88044486f75f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995001"
---
# <a name="in-memory-database"></a>메모리 내 데이터베이스

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

메모리 내 데이터베이스는 메모리 내 기반 기술을 활용하는 SQL Server 내의 기능에 대한 포괄적인 용어입니다. 새로운 메모리 내 기반 기능이 개발됨에 따라 이 페이지는 계속 업데이트됩니다.

## <a name="hybrid-buffer-pool"></a>하이브리드 버퍼 풀

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[하이브리드 버퍼 풀](../database-engine/configure-windows/hybrid-buffer-pool.md)을 사용하면 데이터베이스 엔진이 영구 메모리(PMEM) 디바이스에 저장된 데이터베이스 파일의 데이터 페이지에 직접 액세스할 수 있습니다.

## <a name="memory-optimized-tempdb-metadata"></a>메모리 최적화 TempDB 메타데이터

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]는 [메모리 최적화 tempdb 메타데이터](./databases/tempdb-database.md#memory-optimized-tempdb-metadata)인 새로운 기능을 도입하여 일부 경합 병목 현상을 효과적으로 제거하고 tempdb-heavy 워크로드를 위한 새로운 수준의 확장성을 구현합니다.

## <a name="in-memory-oltp"></a>메모리 내 OLTP

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[메모리 내 OLTP](./in-memory-oltp/in-memory-oltp-in-memory-optimization.md)는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssSDS](../includes/sssds-md.md)]에서 트랜잭션 처리, 데이터 수집, 데이터 로드 및 일시적인 데이터 시나리오의 성능을 최적화하기 위해 사용할 수 있는 뛰어난 기술입니다.

**적용 대상:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]~[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

## <a name="persistent-memory-support-for-linux"></a>Linux에 대한 영구 메모리 지원

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[sqlv15](../includes/sssqlv15-md.md)]는 Linux에 영구 메모리(PMEM) 디바이스에 대한 지원을 추가하여 [영구 메모리](../linux/sql-server-linux-configure-pmem.md)에 배치된 데이터 및 트랜잭션 로그 파일의 전체 이해를 제공합니다.

**적용 대상:** [!INCLUDE[sqlv15](../includes/sssqlv15-md.md)]~[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
