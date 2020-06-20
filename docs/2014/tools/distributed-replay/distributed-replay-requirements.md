---
title: Distributed Replay 요구 사항 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 6fffee7d-891f-4d9d-b2c3-dd19855a1c2c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 860de6d29557b6594c9ec149f09e915b837fa95e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048510"
---
# <a name="distributed-replay-requirements"></a>Distributed Replay Requirements
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay 기능을 사용하기 전에 이 항목에서 설명하는 제품 요구 사항을 검토하세요.  
  
## <a name="input-trace-requirements"></a>입력 추적 요구 사항  
 추적 데이터를 재생하려면 데이터가 버전 및 형식 요구 사항을 충족해야 하고 필요한 이벤트 및 열을 포함해야 합니다.  
  
### <a name="input-trace-versions"></a>입력 추적 버전  
 Distributed Replay는 다음 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 수집된 입력 추적 데이터를 지원합니다.  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
### <a name="input-trace-formats"></a>입력 추적 형식  
 입력 추적 데이터는 다음 형식 중 하나일 수 있습니다.  
  
-   확장명이 `.trc` 인 단일 추적 파일  
  
-   파일 롤오버 명명 규칙을 따르는 일련의 롤오버 추적 파일은 예를 들면 `<TraceFile>.trc`, `<TraceFile>_1.trc`, `<TraceFile>_2.trc`, `<TraceFile>_3.trc`, `<TraceFile>_n.trc`와 같습니다.  
  
### <a name="input-trace-events-and-columns"></a>입력 추적 이벤트 및 열  
 Distributed Replay에서 입력 추적 데이터를 재생하려면 데이터가 특정 이벤트 및 열을 포함해야 합니다. **의** TSQL_Replay [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 템플릿에 필요한 모든 이벤트 및 열과 추가 정보가 포함되어 있습니다. 이 템플릿에 대한 자세한 내용은 [Replay Requirements](../sql-server-profiler/replay-requirements.md)을 참조하십시오.  
  
> [!WARNING]  
>  **TSQL_Replay** 템플릿을 사용하여 입력 추적 데이터를 캡처하지 않거나 입력 추적 요구 사항이 충족되지 않은 경우 예기치 않은 재생 결과가 수신될 수 있습니다.  
  
 사용자 지정 추적 템플릿을 만들고 이를 통해 Distributed Replay를 사용하여 이벤트를 재생할 수도 있습니다. 이 경우 사용자 지정 추적 템플릿에 다음 이벤트가 포함되어 있어야 합니다.  
  
-   로그인 감사  
  
-   로그아웃 감사  
  
-   ExistingConnection  
  
-   RPC Output Parameter  
  
-   RPC:Completed  
  
-   RPC:Starting  
  
-   SQL:BatchCompleted  
  
-   SQL:BatchStarting  
  
 서버 쪽 커서를 재생하는 경우 다음 이벤트도 필요합니다.  
  
-   CursorClose  
  
-   CursorExecute  
  
-   CursorOpen  
  
-   CursorPrepare  
  
-   CursorUnprepare  
  
 서버 쪽 준비된 SQL 문을 재생하는 경우 다음 이벤트도 필요합니다.  
  
-   Exec Prepared SQL  
  
-   Prepare SQL  
  
 모든 입력 추적 데이터는 다음 열을 포함해야 합니다.  
  
-   Event Class  
  
-   EventSequence  
  
-   TextData  
  
-   애플리케이션 이름  
  
-   LoginName  
  
-   DatabaseName  
  
-   데이터베이스 ID  
  
-   HostName  
  
-   이진 데이터  
  
-   SPID  
  
-   시작 시간  
  
-   EndTime  
  
-   IsSystem  
  
## <a name="supported-input-trace-and-target-server-combinations"></a>지원되는 입력 추적 및 대상 서버의 조합  
 다음 표에서는 지원되는 추적 데이터 버전과 버전마다 데이터 재생이 지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 보여 줍니다.  
  
|입력 추적 데이터 버전|대상 서버 인스턴스에 대해 지원되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|  
|---------------------------------|------------------------------------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
  
## <a name="operating-system-requirements"></a>운영 체제 요구 사항  
 관리 도구, 컨트롤러 및 클라이언트 서비스를 실행할 수 있는 운영 체제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스와 동일합니다. 인스턴스에 대해 지원 되는 운영 체제에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [SQL Server 2014를 설치 하기 위한 하드웨어 및 소프트웨어 요구 사항](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)을 참조 하세요.  
  
 Distributed Replay 기능은 x86 기반 및 x64 기반 운영 체제 모두에서 지원됩니다. x64 기반 운영 체제의 경우 WOW(Windows on Windows) 모드만 지원됩니다.  
  
## <a name="installation-limitations"></a>설치 제한 사항  
 컴퓨터당 각 Distributed Replay 기능의 단일 인스턴스를 한 번만 설치할 수 있습니다. 다음 표에서는 단일 환경에서 허용되는 각 Distributed Replay 기능의 설치 횟수를 보여 줍니다.  
  
|Distributed Replay 기능|재생 환경당 최대 설치 횟수|  
|--------------------------------|--------------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller 서비스|1|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Client 서비스|16(실제 또는 가상 컴퓨터)|  
|Administration Tool|제한 없음|  
  
> [!NOTE]  
>  관리 도구는 단일 컴퓨터에 한 번만 설치할 수 있지만 관리 도구의 여러 인스턴스를 시작할 수 있습니다. 여러 관리 도구에서 실행한 명령은 명령을 받은 순서대로 확인됩니다.  
  
## <a name="data-access-provider"></a>데이터 액세스 공급자  
 Distributed Replay는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 데이터 액세스 공급자만 지원합니다.  
  
## <a name="target-server-preparation-requirements"></a>대상 서버 준비 요구 사항  
 테스트 환경에 대상 서버를 배치하는 것이 좋습니다. 데이터가 원래 기록되었던 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 아닌 다른 인스턴스에서 추적 데이터를 재생하려면 대상 서버에서 다음 요구 사항을 충족해야 합니다.  
  
-   추적 데이터에 포함된 모든 로그인 및 사용자가 대상 서버에서 동일한 데이터베이스에 있어야 합니다.  
  
-   대상 서버에 있는 모든 로그인 및 사용자가 원래 서버에서 가진 권한과 같은 권한을 가져야 합니다.  
  
-   대상에 있는 데이터베이스 ID가 원본에 있는 데이터베이스 ID와 같아야 합니다. 그러나 두 ID가 서로 다르다면 **DatabaseName** 이 추적에 있을 경우 이를 기준으로 일치시킬 수 있습니다.  
  
-   추적 데이터에 포함된 각 로그인의 기본 데이터베이스가 대상 서버에서 로그인의 각 대상 데이터베이스로 설정되어야 합니다. 예를 들어 재생할 추적 데이터가 원래 **인스턴스의**Fred_Db **데이터베이스에 있는** Fred [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]라는 로그인에 대한 작업을 포함해야 합니다. 따라서 대상 서버에서 **Fred**로그인에 대한 기본 데이터베이스는 **Fred_Db** 와 일치하는 데이터베이스로 설정되어야 합니다. 데이터베이스 이름이 다르더라도 마찬가지입니다. 로그인의 기본 데이터베이스를 설정하려면 `sp_defaultdb` 시스템 저장 프로시저를 사용합니다.  
  
 누락되거나 잘못된 로그인과 연관된 이벤트를 재생하면 재생 오류가 발생하지만 재생 작업은 계속됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Distributed Replay 보안](distributed-replay-security.md)   
 [Distributed Replay 설치](install-distributed-replay-overview.md)  
  
  
