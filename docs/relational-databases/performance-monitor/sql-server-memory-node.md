---
title: SQL Server, Memory Node | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: cfa8eb11b89919a3a1f151a0deddd24528631fe1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775792"
---
# <a name="sql-server-memory-node"></a>SQL Server, Memory Node
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Microsoft **의** Memory Node [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체는 NUMA 노드의 서버 메모리 사용량을 모니터링하는 카운터를 제공합니다.  
  
## <a name="memory-node-counters"></a>Memory Node 카운터  
 다음 테이블에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** 카운터에 대해 설명합니다.  
  
|SQL Server Memory Manager 카운터|Description|  
|----------------------------------------|-----------------|  
|**Database Node Memory(KB)**|서버가 현재 이 노드에서 데이터베이스 페이지에 사용 중인 메모리의 양을 지정합니다.|  
|**Free Node Memory(KB)**|서버가 이 노드에서 사용하고 있지 않은 메모리의 양을 지정합니다.|  
|**Foreign Node Memory(KB)**|이 노드의 비-NUMA 로컬 메모리의 양을 지정합니다.|  
|**Stolen Memory Node(KB)**|서버가 이 노드에서 데이터베이스 페이지가 아닌 다른 용도로 사용 중인 메모리의 양을 지정합니다.|  
|**Target Node Memory**|이 노드에 적합한 메모리의 양을 지정합니다.|  
|**Total Node Memory**|서버가 이 노드에서 커밋한 총 메모리의 양을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Buffer Manager 개체](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
