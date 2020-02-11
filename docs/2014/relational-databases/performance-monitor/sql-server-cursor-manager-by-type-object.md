---
title: SQL Server, Cursor Manager by Type 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35fa15dc6651d8bfd9b6d32cafd00cd47698560b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68206976"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>SQL Server, Cursor Manager by Type 개체
  **SQLServer:Cursor Manager by Type** 개체는 커서 모니터링에 사용되는 카운터를 유형별로 그룹화하여 제공합니다.  
  
 다음 표에서는 SQL Server **Cursor Manager by Type** 카운터에 대해 설명합니다.  
  
|Cursor Manager by Type 카운터|Description|  
|-------------------------------------|-----------------|  
|**Active cursors**|활성 커서 수입니다.|  
|**Cache Hit Ratio**|캐시 적중 횟수와 조회 간 비율입니다.|  
|**Cached Cursor Counts**|캐시에 있는 특정 유형의 커서 수입니다.|  
|**Cursor Cache Use Count/sec**|각 유형의 캐시된 커서가 사용된 시간입니다.|  
|**Cursor memory usage**|커서가 사용한 메모리 양입니다(KB).|  
|**Cursor Requests/sec**|서버에서 받은 SQL 커서 요청 수입니다.|  
|**Cursor worktable usage**|커서에 사용되는 작업 테이블 수입니다.|  
|**Number of active cursor plans**|커서 계획 수입니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|Cursor Manager 인스턴스|Description|  
|-----------------------------|-----------------|  
|**_Total**|모든 커서에 대한 정보입니다.|  
|**API Cursor**|API 커서 정보만 해당됩니다.|  
|**TSQL Global Cursor**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 전역 커서 정보만 해당됩니다.|  
|**TSQL Local Cursor**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 로컬 커서 정보만 해당됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
