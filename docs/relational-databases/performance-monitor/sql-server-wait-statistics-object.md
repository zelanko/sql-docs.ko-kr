---
title: SQL Server, Wait Statistics 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Wait Statistics object
- SQLServer:Wait Statistics
ms.assetid: cb7f917d-4291-4115-9b78-ee7692ebbb2d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b5b9a2ccdd73150eeaa1dda8403c4b73aed03009
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758916"
---
# <a name="sql-server-wait-statistics-object"></a>SQL Server, Wait Statistics 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **SQLServer:Wait Statistics** 성능 개체는 대기 상태에 대한 정보를 보고하는 성능 카운터를 포함합니다.  
  
 다음 표에서는 Wait Statistics 개체가 포함하는 카운터를 나열합니다.  
  
|SQL Server Wait Statistics 카운터|Description|  
|-----------------------------------------|-----------------|  
|**Lock waits**|잠금을 기다리는 프로세스에 대한 통계입니다.|  
|**Log buffer waits**|로그 버퍼 사용을 기다리는 프로세스에 대한 통계입니다.|  
|**Log write waits**|로그 버퍼 작성을 기다리는 프로세스에 대한 통계입니다.|  
|**Memory grant queue waits**|메모리 부여를 기다리는 프로세스에 대한 통계입니다.|  
|**Network IO waits**|네트워크 I/O 대기와 관련된 통계입니다.|  
|**Non-Page latch waits**|비페이지 래치와 관련된 통계입니다.|  
|**Page IO latch waits**|페이지 I/O 래치와 관련된 통계입니다.|  
|**Page latch waits**|I/O 래치를 제외한 페이지 래치와 관련된 통계입니다.|  
|**Thread-safe memory objects waits**|스레드로부터 안전한 메모리 할당자를 기다리는 프로세스에 대한 통계입니다.|  
|**Transaction ownership waits**|트랜잭션에 대한 액세스를 동기화하는 프로세스와 관련된 통계입니다.|  
|**Wait for the worker**|작업자 활성화를 기다리는 프로세스와 관련된 통계입니다.|  
|**Workspace synchronization waits**|작업 영역에 대한 액세스를 동기화하는 프로세스와 관련된 통계입니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|항목|Description|  
|----------|-----------------|  
|**평균 대기 시간(밀리초)**|선택한 유형에 대한 평균 대기 시간입니다.|  
|**초당 누적 대기 시간(밀리초)**|선택한 유형에 대한 초당 대기 시간 집계입니다.|  
|**진행 중인 대기 작업**|선택한 유형에 대한 현재 대기 중인 프로세스의 수입니다.|  
|**초당 시작된 대기 작업**|선택한 대기 유형에 대한 초당 시작된 대기 작업의 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
