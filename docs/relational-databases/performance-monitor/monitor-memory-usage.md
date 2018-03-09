---
title: "메모리 사용량 모니터링 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 18061fa8a59ab5cd5d86a7505162e5148767b9c7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="monitor-memory-usage"></a>메모리 사용량 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 주기적으로 모니터링하여 메모리 사용이 일반적인 범위를 벗어나지 않는지 확인할 수 있습니다.  
  
 메모리 부족 상태를 모니터링하려면 다음 개체 카운터를 사용하세요.  
  
-   **Memory: Available Bytes**  
  
-   **Memory: Pages/sec**  
  
 **Available Bytes** 카운터는 현재 프로세스에 사용할 수 있는 메모리의 바이트 수를 나타냅니다. **Pages/sec** 카운터는 하드 페이지 폴트 때문에 디스크에서 가져오거나 작업 집합 내의 디스크 여유 공간에 쓴 페이지 수를 나타냅니다.  
  
 **Available Bytes** 카운터 값이 작으면 컴퓨터 전체 메모리가 부족하거나 응용 프로그램이 메모리를 해제하지 않는다는 의미입니다. **Pages/sec** 카운터의 비율이 높으면 페이징이 과도하다는 의미입니다. 디스크 작업의 원인이 페이징이 아닌 것을 확인하려면 **Memory: Page Faults/sec** 카운터를 모니터링하세요.  
  
 컴퓨터에 사용 가능한 메모리가 충분하더라도 페이징 및 그로 인한 페이지 폴트 비율은 낮은 것이 일반적입니다. Microsoft Windows VMM(Virtual Memory Manager)은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 다른 프로세스의 작업 집합 크기를 줄일 때 이러한 프로세스에서 페이지를 가져옵니다. 이 VMM 작업으로 인해 페이지 폴트가 발생할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 나 다른 프로세스가 과도한 페이징의 원인인지 확인하려면 **프로세스 인스턴스의** Process: Page Faults/sec [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 카운터를 모니터링하세요.  
  
 과도한 페이징을 해결하는 방법은 Windows 운영 체제 설명서를 참조하세요.  
  
## <a name="isolating-memory-used-by-sql-server"></a>SQL Server가 사용하는 메모리 격리  
 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 메모리가 더 필요할 경우 운영 체제를 쿼리하여 실제 여유 메모리가 사용 가능한지 확인하고 사용 가능한 메모리를 사용합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 현재 할당된 메모리가 필요하지 않은 경우 운영 체제에서 사용할 수 있도록 해당 메모리를 해제합니다. 그러나 **minservermemory**및 **maxservermemory** 서버 구성 옵션을 사용하여 메모리를 동적으로 사용하도록 옵션을 재정의할 수 있습니다. 자세한 내용은 [서버 메모리 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용하는 메모리의 양을 모니터링하려면 다음 성능 카운터를 검사하세요.  
  
-   **Process: Working Set**  
  
-   **SQL Server: Buffer Manager: Buffer Cache Hit Ratio**  
  
-   **SQL Server: Buffer Manager: Database Pages**  
  
-   **SQL Server: Memory Manager: Total Server Memory (KB)**  
  
 **WorkingSet** 카운터는 프로세스에서 사용하는 메모리의 양을 나타냅니다. 이 숫자가 계속 **min server memory** 및 **max server memory** 서버 옵션에 설정된 메모리의 양보다 작으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 메모리를 너무 많이 사용하도록 구성된 것입니다.  
  
 **Buffer Cache Hit Ratio** 카운터는 응용 프로그램에 따라 다릅니다. 그러나 90% 이상의 비율이 알맞습니다. 이 값이 90%보다 크게 유지될 때까지 메모리를 추가하세요. 값이 90%보다 크면 데이터 캐시를 통해 모든 데이터 요청의 90% 이상이 충족된 것입니다.  
  
 **TotalServerMemory (KB)** 카운터가 컴퓨터의 실제 메모리 양과 비교하여 계속 높게 나타나면 메모리를 추가해야 합니다.  
  
## <a name="determining-current-memory-allocation"></a>현재 메모리 할당 확인  
 다음 쿼리는 현재 할당된 메모리에 대한 정보를 반환합니다.  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
