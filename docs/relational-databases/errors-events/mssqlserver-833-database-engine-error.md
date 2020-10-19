---
description: MSSQLSERVER_833
title: MSSQLSERVER_833 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 132e33d7bf2b03df21a1d6a3475ca625675b3328
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988769"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sql-asdbmi.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|833|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|BUF_LONG_IO|  
|메시지 텍스트|SQL Server에서 데이터베이스 `[%ls] (%d)`의 파일 [%ls]을(를) 완료하는 데 %d초보다 더 오래 걸린 I/O 요청이 %d개 발견되었습니다.  OS 파일 핸들은 0x%p입니다.  가장 최근의 시간 초과 I/O의 오프셋은 %#016I64x입니다.|  
  
## <a name="explanation"></a>설명  
이 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 디스크에서 읽기 또는 쓰기 요청을 실행하여 해당 요청이 반환되는 데 15초 이상 소요되었음을 나타냅니다. 이 오류는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 보고하고 I/O 하위 시스템에 문제가 있음을 나타냅니다. 이 메시지와 관련된 다른 증상(PAGEIOLATCH 대기의 높은 대기 시간, 시스템 이벤트 로그의 경고 또는 오류, 시스템 모니터 카운터의 디스크 대기 시간 이슈 표시 등)도 나타날 수 있습니다. [sys.dm_io_virtual_file_stats](../system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md)를 모니터링하고 스토리지 처리량에 적합한 스토리지 계층 및 IOPS를 선택합니다. 
  
### <a name="possible-causes"></a>가능한 원인  
이 문제는 운영 체제 성능 문제, 하드웨어 오류, 펌웨어 오류, 디바이스 드라이버 문제 또는 데이터베이스 파일의 I/O 프로세스 또는 스토리지 경로에서 필터 드라이버 개입으로 인해 발생할 수 있습니다. SQL Server는 I/O 요청을 시작한 시간을 기록하고 I/O가 완료된 시간을 기록합니다. 차이가 15초 이상이면 이 상태가 검색됩니다. 이는 SQL Server는 이 메시지가 설명하고 보고하는 지연된 I/O 상태의 원인이 아님을 의미합니다. 이 조건을 “중단된 I/O”라고 합니다. 대부분의 디스크 요청은 일반적인 디스크 속도 내에서 발생합니다. 이 일반적인 디스크 속도를 흔히 "디스크 검색 시간"이라고 합니다. 대부분의 표준 디스크에서 디스크 검색 시간은 10밀리초 이내입니다. 따라서 시스템 I/O 경로가 SQL Server로 반환될 때까지 15초는 매우 긴 시간입니다. 
  
## <a name="user-action"></a>사용자 동작  
하드웨어 관련 오류 메시지에 대한 시스템 이벤트 로그를 검사하여 이 오류의 문제를 해결합니다. 또한 사용 가능한 경우 하드웨어 관련 로그를 검사합니다. 필요한 방법과 기술을 사용하여 운영 체제, 드라이버 또는 I/O 하드웨어에서 지연의 원인을 확인해야 합니다. 이 문제를 해결하려면 모든 디바이스 드라이버 및 펌웨어를 업데이트하거나 디스크 시스템과 관련된 다른 진단을 수행해야 합니다. 
  
성능 모니터를 사용하여 다음 카운터를 검사합니다.  
  
-   **Average Disk Sec/Transfer**  
  
-   **Average Disk Queue Length**  
  
-   **Current Disk Queue Length**  
  
예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 실행하는 컴퓨터의 **Average Disk Sec/Transfer** 시간은 일반적으로 15밀리초 미만입니다. **Average Disk Sec/Transfer** 값이 증가하는 경우 이는 I/O 하위 시스템이 I/O 요구를 최적으로 따라가고 있지 못함을 나타냅니다.

[Storport ETW 로깅](/archive/blogs/ntdebugging/storport-etw-logging-to-measure-requests-made-to-a-disk-unit) 같은 기능을 사용하여 디스크 유닛에 대한 요청 대기 시간을 측정할 수도 있습니다. 다른 유사한 디스크 I/O 문제 해결 키트로 [Windows 성능 레코더](/windows-hardware/test/wpt/introduction-to-wpr)의 기본 제공 프로필을 사용할 수 있습니다.
  
> [!NOTE]  
> 바이러스 백신 프로그램으로 인해 디스크 액세스가 느려질 수 있습니다. 액세스 속도를 높이려면 활성 바이러스 검사의 오류 메시지에서 지정한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 파일을 제외하십시오. [fltmc.exe 명령줄 유틸리티](/windows-hardware/drivers/ifs/development-and-testing-tools#fltmcexe-control-program)를 사용하여 시스템에 설치된 모든 필터 드라이버를 쿼리하고 데이터베이스 파일의 스토리지 경로에서 수행하는 기능을 이해할 수 있습니다. 
  
I/O 오류에 대한 자세한 내용은 [Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))(Microsoft SQL Server I/O 기본 사항, 2장) 및 [https://support.microsoft.com/kb/897284/en-us](https://support.microsoft.com/kb/897284/en-us)의 기술 자료 아티클을 참조하세요.  
