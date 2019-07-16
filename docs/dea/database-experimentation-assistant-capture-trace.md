---
title: 데이터베이스 실험 도우미에서 SQL Server 업그레이드에 대 한 추적 캡처
description: 데이터베이스 실험 도우미에서 추적 캡처
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: ab361c4e83ae5e2b2bb6614bdc4a513e0bdd77ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059001"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 추적 캡처

캡처된 서버 이벤트 로그에 있는 추적 파일을 만들려면 추적 캡처를 데이터베이스 실험 도우미 (비활성화)에서 사용할 수 있습니다. 캡처된 서버 이벤트는 특정 기간 동안 특정 서버에서 발생 하는 이벤트입니다. 추적 캡처 서버당 한 번 실행 되어야 합니다.

추적 캡처를 시작 하기 전에 모든 대상 데이터베이스를 백업 해야 합니다.

SQL Server에 캐시 된 쿼리 평가 결과 영향을 줄 수 있습니다. 권장 SQL Server 서비스 (MSSQLSERVER)를 다시 시작 하는 평가 결과의 일관성을 개선 하기 위해 서비스 응용 프로그램에서입니다.

## <a name="create-a-trace-capture"></a>추적 캡처

1. 비활성화를에서 왼쪽된 메뉴에서 메뉴 아이콘을 선택 합니다. 확장 된 메뉴에서 선택 **추적 캡처** 카메라 아이콘 옆에 있습니다.

    ![메뉴에서 추적 캡처를 선택 합니다.](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. 아래 **새 캡처**, 입력 또는 다음 정보를 선택 합니다.

    - **SQL Server 인스턴스 이름을**: 서버 추적을 캡처할 하려는 SQL Server를 실행 하는 컴퓨터의 이름을 입력 합니다.
    - **데이터베이스 이름**: 데이터베이스 추적을 시작 하는 데이터베이스의 이름을 입력 합니다. 데이터베이스를 지정 하지 않으면 추적은 서버의 모든 데이터베이스에서 캡처됩니다.
    - **추적 파일 이름이**: 캡처에 대 한 추적 파일의 이름을 입력 합니다.
    - **최대 파일 크기 (MB)** : 롤오버 파일의 크기를 선택 합니다. 새 파일을 선택 하는 파일 크기에서 필요에 따라 생성 됩니다. 권장 되는 롤오버 크기는 200mb입니다.
    - **기간 (분)** : 기간 (분)에 실행 추적 캡처를 선택 합니다.
    - **추적 출력 파일을 저장할 경로를**: 추적 파일에 대 한 대상 경로 선택 합니다. 

    > [!NOTE]
    > SQL Server를 실행 하는 컴퓨터의 추적 파일에 파일 경로 여야 합니다. SQL Server 서비스는 특정 계정에 대 한을 설정 하지 않으면 서비스 쓸 수 있습니다 필요 권한을 쓸 추적 파일 폴더를 지정된 합니다.
    >
    >

    ![새 캡처 페이지](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>추적 캡처를 시작 합니다.

를 입력 하거나 필요한 정보를 선택한 후 선택할 **시작** 추적 캡처를 시작 합니다. 입력 정보가 올바르면 추적 캡처 프로세스가 시작 됩니다. 그렇지 않으면 잘못 된 항목이 있는 입력란 빨간색 강조 표시 됩니다. 

선택 하거나 입력 한 값 잘못 되어 선택한 했는지 **시작**합니다.

추적 캡처 완료 되 면 새 추적 파일에 지정 된 파일 위치에서 찾을 실행 **추적 출력 파일을 저장할 경로를**입니다. 캡처의 진행률을 모니터링 하려면 왼쪽된 메뉴의 맨 아래에 있는 종 모양 아이콘을 선택 합니다.

![진행률 추적 캡처](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>추적 파일

추적 캡처는 지정된 된 위치에.trc 파일에 씁니다. 추적 파일을 SQL Server 데이터베이스의 활동 추적 결과 포함합니다. TRC 파일 오류를 검색 하 여 SQL Server에서 보고에 대 한 자세한 정보를 제공 하도록 설계 되었습니다.

## <a name="frequently-asked-questions-about-trace-capture"></a>추적 캡처에 대 한 질문과 대답

다음은 몇 가지 질문과 대답에서 비활성화 추적 캡처에 대 한 합니다.

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>프로덕션 데이터베이스에서 추적 캡처를 실행 하면 캡처할 이벤트를?

다음 표에서 이벤트 및 해당 열 데이터 추적의 수집에 목록을 제공 합니다.
  
|이벤트 이름|텍스트 데이터 (1)|이진 데이터 (2)|데이터베이스 ID (3)|호스트 이름 (8)|응용 프로그램 이름 (10)|로그인 이름 (11)|SPID (12)|시작 시간 (14)|종료 시간 (15)|데이터베이스 이름 (35)|이벤트 시퀀스 (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: (10)를 완료 합니다.**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: (11)를 시작 합니다.**||*|*|*|*|*|*|*||*|*|*|  
|**RPC Output Parameter (100)**|*||*|*|*|*|*|*||*|*|*|  
|**Sql: batchcompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**Sql: batchstarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**Audit Login (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Audit Logout (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Prepare SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec Prepared SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>내 프로덕션 서버의 성능에 영향 추적 캡처 실행 중일 때 있나요?
    
예, 추적 수집 하는 동안는 최소 성능에 영향 있습니다. 이 테스트에서 3% 메모리 압력에 대 한 발견 했습니다.
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>어떤 종류의 사용 권한이 프로덕션 워크 로드에 대 한 추적을 캡처하도록 필요 한가요?
    
- 비활성화 응용 프로그램에서 추적 작업을 실행 하는 Windows 사용자는 SQL Server를 실행 하는 컴퓨터에서 sysadmin 권한이 있어야 합니다.
- 지정 된 추적 파일 경로에 SQL Server를 실행 하는 컴퓨터에서 사용 되는 서비스 계정에 쓰기 권한이 있어야 합니다.

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>전체 서버 또는 단일 데이터베이스에 대해서만 추적을 캡처할 수 있나요?
    
단일 데이터베이스 또는 서버의 모든 데이터베이스에 대 한 추적 캡처를 비활성화를 사용할 수 있습니다.
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>연결된 된 서버 내 프로덕션 환경에서 구성 했습니다. 이러한 쿼리 표시지 않습니다 추적에?
    
전체 서버에 대 한 추적 캡처를 실행 하는 경우 추적 된 연결된 서버 쿼리를 포함 하 여 모든 쿼리를 캡처합니다. 전체 서버에 대 한 추적 캡처를 실행 하려면 유지 합니다 **데이터베이스 이름** 상자에 **새 캡처** 빈 합니다.
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>프로덕션 워크 로드 추적에 대 한 권장 되는 최소 시간 이란?
    
워크 로드 전체를 가장 잘 나타내는 시간을 선택 하는 것이 좋습니다. 이런 방식으로 분석 워크 로드의 모든 쿼리에 대해 실행 됩니다.
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>추적 캡처를 시작 하기 전에 데이터베이스 백업을 오른쪽 수행 하려면이 얼마나 중요 한지?
    
추적 캡처를 시작 하기 전에 모든 대상 데이터베이스를 백업 해야 합니다. 대상 1-2 대상에서 캡처한 추적 재생 됩니다. 데이터베이스 상태를 동일한 없으면 실험의 결과 일치 하지 않습니다.

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>추적 하는 대신 XEvents를 수집할 수 있으며 Xevent 재생할 수 있습니까?
    
예 비활성화는 XEvents를 지원합니다. 비활성화의 최신 버전을 다운로드 하 고 사용해 보세요.

## <a name="troubleshoot-trace-captures"></a>추적 캡처를 문제 해결

추적 캡처를 실행 하는 경우 오류를 표시 하는 경우 다음 필수 구성 요소를 검토 합니다.

- SQL Server를 실행 하는 컴퓨터의 이름이 올바른지 확인 합니다. 를 확인 하려면 SQL Server Management Studio (SSMS)를 사용 하 여 SQL Server를 실행 하는 컴퓨터에 연결 하려고 합니다.
- 방화벽 구성에 SQL Server를 실행 하는 컴퓨터에 대 한 연결을 차단 하지 확인 합니다.
- 사용자에 블로그 게시물에 나열 된 권한이 있는지 확인 [재생 FAQ](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)합니다.
- 추적 이름 표준 롤오버 규칙을 따르지는 확인 (캡처\_1). 캡처 같은 추적 이름 대신 시도\_1A 또는 Capture1 합니다.

다음은 몇 가지 가능한 오류 표시 될 수 있습니다 및 해결을 위한 솔루션입니다.

|가능한 오류|해결 방법|  
|---|---|  
|필요한 사용 권한이 있는지 여부 및 SQL Server 계정에 지정 된 추적 파일 경로가 Sql 오류 코드 (53)에 대 한 쓰기 시작할 수 없습니다 대상 SQL Server에서 추적 확인|SQL Server를 실행 하는 컴퓨터에 대 한 액세스를 비활성화 도구를 실행 하는 사용자 있어야 합니다. 사용자는 sysadmin 역할이 할당 되어야 합니다.|  
|필요한 사용 권한이 있는지 여부 및 SQL Server 계정에 지정 된 추적 파일 경로가 Sql 오류 코드 (19062)에 대 한 쓰기 시작할 수 없습니다 대상 SQL Server에서 추적 확인|지정 된 추적 경로 수 없거나 폴더에는 SQL server 서비스가 실행 되 고 (예: 네트워크 서비스) 계정에 대 한 쓰기 권한이 없습니다. 경로 있어야 하 고 시작 하려면 추적에 대 한 권한이 있어야 합니다.|  
|현재 비활성화 추적 대상 서버에서 실행 됩니다.|대상 서버에서 활성화 된 추적 실행 중입니다. 서버 차원의 추적이 이미 실행 하는 경우에 새 추적을 시작할 수 없습니다.|  
|추적 캡처를 위해 요청 된 데이터베이스를 열 수 없습니다. 이 오류는 잘못 된 데이터베이스 이름으로 발생할 수 있습니다.|지정한 데이터베이스가 없거나 현재 사용자에 게 액세스할 수 없는 합니다. 올바른 데이터베이스 이름을 사용 합니다.|  

레이블이 지정 된 다른 오류가 표시 되 면 *Sql 오류 코드*를 참조 하십시오 [시스템 오류 메시지](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/cc645603(v=sql.105)) 자세한 설명 및 해결 방법에 대 한 합니다.
    
## <a name="next-steps"></a>다음 단계

- 캡처된 추적을 재생 하기 전에 SQL server에서 Distributed Replay 도구를 구성 하는 방법에 알아보려면 참조 [재생 구성](database-experimentation-assistant-configure-replay.md)합니다.

- 비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
