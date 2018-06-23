---
title: 서버 메모리 서버 구성 옵션 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 76
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5ddbf4ccd432a7ba7ff9f4d946572dfcc6500dbc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180572"
---
# <a name="server-memory-server-configuration-options"></a>서버 메모리 서버 구성 옵션
  **최소 서버 메모리** 및 **최대 서버 메모리**의 두 가지 서버 메모리 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 사용하는 SQL Server 프로세스의 메모리 양(MB)을 다시 구성할 수 있습니다. 이 메모리는 SQL Server Memory Manager가 관리합니다.  
  
 **min server memory** 의 기본 설정은 0이고, **max server memory** 의 기본 설정은 2147483647MB입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경할 수 있습니다.  
  
> [!NOTE]  
>  **max server memory** 를 최소값으로 설정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 성능이 심각하게 손상되며 SQL Server를 시작하지 못할 수도 있습니다. 이 옵션을 변경한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 수 없으면 **–f** 시작 옵션을 사용하여 SQL Server를 시작하고 **max server memory** 를 이전 값으로 다시 설정합니다. 자세한 내용은 [Database Engine Service Startup Options](database-engine-service-startup-options.md)을(를) 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 동적으로 메모리를 사용하면 주기적으로 시스템을 쿼리하여 사용할 수 있는 메모리 양을 확인합니다. 사용 가능한 메모리를 이 수준으로 유지 관리하면 OS(운영 체제)에서 페이징을 방지합니다. 사용 가능한 메모리가 이보다 적은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 메모리를 OS로 해제합니다. 사용 가능한 메모리가 이보다 많은 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 더 많은 메모리를 할당할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 작업에 메모리가 더 필요한 경우에만 메모리를 추가합니다. 서버가 유휴 상태이면 가상 주소 공간 크기가 증가하지 않습니다.  
  
 현재 사용되는 메모리를 반환하는 쿼리에 대해서는 예제 B를 참조하세요. **최대 서버 메모리** 는 버퍼 풀, 컴파일 메모리, 모든 캐시, qe 메모리 부여, 잠금 관리자 메모리 및 clr 메모리를 포함한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 메모리 할당을 제어합니다(기본적으로 **sys.dm_os_memory_clerks**에 있는 모든 메모리 클럭). 스레드 스택용 메모리, 메모리 힙, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이외에 연결된 서버 공급자, 비 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DLL에서 할당한 모든 메모리는 max server memory로 제어되지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 메모리 알림 API **QueryMemoryResourceNotification** 을 사용하여 SQL Server Memory Manager가 메모리를 할당하고 해제하는 시기를 결정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 메모리를 동적으로 사용할 수 있게 하는 것이 좋지만 메모리 옵션을 수동으로 설정하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 액세스할 수 있는 메모리 양을 제한할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]메모리 양을 설정하기 전에 OS 및 기타 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스(컴퓨터가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]전용이 아닌 경우 다른 시스템 사용)에 필요한 메모리를 총 실제 메모리에서 빼서 적합한 메모리 설정을 결정합니다. 이러한 차이 값이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 할당할 수 있는 최대 메모리 양입니다.  
  
## <a name="setting-the-memory-options-manually"></a>메모리 옵션 수동 설정  
 **min server memory** 및 **max server memory** 를 설정하여 메모리 값 범위를 확장합니다. 이 방법은 시스템 또는 데이터베이스 관리자가 같은 컴퓨터에서 실행 중인 다른 응용 프로그램의 메모리 요구 사항과 관련하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 구성하는 경우 유용합니다.  
  
 **min server memory** 옵션을 사용하여 SQL Server Memory Manager가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 사용할 수 있는 최소 메모리 양을 보장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 시작할 때 **min server memory** 에 지정된 메모리의 양을 즉시 할당하지 않습니다. 그러나 클라이언트 로드 때문에 메모리 사용량이 이 값에 도달하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] min server memory **값을 줄이기 전에는** 가 메모리를 비울 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **min server memory**에 지정된 메모리 양을 할당하는 것이 보장되지 않습니다. 서버의 로드 때문에 **min server memory**에 지정된 메모리 양을 할당할 필요가 없는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 보다 적은 메모리로 실행됩니다.  
  
|OS 유형|최소 메모리 크기에 허용 **최대 서버 메모리**|  
|-------------|----------------------------------------------------------------|  
|32비트|64MB|  
|64비트|128MB|  
  
## <a name="how-to-configure-memory-options-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 메모리 옵션을 구성하는 방법  
 **최소 서버 메모리** 및 **최대 서버 메모리**의 두 가지 서버 메모리 옵션을 사용하여 SQL Server Memory Manager가 관리하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 메모리 양(MB)을 다시 구성할 수 있습니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경할 수 있습니다.  
  
### <a name="procedure-for-configuring-a-fixed-amount-of-memory"></a>고정 메모리 양을 구성하는 절차  
 **고정된 된 양의 메모리 설정:**  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
2.  **메모리** 노드를 클릭합니다.  
  
3.  **서버 메모리 옵션**에서 원하는 **최소 서버 메모리** 및 **최대 서버 메모리**양을 입력합니다.  
  
     기본 설정을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 사용할 수 있는 시스템 리소스에 따라 메모리 요구 사항을 동적으로 변경할 수 있습니다. **최소 서버 메모리** 의 기본 설정은 0이고 **최대 서버 메모리** 의 기본 설정은 2147483647(MB)입니다.  
  
## <a name="maximize-data-throughput-for-network-applications"></a>네트워크 응용 프로그램을 위해 데이터 처리량 최대화  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 시스템 메모리 사용을 최대화하려면 시스템에서 파일 캐싱용으로 사용되는 메모리 용량을 제한해야 합니다. 파일 시스템 캐시를 제한하려면 **파일 공유를 위해 데이터 처리량 최대화** 의 선택을 취소합니다. **사용 메모리 최소화** 또는 **균형**을 선택하여 최소 파일 시스템 캐시를 지정할 수 있습니다.  
  
#### <a name="to-check-the-current-setting-on-your-operating-system"></a>운영 체제의 현재 설정을 확인하려면  
  
1.  **시작**, **제어판**을 차례로 클릭한 다음 **네트워크 연결**, **로컬 영역 연결**을 차례로 두 번 클릭합니다.  
  
2.  **일반** 탭에서 **속성**을 클릭하고 **Microsoft 네트워크용 파일 및 프린터 공유**를 선택한 다음 **속성**을 클릭합니다.  
  
3.  **네트워크 응용 프로그램을 위해 데이터 처리량 최대화** 가 선택된 경우에는 다른 옵션을 선택하고 **확인**을 클릭한 다음 나머지 대화 상자를 닫습니다.  
  
## <a name="lock-pages-in-memory"></a>메모리의 페이지 잠금  
 이 Windows 정책은 데이터를 실제 메모리에 유지하는 프로세스를 사용하여 시스템이 디스크의 가상 메모리로 데이터를 페이징하지 않도록 방지할 수 있는 계정을 결정합니다. 메모리의 페이지를 잠그면 메모리를 디스크로 페이징할 때 서버가 계속해서 응답합니다. SQL Server **메모리의 페이지 잠금** 옵션은 32 비트 및 64 비트 인스턴스를 ON으로 설정 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Standard edition 및 경우에 더 높은 sqlservr.exe 실행 권한이 있는 계정에 부여한 Windows에서 "잠금 페이지 LPIM ("메모리) 사용자 권한이 있습니다. 이전 버전의 SQL Server에서는 SQL Server의 32비트 인스턴스에 대한 페이지 잠금 옵션을 설정하려면 sqlservr.exe 실행 권한이 있는 계정에 LPIM 사용자 권한이 있고 'awe_enabled' 구성 옵션을 ON으로 설정해야 합니다.  
  
 **에 대해** 메모리의 페이지 잠금 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]옵션을 사용하지 않도록 설정하려면 SQL Server 시작 계정에 대해 "메모리의 페이지 잠금" 사용자 권한을 제거합니다.  
  
### <a name="to-disable-lock-pages-in-memory"></a>메모리의 페이지 잠금을 사용하지 않도록 설정하려면  
 **Lock pages in memory 옵션을 사용 하지 않으려면:**  
  
1.  **시작** 메뉴에서 **실행**을 클릭합니다. 에 **열려** 상자에서 입력 `gpedit.msc`합니다.  
  
     **그룹 정책** 대화 상자가 열립니다.  
  
2.  **그룹 정책** 콘솔에서 **컴퓨터 구성**을 확장한 다음 **Windows 설정**을 확장합니다.  
  
3.  **보안 설정**을 확장한 다음 **로컬 정책**을 확장합니다.  
  
4.  **사용자 권한 할당** 폴더를 선택합니다.  
  
     세부 정보 창에 정책이 표시됩니다.  
  
5.  세부 정보 창에서 **메모리의 페이지 잠그기**를 두 번 클릭합니다.  
  
6.  **로컬 보안 정책 설정** 대화 상자에서 sqlservr.exe 실행 권한이 있는 계정을 선택하고 **제거**를 클릭합니다.  
  
## <a name="virtual-memory-manager"></a>가상 메모리 관리자  
 32비트 운영 체제는 4GB의 가상 주소 공간에 대한 액세스를 제공합니다. 2GB의 가상 메모리는 프로세스 전용이며 응용 프로그램에서만 사용 가능합니다. 2GB는 운영 체제용으로 예약됩니다. 모든 운영 체제 버전에는 운영 체제를 1GB로 제한하면서 3GB의 가상 주소 공간에 대한 액세스를 응용 프로그램에 제공할 수 있는 스위치가 있습니다. 스위치 메모리 구성을 사용하는 방법은 4GT(4기가바이트 튜닝)에 관한 Windows 설명서를 참조하세요. 64비트 운영 체제에서 32비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행 중인 경우 운영 체제 사용자가 사용할 수 있는 가상 주소 공간은 모두 4GB입니다.  
  
 주소 공간의 커밋된 영역은 Windows 가상 메모리 관리자(VMM)에 의해 사용할 수 있는 실제 메모리에 매핑됩니다.  
  
 운영 체제별 지원되는 실제 메모리의 양에 대한 자세한 내용은 Windows 설명서 "Windows 릴리스별 메모리 제한(Memory Limits for Windows Releases)"을 참조하세요.  
  
 가상 메모리 체계를 사용하면 실제 메모리가 과다 커밋되어 가상 메모리와 실제 메모리의 비율이 1:1을 초과할 수 있습니다. 그 결과 실제 메모리가 다양하게 구성된 컴퓨터에서 대용량 프로그램을 실행할 수 있습니다. 그러나 모든 프로세스의 현재 평균 설정을 합한 값보다 너무 많은 가상 메모리를 사용하면 성능이 떨어질 수 있습니다.  
  
 **min server memory** 및 **max server memory** 는 고급 옵션입니다. **sp_configure** 시스템 저장 프로시저를 사용하여 이러한 설정을 변경할 경우 **고급 옵션 표시** 를 1로 설정해야만 변경할 수 있습니다. 이러한 설정은 서버를 다시 시작하지 않아도 즉시 적용됩니다.  
  
## <a name="running-multiple-instances-of-sql-server"></a>여러 SQL Server 인스턴스 실행  
 여러 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스를 실행하는 경우 다음 3가지 방법으로 메모리를 관리할 수 있습니다.  
  
-   **max server memory** 를 사용하여 메모리 사용을 제어합니다. 허용되는 총 메모리가 컴퓨터의 실제 메모리 합계보다 크지 않도록 주의하여 각 인스턴스의 최대값을 설정합니다. 예상 작업이나 데이터베이스 크기에 비례하여 각 인스턴스에 메모리를 제공할 수 있습니다. 이 방법은 새 프로세스나 인스턴스 시작 시 여유 메모리를 즉시 사용할 수 있다는 장점이 있습니다. 단점은 모든 인스턴스를 실행하지 않는 경우 실행 중인 인스턴스가 남은 여유 메모리를 사용할 수 없다는 것입니다.  
  
-   **min server memory** 를 사용하여 메모리 사용을 제어합니다. 최소값의 합계가 컴퓨터의 실제 메모리 합계보다 1-2GB 작도록 각 인스턴스의 최소값을 설정합니다. 또한 해당 인스턴스의 예상 부하에 비례하여 이러한 최소값을 설정할 수 있습니다. 이 방법은 모든 인스턴스를 동시에 실행하지 않는 경우 실행 중인 인스턴스에서 남은 여유 메모리를 사용할 수 있다는 장점이 있습니다. 또한 이 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 적절한 양의 메모리가 최소한 할당되도록 하기 때문에 컴퓨터에 메모리를 많이 사용하는 다른 프로세스가 있을 때 유용합니다. 단점은 새 인스턴스나 다른 프로세스 시작 시, 특히 메모리를 해제하기 위해 수정된 페이지를 다시 데이터베이스에 써야 하는 경우 실행 중인 인스턴스가 메모리를 해제하는 데 오랜 시간이 걸린다는 것입니다.  
  
-   아무 작업도 하지 않습니다(권장되지 않음). 작업이 제공되는 첫 번째 인스턴스에서 모든 메모리를 할당합니다. 유휴 인스턴스나 나중에 시작된 인스턴스는 최소의 사용 가능한 메모리만 사용하여 실행될 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 인스턴스의 메모리 사용을 조절하지 않습니다. 그러나 모든 인스턴스는 Windows 메모리 알림 신호에 응답하여 해당 메모리 사용 공간의 크기를 조절합니다. Windows는 메모리 알림 API가 있는 응용 프로그램에서 메모리 균형을 유지하지 않고 단순히 시스템의 메모리 사용 가능 여부에 대한 전역 피드백만 제공합니다.  
  
 인스턴스를 다시 시작하지 않고 이러한 설정을 변경할 수 있으므로 사용 패턴에 가장 맞는 설정을 쉽게 찾을 수 있습니다.  
  
## <a name="providing-the-maximum-amount-of-memory-to-sql-server"></a>SQL Server에 최대 메모리 양 제공  
  
||32비트|64비트|  
|-|-------------|-------------|  
|기본 메모리|모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 프로세스 가상 주소 공간 제한까지 허용됩니다.<br /><br /> 2GB<br /><br /> 3GB **3gb** 부팅 매개 변수 *<br /><br /> W o w 64에서 4GB\*\*|모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 프로세스 가상 주소 공간 제한까지 허용됩니다.<br /><br /> 8TB(x64 아키텍처 사용)|  
  
 ***/3gb** 는 운영 체제 부팅 매개 변수입니다. 자세한 내용은 [MSDN 라이브러리](http://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)를 참조하세요.  
  
 * * WOW64 (Windows on Windows 64)는에 32 비트 모드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 비트 운영 체제에서 실행 됩니다. 자세한 내용은 [MSDN 라이브러리](http://go.microsoft.com/fwlink/?LinkID=10257&clcid=0x409)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="example-a"></a>예 1  
 다음 예에서는 `max server memory` 옵션을 4GB로 설정합니다.  
  
```  
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
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
## <a name="see-also"></a>관련 항목  
 [성능 모니터링 및 튜닝](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [서버 구성 옵션&#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
