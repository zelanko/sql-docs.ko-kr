---
title: 성능 문제 격리 | Microsoft 문서
description: SQL Server Profiler 및 시스템 모니터를 사용하여 Transact-SQL, 애플리케이션 관련 문제, 하드웨어 및 시스템 관련 문제를 모니터링하고 해결하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- isolating performance problems [SQL Server]
- monitoring performance [SQL Server], isolating problems
- database monitoring [SQL Server], isolating problems
- tuning databases [SQL Server], isolating problems
- monitoring server performance [SQL Server], isolating problems
- database performance [SQL Server], isolating problems
- server performance [SQL Server], isolating problems
ms.assetid: 2eb425cb-9166-4027-ae08-c8fc2d236f44
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ed6728b164ab0d8562965935ad869c767a8a9961
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460326"
---
# <a name="isolate-performance-problems"></a>성능 문제 격리
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  도구를 하나씩 사용하는 것보다는 여러 개의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Microsoft Windows 도구를 함께 사용하여 데이터베이스 성능 문제를 격리하는 것이 효과적입니다. 예를 들어 실행 계획이라고도 하는 그래픽 실행 계획 기능을 사용하여 쿼리 하나에 발생한 교착 상태를 즉시 인식할 수 있습니다 그러나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 Windows의 모니터링 기능을 함께 사용하면 다른 성능 문제도 쉽게 인식할 수 있습니다.  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 사용하면 Transact-SQL 및 애플리케이션 관련 문제를 모니터링하고 해결할 수 있습니다. 시스템 모니터를 사용하면 하드웨어와 그 밖의 시스템 관련 문제를 모니터링할 수 있습니다.  
  
 문제를 해결하려면 다음 영역을 모니터링하십시오.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 또는 사용자 애플리케이션이 제출한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 일괄 처리  
  
-   차단 잠금이나 교착 상태와 같은 사용자 동작  
  
-   디스크 사용과 같은 하드웨어 동작  
  
 다음과 같은 문제가 있을 수 있습니다.  
  
-   잘못 작성된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 비롯한 애플리케이션 개발 오류  
  
-   디스크나 네트워크 관련 오류와 같은 하드웨어 오류  
  
-   잘못 지정된 데이터베이스로 인한 과도한 차단  
  
## <a name="tools-for-common-performance-problems"></a>일반적인 성능 문제를 위한 도구  
 각 도구를 사용하여 모니터링하거나 튜닝할 성능 문제를 신중하게 선택하는 것 역시 중요합니다. 도구와 유틸리티는 해결할 성능 문제의 유형에 따라 달라집니다.  
  
 다음 항목에서는 다양한 모니터링 및 튜닝 도구와 이러한 도구로 해결할 수 있는 문제에 대해 설명합니다.  
  
 [병목 상태 식별](../../relational-databases/performance/identify-bottlenecks.md)  
  
 [메모리 사용량 모니터링](../../relational-databases/performance-monitor/monitor-memory-usage.md)  
  
  
