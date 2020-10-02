---
title: SQL Server 업그레이드에 대 한 추적 재생
description: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미를 사용 하 여 캡처된 추적을 재생 하는 방법을 알아봅니다.
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
ms.openlocfilehash: fa37fb348aa94e59ac3816d523cc5a30bc314713
ms.sourcegitcommit: 71d2389cf27156fa0404a6e6f65fb7a61c40789a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91636173"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 추적 재생

데이터베이스 실험 도우미 (DEA)에서는 업그레이드 된 테스트 환경에 대해 캡처된 추적 파일을 재생할 수 있습니다. 예를 들어 SQL Server 2008 r 2에서 실행 되는 프로덕션 워크 로드를 살펴보겠습니다. 워크 로드에 대 한 추적 파일은 프로덕션 환경에서 실행 되는 동일한 버전의 SQL Server 환경에서 한 번, 업그레이드 대상 SQL Server 버전 (예: 2016 SQL Server)이 있는 환경에서 두 번째로 재생 되어야 합니다.

> [!NOTE]
> 추적을 재생 하려면 Distributed Replay 추적을 실행 하는 가상 컴퓨터 또는 물리적 컴퓨터를 수동으로 설정 해야 합니다. 자세한 내용은 [Configure Distributed Replay for 데이터베이스 실험 도우미](database-experimentation-assistant-configure-replay.md)을 참조 하세요.
>

## <a name="configure-a-trace-replay-for-target-1"></a>대상 1에 대 한 추적 재생 구성

먼저 기존 프로덕션 환경을 나타내는 대상 1에 대해 추적 재생을 수행 해야 합니다.

1. DEA의 왼쪽 탐색 모음에서 화살표 아이콘을 선택 하 고 **모든 재생** 페이지에서 **새 재생**을 선택 합니다.

    ![DEA에서 재생 만들기](./media/database-experimentation-assistant-replay-trace/dea-create-replay.png)

    > [!NOTE]
    > Distributed Replay 컨트롤러 컴퓨터를 사용 하려면 원격으로 연결 하는 데 사용 하는 사용자 계정에 대 한 권한이 필요 합니다.

2. **새 재생** 페이지의 **재생 세부 정보**에서 다음 정보를 입력 하거나 선택 합니다.

    - **재생 이름**: 추적 재생의 이름을 입력 합니다.
    - **원본 추적 형식**: 원본 추적 파일의 형식 (Trace 또는 xevent)을 지정 합니다.
    - **소스 파일의 전체 경로**: 원본 추적 파일의 전체 경로를 지정 합니다. DReplay를 사용 하는 경우 파일은 DReplay 컨트롤러 역할을 하는 컴퓨터에 있어야 하 고 사용자 계정에는 파일 및 폴더에 대 한 액세스 권한이 있어야 합니다.
    - **재생 도구**: 재생 도구 (DReplay 또는 기본 제공)를 지정 합니다.
    - **컨트롤러 컴퓨터 이름**: Distributed Replay 컨트롤러 역할을 하는 컴퓨터의 이름을 지정 합니다.
    - **재생 추적 위치**: 추적 재생에 연결 된 추적 파일/xevent을 저장할 경로를 지정 합니다.

        > [!NOTE]
        > Azure SQL Database 또는 Azure SQL Managed Instance의 경우 Azure blob 저장소 계정의 SAS URI를 제공 해야 합니다.

3. **예, 데이터베이스를 수동으로 복원** 했습니다. 확인란을 선택 하 여 데이터베이스를 복원 했는지 확인 합니다.

4. **SQL Server 연결 세부 정보**에서 다음 정보를 입력 하거나 선택 합니다.

    - **서버 유형**: SQL Server의 유형 (**SqlServer**, **AzureSqlDb**, **AzureSqlManagedInstance**)을 지정 합니다.
    - **서버 이름**: SQL Server의 서버 이름 또는 IP 주소를 지정 합니다.
    - **인증 유형**: 인증 유형으로 **Windows**를 선택 합니다.
    - **데이터베이스 이름**: 서버 쪽 추적을 시작할 데이터베이스의 이름을 입력 합니다. 데이터베이스를 지정 하지 않으면 서버에 있는 모든 데이터베이스에서 추적이 캡처됩니다.

5. 시나리오에 적절 한 **연결 암호화** 및 **서버 인증서 신뢰** 확인란을 선택 하거나 선택 취소 합니다.

    ![새 재생 페이지](./media/database-experimentation-assistant-replay-trace/dea-new-replay.png)

## <a name="start-the-trace-replay-on-target-1"></a>대상 1에서 추적 재생 시작

- 필요한 정보를 입력 하거나 선택한 후 **시작** 을 선택 하 여 추적 재생을 시작 합니다.

  입력 한 정보가 유효 하면 Distributed Replay 프로세스가 시작 됩니다. 그렇지 않으면 잘못 된 정보가 있는 텍스트 상자가 빨간색으로 강조 표시 됩니다. 입력 한 값이 올바른지 확인 한 다음 **시작**을 선택 합니다.

  ![대상 1에 대 한 재생 진행률](./media/database-experimentation-assistant-replay-trace/dea-run-replay-target1.png)

  필요에 따라 프로세스를 모니터링할 수 있습니다. 재생이 완료 되 면 DEA은 지정한 위치에 파일에 결과를 저장 합니다.

  ![대상 1의 재생 완료](./media/database-experimentation-assistant-replay-trace/dea-replay-target1-complete.png)

## <a name="perform-the-trace-replay-against-target-2"></a>대상 2에 대해 추적 재생 수행

대상 1에 대 한 추적 재생 수행을 완료 한 후에는 원하는 업그레이드 환경을 나타내는 두 번째 대상에 대해 동일한 작업을 수행 해야 합니다.

1. 이번에는 대상 2 환경과 연결 된 세부 정보를 사용 하 여 추적 재생을 구성 합니다.
2. 대상 2에서 추적 재생을 시작 합니다.

   필요에 따라 프로세스를 모니터링할 수 있습니다. 재생이 완료 되 면 DEA은 지정한 위치에 파일에 결과를 저장 합니다.

## <a name="frequently-asked-questions-about-trace-replay"></a>추적 재생에 대 한 질문과 대답

**Q: 대상 서버에서 재생 캡처를 시작 하려면 어떤 보안 권한이 필요 한가요?**

- DEA 응용 프로그램에서 추적 작업을 실행 하는 Windows 사용자에 게 SQL Server를 실행 하는 대상 컴퓨터에 대 한 sysadmin 권한이 있어야 합니다. 이러한 사용자 권한은 추적을 시작 하는 데 필요 합니다.
- SQL Server를 실행 하는 대상 컴퓨터가 실행 되는 서비스 계정에는 지정 된 추적 파일 경로에 대 한 쓰기 권한이 있어야 합니다.
- Distributed Replay 클라이언트 서비스를 실행 하는 서비스 계정에는 SQL Server를 실행 하는 대상 컴퓨터에 연결 하 고 쿼리를 실행할 수 있는 사용자 권한이 있어야 합니다.

**Q: 동일한 세션에서 둘 이상의 재생을 시작할 수 있나요?**

예, 여러 재생을 시작 하 고 동일한 세션에서 완료 될 때까지 추적할 수 있습니다.

**Q: 둘 이상의 재생을 동시에 시작할 수 있나요?**

예. 단, **컨트롤러와 클라이언트**에서 선택한 것과 동일한 컴퓨터 집합이 아닙니다. 컨트롤러와 클라이언트는 사용 중입니다. **컨트롤러 Plus 클라이언트** 에서 별도의 컴퓨터 집합을 설정 하 여 병렬 재생을 시작 합니다.

**Q: 재생은 일반적으로 완료 하는 데 걸리는 시간**

재생은 일반적으로 소스 추적과 원본 추적을 전처리 하는 데 걸리는 시간을 더한 시간을 사용 합니다. 그러나 컨트롤러에 등록 된 클라이언트 컴퓨터에서 재생에서 생성 된 부하를 관리 하기에 충분 하지 않은 경우 재생을 완료 하는 데 시간이 더 오래 걸릴 수 있습니다. 컨트롤러를 사용 하 여 최대 16 개의 클라이언트 컴퓨터를 등록할 수 있습니다.

**Q: 대상 추적 파일의 크기는 어느 정도 인가요?**

대상 추적 파일은 원본 추적 크기의 5 ~ 15 배 사이가 될 수 있습니다. 파일 크기는 실행 되는 쿼리 수에 따라 달라 집니다. 예를 들어 쿼리 계획 blob는 클 수 있습니다. 이러한 쿼리에 대 한 통계가 자주 변경 되 면 더 많은 이벤트가 캡처됩니다.

**Q: 데이터베이스를 복원 해야 하는 이유는 무엇 인가요?**

SQL Server은 상태 저장 관계형 데이터베이스 관리 시스템입니다. A/B 테스트를 제대로 실행 하려면 항상 데이터베이스 상태를 유지 해야 합니다. 그렇지 않으면 재생 중에 프로덕션에 표시 되지 않는 오류가 표시 될 수 있습니다. 이러한 오류를 방지 하려면 원본 캡처 바로 전에 백업을 수행 하는 것이 좋습니다. 마찬가지로, 재생 하는 동안 오류를 방지 하려면 SQL Server를 실행 하는 대상 컴퓨터에서 백업을 복원 해야 합니다.

**Q: 재생 페이지의 "통과%"는 무엇을 의미 하나요?**

**통과%** 는 쿼리 비율만 전달 됨을 의미 합니다. 오류 수가 예상 되는지 여부를 진단할 수 있습니다. 오류가 발생 하거나 데이터베이스의 무결성이 손실 되어 오류가 발생할 수 있습니다. **Pass%** 에 대 한 값이 잘못 된 경우 추적을 중지 하 고 SQL Profiler에서 추적 파일을 확인 하 여 실패 한 쿼리가 있는지 확인할 수 있습니다.

**Q: 재생 중 수집 된 추적 이벤트를 어떻게 확인할 수 있나요?**

대상 추적 파일을 열고 SQL Profiler에서 봅니다. 또는 재생 캡처를 수정 하려는 경우 모든 SQL Server 스크립트를 C: \\ Program Files (x86) \\ Microsoft Corporation \\ 데이터베이스 실험 도우미 \\ 스크립트 \\ startreplaycapture. SQL에서 사용할 수 있습니다.

**Q: 재생 하는 동안 DEA에서 수집 하는 추적 이벤트는 무엇입니까?**

DEA는 성능 관련 정보를 포함 하는 추적 이벤트를 캡처합니다. 캡처 구성은 StartReplayCaptureTrace 스크립트에 있습니다. 이러한 이벤트는 [sp_trace_setevent (transact-sql) 참조 설명서](../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)에 나열 된 추적 이벤트 SQL Server 일반적인 이벤트입니다.

## <a name="troubleshoot-trace-replay"></a>추적 재생 문제 해결

**Q: SQL Server를 실행 하는 컴퓨터에 연결할 수 없는 이유는 무엇입니까?**

- SQL Server를 실행 하는 컴퓨터의 이름이 올바른지 확인 합니다. 확인 하려면 SSMS (SQL Server Management Studio)를 사용 하 여 서버에 연결을 시도 합니다.
- 방화벽 구성이 SQL Server를 실행 하는 컴퓨터에 대 한 연결을 차단 하지 않는지 확인 합니다.
- 사용자에 게 필요한 사용자 권한이 있는지 확인 합니다.
- Distributed Replay 클라이언트의 서비스 계정에 SQL Server를 실행 하는 컴퓨터에 대 한 액세스 권한이 있는지 확인 합니다.

% Temp% DEA의 로그에서 자세한 내용을 볼 수 있습니다 \\ . 문제가 지속 되 면 제품 팀에 문의 하십시오.

**Q: Distributed Replay 컨트롤러에 연결할 수 없는 이유는 무엇입니까?**

- 컨트롤러 컴퓨터에서 Distributed Replay controller 서비스가 실행 중인지 확인 합니다. 확인 하려면 Distributed Replay 관리 도구 (명령 실행)를 사용 `dreplay.exe status -f 1` 합니다.
- 재생이 원격으로 시작 되는 경우:
  - DEA를 실행 하는 컴퓨터가 컨트롤러를 성공적으로 ping 할 수 있는지 확인 합니다. **재생 환경 구성** 페이지의 지침에 따라 방화벽 설정에서 연결을 허용 하는지 확인 합니다. 자세한 내용은 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md?view=sql-server-2017)문서를 참조 하세요.
  - Distributed Replay 컨트롤러의 사용자에 대해 DCOM 원격 시작 및 원격 활성화가 허용 되는지 확인 합니다.
  - Distributed Replay 컨트롤러의 사용자에 대해 DCOM 원격 액세스 사용자 권한이 허용 되는지 확인 합니다.

**Q: 추적 파일 경로가 내 컴퓨터에 있습니다. 컨트롤러를 찾을 Distributed Replay 없는 이유는 무엇입니까?**

Distributed Replay 로컬 디스크 리소스에만 액세스할 수 있습니다. 재생을 시작 하기 전에 원본 추적 파일을 Distributed Replay 컨트롤러 컴퓨터에 복사 해야 합니다. 또한 DEA **새 재생** 페이지에서 경로를 제공 해야 합니다.

UNC 경로는 Distributed Replay와 호환 되지 않습니다. Distributed Replay 경로는 확장을 포함 하 여 첫 번째 소스 추적 파일의 절대 로컬 경로 여야 합니다.

**Q: 새 재생 페이지에서 파일을 찾을 수 없는 이유는 무엇입니까?**

원격 컴퓨터에서 폴더를 검색할 수 없으므로 파일 검색은 유용 하지 않습니다. 절대 경로를 복사 하 여 붙여 넣는 것이 더 효율적입니다.

**Q: 추적으로 재생을 시작 했지만 이벤트를 재생 하지 Distributed Replay. 굳이?**

추적 파일에 재생 가능한 이벤트가 없거나 이벤트 재생 방법에 대 한 정보가 있는 경우이 문제가 발생할 수 있습니다. 제공 된 추적 파일 경로가 원본 추적 파일을 가리키는지 여부를 확인 합니다. 원본 추적 파일은 StartCaptureTrace 스크립트에서 제공 하는 구성을 사용 하 여 만들어집니다.

**Q: SQL Server 2017 Distributed Replay 컨트롤러를 사용 하 여 추적 파일을 전처리 하려고 하면 "예기치 않은 오류가 발생 했습니다."가 표시 됩니다. 굳이?**

이 문제는 SQL Server 2017의 RTM 버전에서 알려져 있습니다. 자세한 내용은 [2017 SQL Server에서 캡처 기능을 사용 하 여 캡처된 추적을 재생 하는 경우 예기치 않은 오류](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)를 참조 하세요.  
  
SQL Server 2017에 대 한 최신 누적 업데이트 1에서이 문제가 해결 되었습니다. [SQL Server 2017에 대 한 최신 버전의 누적 업데이트 1](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)을 다운로드 합니다.

## <a name="see-also"></a>참조

- 제안 된 변경 내용에 대 한 정보를 얻는 데 도움이 되는 분석 보고서를 만들려면 [보고서 만들기](database-experimentation-assistant-create-report.md)를 참조 하세요.