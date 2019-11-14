---
title: SQL Server 업그레이드에 대 한 추적 재생
description: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미를 사용 하 여 추적 재생
ms.custom: seo-lt-2019
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
ms.openlocfilehash: b1607aefdc8495f374b2586b0b896f20e87f62d1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056704"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 추적 재생

데이터베이스 실험 도우미 (DEA)에서는 업그레이드 된 테스트 환경에 대해 캡처된 추적 파일을 재생할 수 있습니다. 예를 들어 SQL Server 2008 r 2에서 실행 되는 프로덕션 워크 로드를 살펴보겠습니다. 워크 로드에 대 한 추적 파일은 프로덕션 환경에서 실행 되는 동일한 버전의 SQL Server 환경에서 한 번, 업그레이드 대상 SQL Server 버전 (예: 2016 SQL Server)이 있는 환경에서 한 번 재생 되어야 합니다.

> [!NOTE]
> 이 작업을 실행 하려면 Distributed Replay 추적을 실행 하도록 가상 컴퓨터 또는 물리적 컴퓨터를 수동으로 설정 해야 합니다. 자세한 내용은 [Distributed Replay 컨트롤러 및 클라이언트 설정](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)을 참조 하세요.
>
>

## <a name="create-a-trace-replay"></a>추적 재생 만들기

DEA에서 메뉴 아이콘을 선택 합니다. 확장 된 메뉴에서 재생 아이콘 옆에 있는 **추적 재생** 을 선택 합니다.

![메뉴에서 재생 추적을 선택 합니다.](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Distributed Replay 컨트롤러 컴퓨터를 사용 하려면 원격으로 사용 하는 사용자 계정에 대 한 권한이 있어야 합니다.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Distributed Replay 컨트롤러에 대 한 액세스 권한 부여

1. 명령 프롬프트에서 **dcomcnfg** 를 입력 하 여 **구성 요소 서비스** 인터페이스를 엽니다.
1. **구성 요소 서비스** > **컴퓨터** > **내 컴퓨터** > **DCOM 구성** > **DReplayController**를 확장 합니다.
1. **DReplayController**를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.
1. **보안** 탭에서 **편집** 을 선택 하 여 사용자 계정을 추가 합니다.
1. **확인**을 선택합니다.

### <a name="verify-setup"></a>설치 확인

1.  **SQL Server 설치 경로**: SQL Server 설치 된 경로를 입력 합니다. 예를 들어 C:\\Program Files (x86)\\Microsoft SQL Server\\120입니다.
1.  **컨트롤러 컴퓨터 이름**: 컨트롤러로 설정 된 컴퓨터의 이름을 입력 합니다. 이 컴퓨터는 SQL Server Distributed Replay controller 라는 Windows 서비스를 실행 하 고 있습니다. Distributed Replay 컨트롤러는 Distributed Replay 클라이언트의 작업을 오케스트레이션 합니다. 각 Distributed Replay 환경에는 컨트롤러 인스턴스가 하나만 있을 수 있습니다.
1.  **클라이언트 컴퓨터 이름**: 각 클라이언트 컴퓨터의 이름을 쉼표로 구분 하 여 입력 합니다. 예: client1, client2. 최대 5 개의 클라이언트 컨트롤러를 사용할 수 있습니다. 클라이언트는 SQL Server Distributed Replay client 라는 Windows 서비스를 실행 하는 하나 이상의 컴퓨터 (실제 또는 가상)입니다. 여러 Distributed Replay Client가 함께 작동하여 SQL Server 인스턴스에 대해 작업을 시뮬레이션합니다. 각 Distributed Replay 환경에 하나 이상의 클라이언트가 있을 수 있습니다.
1.  **다음**을 선택합니다.

### <a name="select-a-trace"></a>추적 선택

1.  **추적 파일 경로**: 입력 추적 (.trc) 파일의 경로를 입력 합니다.
1.  **재생 전처리 출력 저장소 경로**:  
    \- IRF 파일이 아직 없는 경우 IRF 파일 및 기타 전처리 출력을 저장할 위치의 경로를 입력 합니다.  
    \- IRF 파일이 이미 있는 경우 IRF 파일의 경로를 입력 합니다.
1. **다음**을 선택합니다.

### <a name="replay-a-trace"></a>추적 재생

1.  **추적 파일 이름**: 추적 파일 이름을 입력 합니다.
1.  **최대 파일 크기 (MB)** : 추적 파일 롤오버 크기 값을 입력 합니다. 기본값은 200입니다. 사용자 지정 값을 입력할 수 있습니다.
1.  **저장소 재생 추적 출력 경로**: 출력 .trc 파일의 경로를 입력 합니다.
1.  **SQL Server 인스턴스 이름**: 추적을 재생할 SQL Server 인스턴스의 이름을 입력 합니다.
1.  **시작**을 선택합니다.

입력 한 정보가 유효 하면 Distributed Replay 프로세스가 시작 됩니다. 그렇지 않으면 잘못 된 정보가 있는 텍스트 boses가 빨간색으로 강조 표시 됩니다. 입력 한 값이 올바른지 확인 한 다음 **시작**을 선택 합니다.

지정 된 위치를 확인 하기 위해 재생이 실행이 완료 될 때까지 기다립니다. 왼쪽 메뉴의 아래쪽에 있는 종 모양 아이콘을 선택 하 여 재생 진행률을 모니터링 합니다.

![재생 추적 진행률](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>추적 재생에 대 한 질문과 대답

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>대상 서버에서 재생 캡처를 시작 하려면 어떤 보안 권한이 필요 한가요?

- DEA 응용 프로그램에서 추적 작업을 실행 하는 Windows 사용자에 게 SQL Server를 실행 하는 대상 컴퓨터에 대 한 sysadmin 권한이 있어야 합니다. 이러한 사용자 권한은 추적을 시작 하는 데 필요 합니다.
- SQL Server를 실행 하는 대상 컴퓨터가 실행 되는 서비스 계정에는 지정 된 추적 파일 경로에 대 한 쓰기 권한이 있어야 합니다.
- Distributed Replay 클라이언트 서비스를 실행 하는 서비스 계정에는 SQL Server를 실행 하는 대상 컴퓨터에 연결 하 고 쿼리를 실행할 수 있는 사용자 권한이 있어야 합니다.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>동일한 세션에서 둘 이상의 재생을 시작할 수 있나요?

예, 여러 재생을 시작 하 고 동일한 세션에서 완료 될 때까지 추적할 수 있습니다.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>동시에 둘 이상의 재생을 시작할 수 있나요?

예. 단, **컨트롤러와 클라이언트**에서 선택한 것과 동일한 컴퓨터 집합이 아닙니다. 컨트롤러와 클라이언트는 사용 중입니다. **컨트롤러 Plus 클라이언트** 에서 별도의 컴퓨터 집합을 설정 하 여 병렬 재생을 시작 합니다.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>재생은 일반적으로 완료 하는 데 소요 되는 시간

재생은 일반적으로 소스 추적과 원본 추적을 전처리 하는 데 걸리는 시간을 더한 시간을 사용 합니다. 그러나 컨트롤러에 등록 된 클라이언트 컴퓨터에서 재생에서 생성 된 부하를 관리 하기에 충분 하지 않은 경우 재생을 완료 하는 데 시간이 더 오래 걸릴 수 있습니다. 컨트롤러를 사용 하 여 최대 16 개의 클라이언트 컴퓨터를 등록할 수 있습니다.

### <a name="how-large-do-target-trace-files-get"></a>대상 추적 파일의 크기는 얼마나 되나요?

대상 추적 파일은 원본 추적 크기의 5 ~ 15 배가 될 수 있습니다. 파일 크기는 실행 되는 쿼리 수에 따라 달라 집니다. 예를 들어 쿼리 계획 blob는 클 수 있습니다. 이러한 쿼리에 대 한 통계가 자주 변경 되 면 더 많은 이벤트가 캡처됩니다.

### <a name="why-do-i-need-to-restore-databases"></a>데이터베이스를 복원 해야 하는 이유는 무엇 인가요?

SQL Server은 상태 저장 관계형 데이터베이스 관리 시스템입니다. A/B 테스트를 제대로 실행 하려면 항상 데이터베이스 상태를 유지 해야 합니다. 그렇지 않으면 재생 중에 프로덕션에 표시 되지 않는 오류가 표시 될 수 있습니다. 이러한 오류를 방지 하려면 원본 캡처 바로 전에 백업을 수행 하는 것이 좋습니다. 마찬가지로, 재생 하는 동안 오류를 방지 하려면 SQL Server를 실행 하는 대상 컴퓨터에서 백업을 복원 해야 합니다.

### <a name="what-does-pass--on-the-replay-page-mean"></a>재생 페이지의 "통과%"는 무엇을 의미 하나요?

**통과%** 는 쿼리 비율만 전달 됨을 의미 합니다. 오류 수가 예상 되는지 여부를 진단할 수 있습니다. 오류가 발생 하거나 데이터베이스의 무결성이 손실 되어 오류가 발생할 수 있습니다. **Pass%** 에 대 한 값이 잘못 된 경우 추적을 중지 하 고 SQL Profiler에서 추적 파일을 확인 하 여 실패 한 쿼리가 있는지 확인할 수 있습니다.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>재생 하는 동안 수집 된 추적 이벤트를 어떻게 확인할 수 있나요?

대상 추적 파일을 열고 SQL Profiler에서 봅니다. 또는 재생 캡처를 수정 하려는 경우 모든 SQL Server 스크립트를 C:\\Program Files (x86)\\Microsoft Corporation\\데이터베이스 실험 도우미\\스크립트\\StartReplayCapture. SQL에서 사용할 수 있습니다.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>재생 하는 동안 DEA에서 수집 하는 추적 이벤트는 무엇입니까?

DEA는 성능 관련 정보를 포함 하는 추적 이벤트를 캡처합니다. 캡처 구성은 StartReplayCaptureTrace 스크립트에 있습니다. 이러한 이벤트는 [sp_trace_setevent (transact-sql) 참조 설명서](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)에 나열 된 추적 이벤트 SQL Server 일반적인 이벤트입니다.

## <a name="troubleshoot-trace-replay"></a>추적 재생 문제 해결

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>SQL Server를 실행 하는 컴퓨터에 연결할 수 없습니다.

- SQL Server를 실행 하는 컴퓨터의 이름이 올바른지 확인 합니다. 확인 하려면 SSMS (SQL Server Management Studio)를 사용 하 여 서버에 연결을 시도 합니다.
- 방화벽 구성이 SQL Server를 실행 하는 컴퓨터에 대 한 연결을 차단 하지 않는지 확인 합니다.
- 사용자에 게 필요한 사용자 권한이 있는지 확인 합니다.
- Distributed Replay 클라이언트의 서비스 계정에 SQL Server를 실행 하는 컴퓨터에 대 한 액세스 권한이 있는지 확인 합니다.

% Temp%\\DEA의 로그에서 자세한 내용을 볼 수 있습니다. 문제가 지속 되 면 제품 팀에 문의 하십시오.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>Distributed Replay 컨트롤러에 연결할 수 없습니다.

- 컨트롤러 컴퓨터에서 Distributed Replay controller 서비스가 실행 중인지 확인 합니다. 확인 하려면 Distributed Replay 관리 도구 (명령 `dreplay.exe status -f 1`실행)를 사용 합니다.
- 재생이 원격으로 시작 되는 경우:
  - DEA를 실행 하는 컴퓨터에서 컨트롤러를 성공적으로 ping 할 수 있는지 확인 합니다. **재생 환경 구성** 페이지의 지침에 따라 방화벽 설정에서 연결을 허용 하는지 확인 합니다. 자세한 내용은 [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)문서를 참조 하세요.
  - Distributed Replay 컨트롤러의 사용자에 대해 DCOM 원격 시작 및 원격 활성화가 허용 되는지 확인 합니다.
  - Distributed Replay controller 사용자에 대 한 DCOM 원격 액세스 사용자 권한이 허용 되는지 확인 합니다.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>추적 파일 경로가 내 컴퓨터에 있습니다. 컨트롤러를 찾을 Distributed Replay 없는 이유는 무엇입니까?

Distributed Replay 로컬 디스크 리소스에만 액세스할 수 있습니다. 재생을 시작 하기 전에 원본 추적 파일을 Distributed Replay 컨트롤러 컴퓨터에 복사 해야 합니다. 또한 DEA **새 재생** 페이지에서 경로를 제공 해야 합니다. 

UNC 경로는 Distributed Replay와 호환 되지 않습니다. Distributed Replay 경로는 확장을 포함 하 여 첫 번째 소스 추적 파일의 절대 로컬 경로 여야 합니다.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>새 재생 페이지에서 파일을 찾을 수 없는 이유는 무엇입니까?

원격 컴퓨터의 폴더를 검색할 수 없으므로 파일 검색은 유용 하지 않습니다. 절대 경로를 복사 하 여 붙여 넣는 것이 더 효율적입니다.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>추적을 사용 하 여 재생을 시작 했지만 이벤트를 재생 하지 Distributed Replay

이 문제는 추적 파일에 재생 가능한 이벤트가 없거나 이벤트를 재생 하는 방법에 대 한 정보가 없는 경우에 발생할 수 있습니다. 제공 된 추적 파일 경로가 원본 추적 파일 인지 여부를 확인 합니다. 원본 추적 파일은 StartCaptureTrace 스크립트에서 제공 하는 구성을 사용 하 여 만들어집니다.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>"예기치 않은 오류가 발생 했습니다."가 표시 됩니다. SQL Server 2017 Distributed Replay 컨트롤러를 사용 하 여 추적 파일을 전처리 하려고 하면

이 문제는 SQL Server 2017의 RTM 버전에서 알려져 있습니다. 자세한 내용은 [2017 SQL Server에서 캡처 기능을 사용 하 여 캡처된 추적을 재생 하는 경우 예기치 않은 오류](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)를 참조 하세요.  
  
SQL Server 2017에 대 한 최신 누적 업데이트 1에서이 문제가 해결 되었습니다. [SQL Server 2017에 대 한 최신 버전의 누적 업데이트 1](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)을 다운로드 합니다.

## <a name="next-steps"></a>다음 단계

- 제안 된 변경 내용에 대 한 정보를 얻는 데 도움이 되는 분석 보고서를 만들려면 [보고서 만들기](database-experimentation-assistant-create-report.md)를 참조 하세요.

- DEA 및 데모에 대 한 19 분의 소개는 다음 비디오를 시청 하세요.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
