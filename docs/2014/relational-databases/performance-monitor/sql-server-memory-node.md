---
title: SQL Server, Memory Node | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 55b28ba9-b6d5-4ea9-8103-db8a72f42982
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 32a2296fdb68e640ce8ebfc8dd9cdb351666b337
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250576"
---
# <a name="sql-server-memory-node"></a>SQL Server, Memory Node
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 **memory NODE** 개체는 NUMA 노드의 서버 메모리 사용량을 모니터링 하는 카운터를 제공 합니다.  
  
## <a name="memory-node-counters"></a>Memory Node 카운터  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Node** 카운터에 대해 설명합니다.  
  
|SQL Server Memory Manager 카운터|Description|  
|----------------------------------------|-----------------|  
|**데이터베이스 노드 메모리 (KB)**|서버가 현재 이 노드에서 데이터베이스 페이지에 사용 중인 메모리의 양을 지정합니다.|  
|**사용 가능한 노드 메모리 (KB)**|서버가 이 노드에서 사용하고 있지 않은 메모리의 양을 지정합니다.|  
|**외부 노드 메모리 (KB)**|이 노드의 비-NUMA 로컬 메모리의 양을 지정합니다.|  
|**도난당 한 메모리 노드 (KB)**|서버가 이 노드에서 데이터베이스 페이지가 아닌 다른 용도로 사용 중인 메모리의 양을 지정합니다.|  
|**대상 노드 메모리**|이 노드에 적합한 메모리의 양을 지정합니다.|  
|**총 노드 메모리**|서버가 이 노드에서 커밋한 총 메모리의 양을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, Buffer Manager 개체](sql-server-buffer-manager-object.md)   
 [dm_os_performance_counters &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
