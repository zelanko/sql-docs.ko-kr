---
title: SQL Server, Memory Manager 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Manager
- Memory Manager object
ms.assetid: dbf49000-eeb0-4e9c-a361-5092363920dc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 822cb494b7dce35ea965a2a53cab36785a38bc75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63250625"
---
# <a name="sql-server-memory-manager-object"></a>SQL Server, Memory Manager 개체
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 **memory Manager** 개체는 전체 서버 메모리 사용량을 모니터링 하는 카운터를 제공 합니다. 서버 메모리의 전반적인 사용량을 모니터링하여 사용자 작업 및 리소스 사용량을 측정하면 성능 병목 상태가 발생하는지 확인할 수 있습니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 사용하는 메모리를 모니터링하면 다음 사항을 확인할 수 있습니다.  
  
-   자주 액세스되는 데이터를 캐시에 저장하기 위한 실제 메모리가 부족하여 병목 상태가 발생하는지 여부. 메모리가 부족한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 디스크에서 데이터를 검색해야 합니다.  
  
-   메모리를 추가하거나 데이터 캐시 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 구조에 사용 가능한 메모리를 늘리면 쿼리 성능을 향상시킬 수 있는지 여부  
  
## <a name="memory-manager-counters"></a>Memory Manager 카운터  
 다음 표에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Manager** 카운터에 대해 설명합니다.  
  
|SQL Server Memory Manager 카운터|Description|  
|----------------------------------------|-----------------|  
|**연결 메모리 (KB)**|연결 유지 관리를 위해 서버에서 사용 중인 총 동적 메모리 양을 지정합니다.|  
|**데이터베이스 캐시 메모리 (KB)**|서버가 현재 데이터베이스 페이지 캐시에 사용 중인 메모리 양을 지정합니다.|  
|**사용 가능한 메모리 (KB)**|서버에서 현재 사용하지 않는 커밋된 메모리 양을 지정합니다.|  
|**부여 된 작업 영역 메모리 (KB)**|해시, 정렬, 대량 복사 및 인덱스 만들기 작업과 같은 실행 중인 프로세스에 현재 부여된 총 메모리 양을 지정합니다.|  
|**잠금 블록**|서버에서 현재 사용 중인 잠금 블록 수를 지정합니다. 이 값은 주기적으로 새로 고쳐집니다. 잠금 블록은 테이블, 페이지, 행과 같은 개별적인 잠금 리소스를 나타냅니다.|  
|**잠금 블록이 할당 됨**|할당된 잠금 블록의 현재 개수를 지정합니다. 서버를 시작할 때 할당된 잠금 블록과 할당된 잠금 소유자 블록의 개수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **잠금** 구성 옵션의 설정에 따라 결정됩니다. 잠금 블록이 더 필요하면 이 값을 늘리십시오.|  
|**잠금 메모리 (KB)**|서버가 잠금에 사용 중인 총 동적 메모리 양을 지정합니다.|  
|**잠금 소유자 블록**|서버에서 현재 사용 중인 잠금 소유자 블록 수를 지정합니다. 이 값은 주기적으로 새로 고쳐집니다. 잠금 소유자 블록은 개별 스레드의 개체 잠금에 대한 소유권을 나타냅니다. 그러므로 3개의 스레드가 페이지에 각각의 공유된 잠금을 가지면 소유자 블록도 3개 존재합니다.|  
|**잠금 소유자 블록이 할당 됨**|할당된 잠금 소유자 블록의 현재 개수를 지정합니다. 서버를 시작할 때 할당된 잠금 블록과 할당된 잠금 소유자 블록의 개수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **잠금** 구성 옵션의 설정에 따라 결정됩니다. 잠금 소유자 블록이 더 필요하면 이 값을 늘리십시오.|  
|**최대 작업 영역 메모리 (KB)**|해시, 정렬, 대량 복사, 인덱스 만들기 작업과 같은 실행 중인 프로세스에서 사용할 수 있는 최대 메모리 양을 나타냅니다.|  
|**처리 중인 메모리 부여**|부여된 작업 영역 메모리를 성공적으로 인식한 총 프로세스 수를 지정합니다.|  
|**메모리 부여 보류 중**|작업 공간 메모리 부여를 대기 중인 총 프로세스 수를 지정합니다.|  
|**최적화 프로그램 메모리 (KB)**|서버가 쿼리 최적화를 위해 사용 중인 총 동적 메모리 양을 지정합니다.|  
|**예약 된 서버 메모리 (KB)**|서버가 나중에 사용하기 위해 예약한 메모리 양을 지정합니다. 이 카운터는 **Granted Workspace Memory(KB)** 에 표시된 최초 부여 메모리 중 현재 사용되지 않는 메모리 양을 보여 줍니다.|  
|**SQL 캐시 메모리 (KB)**|서버가 동적 SQL 캐시를 위해 사용 중인 총 동적 메모리 양을 지정합니다.|  
|**도난 서버 메모리 (KB)**|서버가 데이터베이스 페이지가 아닌 다른 용도로 사용 중인 메모리 양을 지정합니다.|  
|**대상 서버 메모리 (KB)**|서버가 사용할 이상적인 메모리 양을 나타냅니다.|  
|**총 서버 메모리 (KB)**|서버가 메모리 관리자를 사용하여 커밋한 메모리 양을 지정합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, Buffer Manager 개체](sql-server-buffer-manager-object.md)   
 [dm_os_performance_counters &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
