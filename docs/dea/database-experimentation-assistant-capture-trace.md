---
title: SQL Server 업그레이드에 대 한 추적 캡처
description: 캡처 서버 이벤트 로그를 사용 하 여 추적 파일을 만들려면 데이터베이스 실험 도우미 (DEA)를 사용 합니다.
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.openlocfilehash: e335170c97f18039767fab8bf0b8400ce9f9b45d
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97643763"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 추적 캡처

데이터베이스 실험 도우미 (DEA)를 사용 하 여 캡처된 서버 이벤트의 로그를 사용 하 여 추적 파일을 만들 수 있습니다. 캡처한 서버 이벤트는 특정 기간 동안 특정 서버에서 발생 하는 이벤트입니다. 추적 캡처는 서버당 한 번만 실행 해야 합니다.

추적 캡처를 시작 하기 전에 모든 대상 데이터베이스를 백업 해야 합니다.

SQL Server의 쿼리 캐싱은 평가 결과에 영향을 줄 수 있습니다. 평가 결과의 일관성을 향상 시키려면 서비스 응용 프로그램에서 SQL Server 서비스 (MSSQLSERVER)를 다시 시작 하는 것이 좋습니다.

## <a name="configure-a-trace-capture"></a>추적 캡처 구성

1. DEA의 왼쪽 탐색 모음에서 카메라 아이콘을 선택 하 고 **모든 캡처** 페이지에서 **새 캡처** 를 선택 합니다.

    ![DEA에서 캡처 만들기](./media/database-experimentation-assistant-capture-trace/dea-initiate-capture.png)

2. **새 캡처** 페이지의 **세부 정보 캡처** 에서 다음 정보를 입력 하거나 선택 합니다.

    - **캡처 이름**: 캡처에 대 한 추적 파일의 이름을 입력 합니다.
    - **형식**: 캡처에 대 한 형식 (Trace 또는 xevent)을 지정 합니다.
    - **기간**: 추적 캡처를 실행할 시간 (분)을 선택 합니다.
    - **캡처 위치**: 추적 파일의 대상 경로를 선택 합니다.

        > [!NOTE]
        > 추적 파일의 파일 경로는 SQL Server를 실행 하는 컴퓨터에 있어야 합니다. SQL Server 서비스가 특정 계정에 대해 설정 되지 않은 경우 서비스는 기록할 추적 파일에 대해 지정 된 폴더에 대 한 쓰기 권한이 필요할 수 있습니다.

3. **예, 수동으로 백업을 수행 했습니다** ...를 선택 하 여 백업을 수행 했는지 확인 합니다. 선택합니다.

4. **세부 정보 캡처** 에서 다음 정보를 입력 하거나 선택 합니다.

    - **서버 유형**: SQL Server의 유형 (**SqlServer**, **AzureSqlDb**, **AzureSqlManagedInstance**)을 지정 합니다.
    - **서버 이름**: SQL Server의 서버 이름 또는 IP 주소를 지정 합니다.
    - **인증 유형**: 인증 유형으로 **Windows** 를 선택 합니다.
    - **데이터베이스 이름**: 데이터베이스 추적을 시작할 데이터베이스의 이름을 입력 합니다. 데이터베이스를 지정 하지 않으면 서버에 있는 모든 데이터베이스에서 추적이 캡처됩니다.

5. 시나리오에 적절 한 **연결 암호화** 및 **서버 인증서 신뢰** 확인란을 선택 하거나 선택 취소 합니다.

    ![새 캡처 페이지](./media/database-experimentation-assistant-capture-trace/dea-new-capture.png)

## <a name="start-the-trace-capture"></a>추적 캡처 시작

1. 필요한 정보를 입력 하거나 선택한 후 **시작** 을 선택 하 여 추적 캡처를 시작 합니다.

    입력 한 정보가 올바르면 추적 캡처 프로세스가 시작 됩니다. 그렇지 않으면 잘못 된 항목을 포함 하는 입력란이 빨간색으로 강조 표시 됩니다. 오류가 발생 하면 필요한 항목을 수정한 후 다시 **시작** 을 선택 합니다.

    추적 캡처가 실행 되는 동안 **세부 정보 캡처** 에서 추적 캡처 프로세스의 상태와 진행률이 표시 됩니다.

    ![캡처 진행률 모니터링](./media/database-experimentation-assistant-capture-trace/dea-capture-running.png)

2. 추적 캡처의 실행이 완료 되 면 새 추적 파일 (.trc)이 초기 구성 중에 특정 한 **캡처 위치** 에 저장 됩니다.

    ![완료 된 추적 캡처](./media/database-experimentation-assistant-capture-trace/dea-capture-complete.png)

    추적 파일에는 SQL Server 데이터베이스 작업의 추적 결과가 포함 됩니다. .trc 파일은 SQL Server에서 검색 및 보고 하는 오류에 대 한 자세한 정보를 제공 하도록 설계 되었습니다.

## <a name="frequently-asked-questions-about-trace-capture"></a>추적 캡처에 대 한 질문과 대답

다음은 DEA의 추적 캡처에 대 한 몇 가지 질문과 대답입니다.

**Q: 프로덕션 데이터베이스에서 추적 캡처를 실행할 때 캡처되는 이벤트는 무엇입니까?**

다음 표에서는 DEA에서 추적에 대해 수집 하는 이벤트 및 해당 열 데이터를 나열 합니다.
  
|이벤트 이름|텍스트 데이터 (1)|이진 데이터 (2)|데이터베이스 ID (3)|호스트 이름 (8)|응용 프로그램 이름 (10)|로그인 이름 (11)|SPID (12)|시작 시간 (14)|종료 시간 (15)|데이터베이스 이름 (35)|이벤트 시퀀스 (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC: 완료 됨 (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC: 시작 (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC 출력 매개 변수 (100)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL: BatchCompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL: BatchStarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**감사 로그인 (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**로그 아웃 감사 (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**SQL 준비 (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec 준비 SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

**Q: 추적 캡처가 실행 중일 때 프로덕션 서버에 성능 영향이 있나요?**

예, 추적 수집 중에는 최소한의 성능 효과가 있습니다. 테스트에서 3% 메모리가 중을 발견 했습니다.

**Q: 프로덕션 워크 로드에서 추적을 캡처하는 데 필요한 권한 종류는 무엇 인가요?**

- DEA 응용 프로그램에서 추적 작업을 실행 하는 Windows 사용자에 게 SQL Server를 실행 하는 컴퓨터에 대 한 sysadmin 권한이 있어야 합니다.
- SQL Server를 실행 하는 컴퓨터에서 사용 되는 서비스 계정에는 지정 된 추적 파일 경로에 대 한 쓰기 권한이 있어야 합니다.

**Q: 전체 서버 또는 단일 데이터베이스에 대 한 추적을 캡처할 수 있나요?**

DEA를 사용 하 여 서버 또는 단일 데이터베이스의 모든 데이터베이스에 대 한 추적을 캡처할 수 있습니다.

**Q: 내 프로덕션 환경에 연결 된 서버를 구성 했습니다. 이러한 쿼리가 추적에 표시 되나요?**

전체 서버에 대해 추적 캡처를 실행 하는 경우 추적은 연결 된 서버 쿼리를 포함 하 여 모든 쿼리를 캡처합니다. 전체 서버에 대해 추적 캡처를 실행 하려면 **데이터베이스 이름** 상자를 **새 캡처** 빈 상태로 둡니다.

**Q: 프로덕션 작업 추적에 대해 권장 되는 최소 시간은 무엇 인가요?**

전체 워크 로드를 가장 잘 나타내는 시간을 선택 하는 것이 좋습니다. 이렇게 하면 작업의 모든 쿼리에서 분석이 실행 됩니다.

**Q: 추적 캡처를 시작 하기 전에 데이터베이스 백업을 즉시 수행 하는 것이 얼마나 중요 합니까?**

추적 캡처를 시작 하기 전에 모든 대상 데이터베이스를 백업 해야 합니다. 대상 1과 대상 2에서 캡처된 추적이 재생 됩니다. 데이터베이스 상태가 동일 하지 않으면 실험 결과가 왜곡 됩니다.

**Q: 추적 대신 Xevent를 수집할 수 있으며 Xevent를 재생할 수 있나요?**

예. DEA는 Xevent을 지원 합니다. 최신 버전의 DEA를 다운로드 하 여 사용해 보세요.

## <a name="troubleshoot-trace-captures"></a>추적 캡처 문제 해결

추적 캡처를 실행할 때 오류가 표시 되는 경우 다음을 확인 합니다.

- SQL Server를 실행 하는 컴퓨터의 이름이 유효 합니다. 확인 하려면 SSMS (SQL Server Management Studio)를 사용 하 여 SQL Server를 실행 하는 컴퓨터에 연결을 시도 합니다.
- 방화벽 구성은 SQL Server를 실행 하는 컴퓨터에 대 한 연결을 차단 하지 않습니다.
- 사용자에 게 [재생 FAQ](./database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)에 나열 된 사용 권한이 있습니다.
- 추적 이름은 표준 롤오버 규칙 (캡처 1)을 따르지 않습니다 \_ . 대신 Capture 1a 또는 Capture1와 같은 추적 이름을 사용해 보세요 \_ .

다음은 표시 될 수 있는 몇 가지 오류와 해결 방법입니다.

|가능한 오류|해결 방법|  
|---|---|  
|대상 SQL Server에서 추적을 시작할 수 없습니다. 필요한 권한이 있는지 확인 하 고 SQL Server 계정에 지정 된 추적 파일 경로 Sql 오류 코드 (53)에 대 한 쓰기 권한이 있는지 확인 하십시오.|DEA 도구를 실행 하는 사용자는 SQL Server를 실행 하는 컴퓨터에 액세스할 수 있어야 합니다. 사용자에 게 sysadmin 역할이 할당 되어야 합니다.|  
|대상 SQL Server에서 추적을 시작할 수 없습니다. 필요한 권한이 있는지 확인 하 고 SQL Server 계정에 지정 된 추적 파일 경로 Sql 오류 코드 (19062)에 대 한 쓰기 권한이 있는지 확인 하십시오.|지정 된 추적 경로가 없거나, 해당 폴더에 SQL Server 서비스가 실행 중인 계정에 대 한 쓰기 권한이 없는 경우 (예: 네트워크 서비스) 경로가 있어야 하 고 추적을 시작 하는 데 필요한 권한이 있어야 합니다.|  
|DEA 추적이 현재 대상 서버에서 실행 되 고 있습니다.|활성 추적이 대상 서버에서 이미 실행 중입니다. 서버 차원 추적이 이미 실행 중인 경우에는 새 추적을 시작할 수 없습니다.|  
|추적을 캡처하기 위해 요청 된 데이터베이스를 열 수 없습니다. 이 오류는 잘못 된 데이터베이스 이름으로 인해 발생할 수 있습니다.|지정 된 데이터베이스가 존재 하지 않거나 현재 사용자가 액세스할 수 없습니다. 올바른 데이터베이스 이름을 사용 하십시오.|  

*Sql 오류 코드* 라는 다른 오류가 표시 되는 경우 자세한 설명은 [데이터베이스 엔진 오류](../relational-databases/errors-events/database-engine-events-and-errors.md) 를 참조 하세요.

## <a name="see-also"></a>참고 항목

- 캡처된 추적을 재생 하기 전에 SQL Server에서 Distributed Replay 도구를 구성 하는 방법을 알아보려면 [데이터베이스 실험 도우미에 대 한 Distributed Replay 구성](database-experimentation-assistant-configure-replay.md)을 참조 하세요.