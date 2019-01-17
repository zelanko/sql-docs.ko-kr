---
title: 서버 메모리 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Virtual Memory Manager
- max server memory option
- virtual memory [SQL Server]
- VMM
- server memory options [SQL Server]
- servers [SQL Server], memory
- buffer pools [SQL Server]
- min server memory option
- manual memory options [SQL Server]
- memory [SQL Server], servers
ms.assetid: 29ce373e-18f8-46ff-aea6-15bbb10fb9c2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b1342d023b1edc828105dbbda2e18b0ca09877de
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591647"
---
# <a name="server-memory-server-configuration-options"></a>서버 메모리 서버 구성 옵션
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**최소 서버 메모리** 및 **최대 서버 메모리**의 두 가지 서버 메모리 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용하는 SQL Server 프로세스의 메모리 양(MB)을 다시 구성할 수 있습니다. 이 메모리는 SQL Server Memory Manager가 관리합니다.  
  
**min server memory**의 기본 설정은 0이고 **max server memory**의 기본 설정은 2,147,483,647(MB)입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경할 수 있습니다. 자세한 내용은 [동적 메모리 관리](../../relational-databases/memory-management-architecture-guide.md#dynamic-memory-management)을 참조하세요. 

**max server memory** 에 지정할 수 있는 최소 메모리 양은 128MB입니다.
  
> [!IMPORTANT]  
> **max server memory** 값을 너무 높게 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 단일 인스턴스가 동일한 호스트에서 호스팅되는 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 메모리를 경쟁해야 할 수 있습니다. 그러나 이 값을 너무 낮게 설정하면 메모리 부족 및 성능 문제가 발생할 수 있습니다. **max server memory** 를 최소값으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작하지 못할 수도 있습니다. 이 옵션을 변경한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작할 수 없으면 **_–f_** 시작 옵션을 사용하여 시작하고 **최대 서버 메모리**를 이전 값으로 다시 설정합니다. 자세한 내용은 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)을(를) 참조하세요.  
    
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 메모리를 동적으로 사용할 수 있지만 메모리 옵션을 수동으로 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 액세스할 수 있는 메모리 양을 제한할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 메모리 양을 설정하기 전에 OS, max_server_memory setting에 의해 제어되지 않는 메모리 할당, 기타 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스(컴퓨터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전용이 아닌 경우 다른 시스템 사용)에 필요한 메모리를 총 실제 메모리에서 빼서 적합한 메모리 설정을 결정합니다. 이러한 차이 값이 현재 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 할당할 수 있는 최대 메모리 양입니다.  
 
## <a name="setting-the-memory-options-manually"></a>메모리 옵션 수동 설정  
서버 옵션 **min server memory** 및 **max server memory**를 설정하여 메모리 값 범위를 확장합니다. 이 방법은 시스템 또는 데이터베이스 관리자가 다른 애플리케이션의 메모리 요구 사항 또는 동일한 호스트에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스와 함께 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 구성하는 데 유용합니다.

> [!NOTE]
> **min server memory** 및 **max server memory** 는 고급 옵션입니다. **sp_configure** 시스템 저장 프로시저를 사용하여 이러한 설정을 변경할 경우 **고급 옵션 표시** 를 1로 설정해야만 변경할 수 있습니다. 이러한 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
<a name="min_server_memory"></a> **min_server_memory** 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Memory Manager가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 사용할 수 있는 최소 메모리 양을 보장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 시작할 때 **min server memory** 에 지정된 메모리의 양을 즉시 할당하지 않습니다. 그러나 클라이언트 로드 때문에 메모리 사용량이 이 값에 도달하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] min server memory **값을 줄이기 전에는** 가 메모리를 비울 수 없습니다. 예를 들어 동일한 호스트에 여러 인스턴스 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 동시에 존재할 수 있는 경우 인스턴스의 메모리를 예약하기 위해 max_server_memory 대신 min_server_memory 매개 변수를 설정합니다. 또한 가상 환경에서 min_server_memory 값을 설정하여 기본 호스트의 메모리 압력을 가하는 것은 게스트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가상 머신(VM)의 버퍼 풀에서 수용 가능한 성능에 필요한 것 이상으로 메모리를 할당 해제하지 않도록 하는 데 필수적입니다.
 
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **min server memory**에 지정된 메모리 양을 할당하는 것이 보장되지 않습니다. 서버의 로드 때문에 **min server memory**에 지정된 메모리 양을 할당할 필요가 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 보다 적은 메모리로 실행됩니다.  
  
<a name="max_server_memory"></a> OS가 유해 메모리 압력을 겪지 않도록 **max_server_memory**를 사용합니다. 최대 서버 메모리 구성을 설정하려면 메모리 요구 사항을 결정하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스의 전체 소비량을 모니터링합니다. 단일 인스턴스에 대해 이러한 계산을 통해보다 정확한 결과를 얻으려면
 -  전체 OS 메모리에서 1GB-4GB를 OS에 예약합니다.
 -  그런 다음,  **_스택 크기 <sup>1</sup> \* 계산된 최대 작업자 스레드 수 <sup>2</sup> + -g 시작 매개 변수 <sup>3</sup>_**(또는 *-g*가 설정되지 않은 경우 기본적으로 256MB)으로 구성된 **최대 서버 메모리** 컨트롤 외부의 잠재적 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 할당량을 뺍니다. 남은 일은 단일 인스턴스 설정을 위한 max_server_memory를 설정하는 것입니다.
 
<sup>1</sup> 아키텍처당 스레드 스택 크기에 대한 내용은 [ 메모리 관리 아키텍처 가이드 ](../../relational-databases/memory-management-architecture-guide.md#stacksizes)를 참조하세요.

<sup>2</sup> 현재 호스트에서 선호도가 높은 CPU의 지정된 수에 대해 계산된 기본 작업자 스레드에 대한 내용은 [max worker threads 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) 방법에 대한 설명서 페이지를 참조하세요.

<sup>3</sup> *-g* 시작 매개 변수에 대한 자세한 내용은 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)의 설명서 페이지를 참조하세요.

## <a name="how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd"></a>[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 메모리 옵션을 구성하는 방법  
**min server memory** 및 **max server memory**의 두 가지 서버 메모리 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Memory Manager가 관리하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 메모리 양(MB)을 다시 구성할 수 있습니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경할 수 있습니다.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory-not-recommended"></a>고정 메모리 양을 구성하는 절차(권장되지 않음)  
고정 메모리 크기를 설정하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **메모리** 노드를 클릭합니다.  
  
3.  **서버 메모리 옵션**에서 원하는 **최소 서버 메모리** 및 **최대 서버 메모리**와 동일한 양을 입력합니다.  
  
     기본 설정을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경할 수 있습니다. **최대 서버 메모리**는 [위에서 설명한 대로](#max_server_memory) 설정하는 것이 좋습니다. 
  
## <a name="lock-pages-in-memory-lpim"></a>메모리의 페이지 잠금(LPIM) 
이 Windows 정책은 데이터를 실제 메모리에 유지하는 프로세스를 사용하여 시스템이 디스크의 가상 메모리로 데이터를 페이징하지 않도록 방지할 수 있는 계정을 결정합니다. 메모리의 페이지를 잠그면 메모리를 디스크로 페이징할 때 서버가 계속해서 응답합니다. sqlservr.exe 실행 권한이 있는 계정에 Windows *메모리의 페이지 잠금*(LPIM) 사용자 권한이 부여된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard 이상 버전의 인스턴스에서 **메모리의 페이지 잠금** 옵션은 ON으로 설정됩니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대해 **메모리의 페이지 잠금** 옵션을 사용하지 않도록 설정하려면 권한을 가진 계정에 대해 *메모리의 페이지 잠금* 사용자 권한을 제거하여 sqlservr.exe 시작 계정([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 계정)을 실행합니다.  
 
이 옵션을 설정해도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [동적 메모리 관리](../../relational-databases/memory-management-architecture-guide.md#dynamic-memory-management)에는 영향을 미치지 않으므로 다른 메모리 클럭의 요청에 따라 확장 또는 축소할 수 있습니다. *메모리의 페이지 잠금* 사용자 권한을 사용할 때 **max server memory**를 에 대한 상한값을 [위에서 설명한 대로](#max_server_memory) 설정하는 것이 좋습니다.

> [!IMPORTANT]
> 이 옵션의 설정은 필요한 경우, 즉 sqlservr 프로세스가 페이징 아웃되고 있다는 징후가 있는 경우에만 사용해야 합니다. 이 경우 오류 17890이 아래 `A significant part of sql server process memory has been paged out. This may result in a performance degradation. Duration: #### seconds. Working set (KB): ####, committed (KB): ####, memory utilization: ##%.` 예제와 유사한 Errorlog에 보고됩니다.
> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]부터 [추적 플래그 845](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)는 페이지 잠금을 사용하는 데 Standard Edition가 필요하지 않습니다. 
  
### <a name="to-enable-lock-pages-in-memory"></a>메모리의 페이지 잠금을 사용하려면  
메모리의 페이지 잠금 옵션을 사용하려면  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다. **열기** 상자에 **gpedit.msc**를 입력합니다.  
  
     **그룹 정책** 대화 상자가 열립니다.  
  
2.  **그룹 정책** 콘솔에서 **컴퓨터 구성**을 확장한 다음 **Windows 설정**을 확장합니다.  
  
3.  **보안 설정**을 확장한 다음 **로컬 정책**을 확장합니다.  
  
4.  **사용자 권한 할당** 폴더를 선택합니다.  
  
     세부 정보 창에 정책이 표시됩니다.  
  
5.  세부 정보 창에서 **메모리의 페이지 잠그기**를 두 번 클릭합니다.  
  
6.  **로컬 보안 정책 설정** 대화 상자에서 sqlservr.exe 실행 권한이 있는 계정을 추가합니다([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 계정).  
  
## <a name="running-multiple-instances-of-includessnoversionincludesssnoversion-mdmd"></a>여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 실행  
 여러 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스를 실행하는 경우 다음 3가지 방법으로 메모리를 관리할 수 있습니다.  
  
-   **max server memory**를 사용하여 [위에서 설명한 대로](#max_server_memory) 메모리 사용을 제어합니다. 허용되는 총 메모리가 컴퓨터의 실제 메모리 합계보다 크지 않도록 주의하여 각 인스턴스의 최대값을 설정합니다. 예상 작업이나 데이터베이스 크기에 비례하여 각 인스턴스에 메모리를 제공할 수 있습니다. 이 방법은 새 프로세스나 인스턴스 시작 시 여유 메모리를 즉시 사용할 수 있다는 장점이 있습니다. 단점은 모든 인스턴스를 실행하지 않는 경우 실행 중인 인스턴스가 남은 여유 메모리를 사용할 수 없다는 것입니다.  
  
-   **min server memory**를 사용하여 [위에서 설명한 대로](#min_server_memory) 메모리 사용을 제어합니다. 최소값의 합계가 컴퓨터의 실제 메모리 합계보다 1-2GB 작도록 각 인스턴스의 최소값을 설정합니다. 또한 해당 인스턴스의 예상 부하에 비례하여 이러한 최소값을 설정할 수 있습니다. 이 방법은 모든 인스턴스를 동시에 실행하지 않는 경우 실행 중인 인스턴스에서 남은 여유 메모리를 사용할 수 있다는 장점이 있습니다. 또한 이 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 적절한 양의 메모리가 최소한 할당되도록 하기 때문에 컴퓨터에 메모리를 많이 사용하는 다른 프로세스가 있을 때 유용합니다. 단점은 새 인스턴스나 다른 프로세스 시작 시, 특히 메모리를 해제하기 위해 수정된 페이지를 다시 데이터베이스에 써야 하는 경우 실행 중인 인스턴스가 메모리를 해제하는 데 오랜 시간이 걸린다는 것입니다.  
  
-   아무 작업도 하지 않습니다(권장되지 않음). 작업이 제공되는 첫 번째 인스턴스에서 모든 메모리를 할당합니다. 유휴 인스턴스나 나중에 시작된 인스턴스는 최소의 사용 가능한 메모리만 사용하여 실행될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 인스턴스의 메모리 사용을 조절하지 않습니다. 그러나 모든 인스턴스는 Windows 메모리 알림 신호에 응답하여 해당 메모리 사용 공간의 크기를 조절합니다. Windows는 메모리 알림 API가 있는 애플리케이션에서 메모리 균형을 유지하지 않고 단순히 시스템의 메모리 사용 가능 여부에 대한 전역 피드백만 제공합니다.  
  
 인스턴스를 다시 시작하지 않고 이러한 설정을 변경할 수 있으므로 사용 패턴에 가장 맞는 설정을 쉽게 찾을 수 있습니다.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>SQL Server에 최대 메모리 양 제공  
모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 프로세스 가상 주소 공간 제한까지 메모리를 구성할 수 있습니다. 자세한 내용은 [Windows 및 Windows Server 릴리스에 대한 메모리 제한](/windows/desktop/Memory/memory-limits-for-windows-releases#physical_memory_limits_windows_server_2016)을 참조하세요.
  
## <a name="examples"></a>예  
  
### <a name="example-a"></a>예 1  
 다음 예에서는 `max server memory` 옵션을 4GB로 설정합니다.  
  
```sql  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'max server memory', 4096;  
GO  
RECONFIGURE;  
GO  
```  
  
### <a name="example-b-determining-current-memory-allocation"></a>예 B. 현재 메모리 할당 확인  
 다음 쿼리는 현재 할당된 메모리에 대한 정보를 반환합니다.  
  
```sql  
SELECT 
  physical_memory_in_use_kb/1024 AS sql_physical_memory_in_use_MB, 
    large_page_allocations_kb/1024 AS sql_large_page_allocations_MB, 
    locked_page_allocations_kb/1024 AS sql_locked_page_allocations_MB,
    virtual_address_space_reserved_kb/1024 AS sql_VAS_reserved_MB, 
    virtual_address_space_committed_kb/1024 AS sql_VAS_committed_MB, 
    virtual_address_space_available_kb/1024 AS sql_VAS_available_MB,
    page_fault_count AS sql_page_fault_count,
    memory_utilization_percentage AS sql_memory_utilization_percentage, 
    process_physical_memory_low AS sql_process_physical_memory_low, 
    process_virtual_memory_low AS sql_process_virtual_memory_low
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>참고 항목  
 [메모리 관리 아키텍처 가이드](../../relational-databases/memory-management-architecture-guide.md)   
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [데이터베이스 엔진 서비스 시작 옵션](../../database-engine/configure-windows/database-engine-service-startup-options.md)   
 [버전 및 SQL Server 2016의 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2016.md#Cross-BoxScaleLimits)   
 [버전 및 SQL Server 2017의 지원되는 기능](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)   
 [Linux의 SQL Server 2017 버전 및 지원되는 기능](../../linux/sql-server-linux-editions-and-components-2017.md#Cross-BoxScaleLimits)   
 [Windows 및 Windows Server 릴리스에 대한 메모리 제한](/windows/desktop/Memory/memory-limits-for-windows-releases)
 
