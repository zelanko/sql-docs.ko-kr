---
title: SQL Server, ExecStatistics 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:ExecStatistics
- ExecStatistics object
ms.assetid: 4f8557a8-345f-4622-a8a5-763a0388ad94
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 258aaee37e6e0c6bbbb0a43326a21c80712e9749
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773111"
---
# <a name="sql-server-execstatistics-object"></a>SQL Server, ExecStatistics 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft SQL Server의 **SQLServer:ExecStatistics** 개체는 다양한 실행을 모니터링하는 카운터를 제공합니다.  
  
 이 표에서는 SQL Server **Exec Statistics** 카운터를 설명합니다.  
  
|SQL Server Exec Statistics 카운터|설명|  
|-----------------------------------------|-----------------|  
|**Distributed Query**|분산 쿼리의 실행과 관련된 통계입니다.|  
|**DTC calls**|DTC 호출의 실행과 관련된 통계입니다.|  
|**Extended Procedures**|확장 프로시저의 실행과 관련된 통계입니다.|  
|**OLEDB calls**|OLEDB 호출의 실행과 관련된 통계입니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|항목|설명|  
|----------|-----------------|  
|**평균 실행 시간(ms)**|선택된 실행 유형의 평균 실행 시간입니다.|  
|**초당 누적 실행 시간(ms)**|선택된 실행 유형의 초당 총 실행 시간입니다.|  
|**진행 중인 실행 작업**|선택된 실행 유형의 진행 중인 실행 작업 수입니다.|  
|**초당 시작된 실행 작업**|선택된 실행 유형의 초당 시작된 실행 작업 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
