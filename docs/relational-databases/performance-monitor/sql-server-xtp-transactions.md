---
title: SQL Server의 XTP 트랜잭션 | Microsoft 문서
description: SQL Server의 메모리 내 OLTP 트랜잭션과 관련된 카운터를 포함하는 SQL Server XTP 트랜잭션 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 443d67e4-1c7f-41d7-b18d-2d657f58c22a
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 384e2feb7d638a7ff8cad4e22346ba58369cc6aa
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458073"
---
# <a name="sql-server-xtp-transactions"></a>SQL Server XTP 트랜잭션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL Server XTP 트랜잭션 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 메모리 내 OLTP 트랜잭션과 관련된 카운터가 포함됩니다.  
  
 이 표에서는 **SQL Server XTP 트랜잭션** 카운터에 대해 설명합니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|**Cascading aborts/sec**|커밋 종속성 롤백으로 인해 롤백되는 초당 트랜잭션 수입니다(평균).|  
|**Commit dependencies taken/sec**|트랜잭션에 의해 사용되는 초당 커밋 종속성 수입니다(평균).|  
|**Read-only transactions prepared/sec**|커밋 처리를 위해 준비된 초당 읽기 전용 트랜잭션 수입니다.|  
|**Save point refreshes/sec**|저장점을 "새로 고친" 초당 횟수입니다(평균). 저장점 새로 고침은 기존 저장점이 트랜잭션의 수명에서 현재 지점으로 재설정될 때 수행됩니다.|  
|**Save point rollbacks/sec**|트랜잭션이 저장점으로 롤백된 초당 횟수입니다(평균).|  
|**Save points created /sec**|초당 생성된 저장점 수입니다(평균).|  
|**Transaction validation failure/sec**|유효성 검사 처리에 실패한 초당 트랜잭션 수입니다(평균).|  
|**Transactions aborted by user/sec**|사용자에 의해 중단된 초당 트랜잭션 수입니다(평균).|  
|**Transactions aborted/sec**|사용자 및 시스템에 의해 중단된 초당 트랜잭션 수입니다(평균).|  
|**Transactions created/sec**|시스템에서 생성된 초당 트랜잭션 수입니다(평균).<br /><br /> XTP 트랜잭션은 디스크 기반 트랜잭션과 다르게 계산됩니다(Databases:Transactions/sec에 반영됨). 예를 들어, created/sec 트랜잭션은 read/only 트랜잭션을 계산하지만 Databases:Transactions/sec는 그렇지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
