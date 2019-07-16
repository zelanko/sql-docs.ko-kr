---
title: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미를 사용 하 여 추적 재생
description: 데이터베이스 실험 도우미를 사용 하 여 추적 재생
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
ms.openlocfilehash: 53534d9d269803a4bce0902c1f22349dfe6c57e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058890"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 추적 재생

데이터베이스 실험 도우미 (비활성화), 캡처된 추적 파일을 업그레이드 된 테스트 환경에 대해 재생할 수 있습니다. 예를 들어, SQL Server 2008 R2에서 실행 되는 프로덕션 워크 로드를 고려 합니다. 워크 로드에 대 한 추적 파일을 두 번 재생 해야 합니다: 프로덕션에 다시 업그레이드 대상 SQL Server 버전 등 SQL Server 2016가 설치 된 환경에서 실행 되는 SQL Server의 동일한 버전을 사용 하 여 환경에서 한 번입니다.

> [!NOTE]
> 이 작업을 실행 하려면 수동으로 설정 해야 가상 컴퓨터 또는 물리적 컴퓨터 Distributed Replay 추적을 실행 합니다. 자세한 내용은 [Distributed Replay 컨트롤러 및 클라이언트 설치](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)합니다.
>
>

## <a name="create-a-trace-replay"></a>추적 재생을 만들려면

비활성화를에서 메뉴 아이콘을 선택 합니다. 확장 된 메뉴에서 선택 **추적 재생** 재생 아이콘 옆에 있는 합니다.

![메뉴에서 추적 재생을 선택 합니다.](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Distributed Replay 컨트롤러 컴퓨터에는 원격을 사용 하는 사용자 계정에 권한이 필요 합니다.
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Distributed Replay 컨트롤러에 액세스 권한 부여

1. 명령 프롬프트에서 입력 **dcomcnfg** 열려는 합니다 **구성 요소 서비스** 인터페이스입니다.
1. 확장 **구성 요소 서비스** > **컴퓨터** > **컴퓨터로** > **DCOM 구성**  >  **DReplayController**합니다.
1. 마우스 오른쪽 단추로 클릭 **DReplayController**를 선택한 후 **속성**합니다.
1. 에 **보안** 탭을 선택 **편집** 사용자 계정을 추가 합니다.
1. **확인**을 선택합니다.

### <a name="verify-setup"></a>설치 확인

1.  **SQL Server 설치 경로**: SQL Server를 설치 하는 위치에 경로 입력 합니다. 예를 들어 c:\\프로그램 파일 (x86)\\Microsoft SQL Server\\120입니다.
1.  **컨트롤러 컴퓨터 이름**: 컨트롤러와 설정 된 컴퓨터의 이름을 입력 합니다. 이 컴퓨터에는 SQL Server Distributed Replay controller 라는 Windows 서비스 실행 중입니다. Distributed Replay controller는 Distributed Replay client의 동작을 오케스트레이션 합니다. 각 Distributed Replay 환경에는 컨트롤러 인스턴스가 하나만 있을 수 있습니다.
1.  **클라이언트 컴퓨터 이름을**: 쉼표로 구분 하 여 각 클라이언트 컴퓨터의 이름을 입력 합니다. 예: client1 client2 합니다. 최대 5 명의 클라이언트 컨트롤러를 사용할 수 있습니다. 클라이언트 컴퓨터를 하나, 물리적 또는 가상 SQL Server Distributed Replay client 라는 Windows 서비스를 실행 하는입니다. 여러 Distributed Replay Client가 함께 작동하여 SQL Server 인스턴스에 대해 작업을 시뮬레이션합니다. 각 Distributed Replay 환경에 하나 이상의 클라이언트가 있을 수 있습니다.
1.  **다음**을 선택합니다.

### <a name="select-a-trace"></a>추적을 선택 합니다.

1.  **추적 파일의 경로를**: 입력된 추적 (.trc) 파일로 경로 입력 합니다.
1.  **재생을 저장할 경로를 전처리 출력**:  
    \- IRF 파일이 없는 경우 IRF 파일을 저장 하려는 위치로 경로 입력 하 고 기타 전처리 출력 합니다.  
    \- IRF 파일에 이미 있는 경우 IRF 파일 경로 입력 합니다.
1. **다음**을 선택합니다.

### <a name="replay-a-trace"></a>추적 재생

1.  **추적 파일 이름이**: 추적 파일 이름을 입력 합니다.
1.  **최대 파일 크기 (MB)** : 추적 파일 롤오버 크기 값을 입력 합니다. 기본값은 200mb입니다. 사용자 지정 값을 입력할 수 있습니다.
1.  **재생 추적 출력을 저장할 경로를**: 출력.trc 파일에 대 한 경로 입력 합니다.
1.  **SQL Server 인스턴스 이름을**:  추적 재생에 SQL Server 인스턴스의 이름을 입력 합니다.
1.  **시작**을 선택합니다.

입력 한 정보가 올바른 경우에 Distributed Replay 프로세스가 시작 됩니다. 그렇지 않으면 잘못 된 정보가 포함 된 텍스트 boses 빨간색으로 강조 표시 됩니다. 입력 한 값 잘못 되어 선택한 했는지 **시작**합니다.

재생이 완료 될 때까지 대기 합니다. 지정 된 위치를 실행 합니다. 재생 진행률을 모니터링 하려면 왼쪽된 메뉴의 맨 아래에 있는 종 모양 아이콘을 선택 합니다.

![재생 추적 진행률](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>추적 재생에 대 한 질문과 대답

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>보안 권한을 내 대상 서버에서 재생 캡처를 시작 하나요?

- 비활성화 응용 프로그램에서 추적 작업을 실행 하는 Windows 사용자는 SQL Server를 실행 하는 대상 컴퓨터에서 sysadmin 권한이 있어야 합니다. 추적을 시작 하려면 이러한 사용자 권한이 필요 합니다.
- 지정 된 추적 파일 경로에 SQL Server를 실행 하는 대상 컴퓨터는 실행 중인 서비스 계정에 쓰기 권한이 있어야 합니다.
- Distributed Replay Client 서비스를 실행 중인 서비스 계정에 SQL Server를 실행 하는 대상 컴퓨터에 연결 하 고 쿼리를 실행할 권한이 있어야 합니다.

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>동일한 세션에서 둘 이상의 재생 시작

예, 여러 재생을 시작 하 고 완료 될 때까지 동일한 세션의 추적 수 있습니다.

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>동시에 둘 이상의 재생 시작

예, 하지만 집합에서 선택한 컴퓨터와 동일한 **컨트롤러와 클라이언트**합니다. 컨트롤러 및 클라이언트 사용 됩니다. 아래에 있는 컴퓨터의 개별 집합을 설정 **컨트롤러와 클라이언트** 병렬 재생을 시작 합니다.

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>재생을 일반적으로 얼마를 완료 하려면?

원본 추적으로 동일한 기간 및 소스 추적을 전처리 하는 데 걸리는 시간에 일반적으로 재생을 사용 합니다. 그러나 컨트롤러를 사용 하 여 등록 된 클라이언트 컴퓨터 재생에서 생성 되는 부하를 관리 하는 데 충분 하지 않으면 재생을 완료 하는 데 더 걸릴 수 있습니다. 컨트롤러를 사용 하 여 최대 16 개의 클라이언트 컴퓨터를 등록할 수 있습니다.

### <a name="how-large-do-target-trace-files-get"></a>얼마나 큰 추적 파일 대상 합니까?

5 월 15 일 까지의 파일 것일 대상 추적 소스는 추적 크기가 시간입니다. 파일 크기를 얼마나 많은 쿼리가 실행 되는 기반으로 합니다. 예를 들어 쿼리 계획 blob 클 수 있습니다. 이러한 쿼리에 대 한 통계를 자주 변경 하는 경우 더 많은 이벤트가 캡처됩니다.

### <a name="why-do-i-need-to-restore-databases"></a>데이터베이스를 복원 해야 하는 이유는 합니까?

SQL Server가 상태 저장 관계형 데이터베이스 관리 시스템입니다. 제대로 A를 실행 하려면 / B 테스트, 데이터베이스의 상태를 항상 유지 되어야 합니다. 그렇지 않은 경우 프로덕션에 나타나지는 재생 하는 동안 쿼리에서 오류를 볼 수 있습니다. 이러한 오류를 방지 하려면 원본 캡처 직전 백업을 수행 하는 것이 좋습니다. 마찬가지로, SQL Server를 실행 하는 대상 컴퓨터의 백업을 복원 하는 재생 하는 동안 오류가 발생 하지 않도록 해야 합니다.

### <a name="what-does-pass--on-the-replay-page-mean"></a>"통과 %" 재생 페이지 mean?

**% 전달** 쿼리의 백분율만 전달 하는 것을 의미 합니다. 오류 수가 필요 여부를 진단할 수 있습니다. 오류를 예상할 수 또는 데이터베이스에서 손실 무결성 있으므로 오류가 발생할 수 있습니다. 경우에 대 한 값 **패스 %** 예상 대로 되지 않습니다. 추적을 중지 하 고 쿼리 실패를 보려면 SQL Profiler 추적 파일을 확인 합니다.

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>재생 하는 동안 수집 된 추적 이벤트를 살펴볼 수는 방법

대상 추적 파일을 열고 SQL Profiler에 보고 합니다. 모든 SQL Server 스크립트를 c:로 사용할 재생 캡처를 수정 하려는 경우 또는\\프로그램 파일 (x86)\\Microsoft Corporation\\데이터베이스 실험 도우미\\스크립트\\ StartReplayCapture.sql 합니다.

### <a name="what-trace-events-does-dea-collect-during-replay"></a>추적 이벤트는 비활성화 수집 재생 하는 동안 합니까?

비활성화는 성능 관련 정보가 포함 된 추적 이벤트를 캡처합니다. 캡처 구성이 StartReplayCaptureTrace.sql 스크립트입니다. 이러한 이벤트는에 나와 있는 일반적인 SQL Server 추적 이벤트를 [sp_trace_setevent (TRANSACT-SQL) 참조 설명서](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)합니다.

## <a name="troubleshoot-trace-replay"></a>추적 재생 문제 해결

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>SQL Server를 실행 하는 컴퓨터에 연결할 수 없습니다.

- SQL Server를 실행 하는 컴퓨터의 이름이 올바른지 확인 합니다. 를 확인 하려면 SQL Server Management Studio (SSMS)를 사용 하 여 서버에 연결 하려고 합니다.
- 방화벽 구성을 SQL Server를 실행 하는 컴퓨터에 대 한 연결을 차단 하지 확인 합니다.
- 사용자는 필요한 사용자 권한이 있는지 확인 합니다.
- Distributed Replay client의 서비스 계정에 SQL Server를 실행 하는 컴퓨터에 대 한 액세스를 확인 합니다.

% Temp %에 로그에서 자세한 내용을 확인할 수 있습니다\\비활성화 합니다. 문제가 지속 되 면 제품 팀에 문의 합니다.

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>Distributed Replay controller 연결할 수 없습니다.

- Distributed Replay controller 서비스 컨트롤러 컴퓨터에서 실행 되 고 있는지 확인 합니다. 확인 하려면 Distributed Replay 관리 도구를 사용 (명령을 실행 하 여 `dreplay.exe status -f 1`).
- 재생 원격으로 시작 하는 경우:
  - 비활성화를 실행 하는 컴퓨터는 컨트롤러를 성공적으로 ping 수 있는지 확인 합니다. 방화벽 설정에서 지침에 따라 연결을 허용 하는지 확인 합니다 **Replay 환경 구성** 페이지입니다. 자세한 내용은 문서 참조 [SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)합니다.
  - DCOM 원격 시작 및 원격 활성화는 Distributed Replay controller의 사용자에 대해 허용 해야 합니다.
  - Distributed Replay controller의 사용자에 대 한 DCOM 원격 액세스 권한이 허용 됩니다 있는지를 확인 합니다.

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>내 컴퓨터에서 추적 파일 경로가 있습니다. Distributed Replay controller를 이유 찾지 못하셨습니까?

Distributed Replay만 로컬 디스크 리소스에 액세스할 수 있습니다. 원본 추적 파일 재생을 시작 하기 전에 Distributed Replay 컨트롤러 컴퓨터에 복사 해야 합니다. 비활성화에서 경로 제공 해야는 또한 **새 재생** 페이지입니다. 

UNC 경로 Distributed Replay를 사용 하 여 호환 되지 않습니다. Distributed Replay 경로 확장명을 포함 하는 첫 번째 원본 추적 파일에 대 한 로컬, 절대 경로 여야 합니다.

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>새 재생 페이지의 파일에 대 한 찾아볼 수 없습니다는 이유

원격 컴퓨터의 폴더를 찾아볼 수 없습니다 것, 때문에 유용 하지 파일을 검색 합니다. 복사 및 붙여넣기 절대 경로 더 효율적입니다.

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>Distributed Replay 모든 이벤트를 재생 하지 않은 하지만 추적을 사용 하 여 재생을 시작 했습니다.

추적 파일 하거나 재생 가능한 이벤트가 없거나 이벤트를 재생 하는 방법에 대 한 정보를 없기 때문에이 문제가 발생할 수 있습니다. 추적 파일 경로가 제공 된 원본 추적 파일 인지 확인 합니다. 원본 추적 파일 StartCaptureTrace.sql 스크립트에 제공 된 구성을 사용 하 여 만들어집니다.

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>"예기치 않은 오류가 발생 했습니다!" 표시 SQL Server 2017 Distributed Replay controller를 사용 하 여 추적 파일을 전처리 하 려 할 때

이 문제는 SQL Server 2017의 RTM 버전에서 이라고 합니다. 자세한 내용은 [DReplay 기능을 사용 하 여 SQL Server 2017에서 캡처된 추적을 재생할 때 예기치 않은 오류](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)합니다.  
  
SQL Server 2017에 대 한 최신 누적 업데이트 1에서 문제가 해결 되었습니다. 최신 버전을 다운로드 [SQL Server 2017 용 누적 업데이트 1](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)합니다.

## <a name="next-steps"></a>다음 단계

- 제안 된 변경 내용에 대 한 정보를 얻을 수 있도록 분석 보고서를 참조 하세요 [보고서를 만들](database-experimentation-assistant-create-report.md)합니다.

- 비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
