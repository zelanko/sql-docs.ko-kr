---
title: 데이터베이스 실험 도우미 개요
description: 데이터베이스 실험 도우미 개요
ms.custom: seo-lt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 7180656f8a4779c43f4c691f583aaaf5fcbf86d0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056579"
---
# <a name="overview-of-database-experimentation-assistant"></a>데이터베이스 실험 도우미 개요

DEA (데이터베이스 실험 도우미)는 SQL Server 업그레이드를 위한 실험 솔루션입니다. DEA는 특정 작업에 대 한 대상 버전의 SQL Server을 평가 하는 데 도움이 됩니다. 이전 SQL Server 버전 (2005부터)에서 최신 버전의 SQL Server로 업그레이드 하는 고객은 도구가 제공 하는 분석 메트릭을 사용할 수 있습니다.

DEA 분석 메트릭은 다음과 같습니다.

- 호환성 오류가 있는 쿼리
- 저하 된 쿼리 및 쿼리 계획
- 기타 워크 로드 비교 데이터

비교 데이터는 더 높은 신뢰도와 성공적인 업그레이드 환경을 유발할 수 있습니다.

## <a name="get-dea"></a>DEA 가져오기

DEA를 설치 하려면 최신 버전의 도구를 [다운로드](https://www.microsoft.com/download/details.aspx?id=54090) 합니다. 그런 다음 **DatabaseExperimentationAssistant** 파일을 실행 합니다.

## <a name="solution-architecture-for-comparing-workloads"></a>워크 로드 비교를 위한 솔루션 아키텍처

다음 다이어그램에서는 워크 로드 비교에 대 한 솔루션 아키텍처를 보여 줍니다. 작업 비교는 SQL Server 2008에서 SQL Server 2016로 업그레이드 하는 동안 DEA 및 Distributed Replay를 사용 합니다.

![워크 로드 비교 솔루션 아키텍처](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>DEA 필수 구성 요소

DEA를 실행 하기 위한 몇 가지 필수 구성 요소는 다음과 같습니다.

- 최소 하드웨어 요구 사항: 3.5 GB의 RAM이 있는 단일 코어 컴퓨터입니다.
- 이상적인 하드웨어 요구 사항: 8 코어 CPU (3.5 GB 이상의 RAM 이상). 코어 수가 8 개를 초과 하는 프로세서는 DEA 런타임을 향상 시 키 지 않습니다.
- A, B 및 보고서 분석 데이터베이스를 저장 하려면 성능 추적 크기의 추가 33%가 필요 합니다.

## <a name="configure-dea"></a>DEA 구성

필수 구성 요소 환경 아키텍처에서는 *Distributed Replay 컨트롤러와 동일한 컴퓨터에*DEA를 설치 하는 것이 좋습니다. 이 방법을 통해 시스템 간 호출을 방지 하 고 구성을 간소화 합니다.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>DEA를 사용 하 여 작업 비교에 필요한 구성

DEA는 Windows 인증을 사용 하 여 데이터베이스 서버에 연결 합니다. DEA를 실행 하는 사용자가 Windows 인증을 사용 하 여 데이터베이스 서버 (원본, 대상 및 분석)에 연결할 수 있는지 확인 합니다.

**캡처 구성 요구 사항**:

- DEA를 실행 하는 사용자는 Windows 인증을 사용 하 여 원본 데이터베이스 서버에 연결할 수 있습니다.
- DEA를 실행 하는 사용자에 게 원본 데이터베이스 서버에 대 한 sysadmin 권한이 있습니다.
- 원본 데이터베이스 서버를 실행 하는 서비스 계정에는 추적 폴더 경로에 대 한 쓰기 권한이 있습니다.

자세한 내용은 [캡처 FAQ](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture) 를 참조 하세요.

**재생 구성 요구 사항**: 

- DEA를 실행 하는 사용자는 Windows 인증을 사용 하 여 대상 데이터베이스 서버에 연결할 수 있습니다.
- DEA를 실행 하는 사용자에 게 대상 데이터베이스 서버에 대 한 sysadmin 권한이 있습니다.
- 대상 데이터베이스 서버를 실행 하는 서비스 계정에는 추적 폴더 경로에 대 한 쓰기 권한이 있습니다.
- Distributed Replay 클라이언트를 실행 하는 서비스 계정은 Windows 인증을 사용 하 여 대상 데이터베이스 서버에 연결할 수 있습니다.
- DEA는 COM 인터페이스를 사용 하 여 Distributed Replay 컨트롤러와 통신 합니다. Distributed Replay 컨트롤러에서 들어오는 요청에 대해 TCP 포트가 열려 있는지 확인 합니다.

자세한 내용은 [재생 FAQ](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay) 를 참조 하세요.

**분석 구성 요구 사항**:

- DEA를 실행 하는 사용자는 Windows 인증을 사용 하 여 분석 데이터베이스 서버에 연결할 수 있습니다.
- DEA를 실행 하는 사용자에 게 원본 데이터베이스 서버에 대 한 sysadmin 권한이 있습니다.

자세한 내용은 [분석 FAQ](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports) 를 참조 하세요.

## <a name="set-up-telemetry"></a>원격 분석 설정

DEA에는 원격 분석 정보를 Microsoft에 보낼 수 있는 인터넷 사용 기능이 있습니다. Microsoft는 제품 환경을 개선 하기 위해 원격 분석을 수집 합니다. 원격 분석은 선택 사항입니다. 수집 되는 정보는 로컬 감사를 위해 컴퓨터에도 저장 됩니다. 수집 된 항목을 언제 든 지 볼 수 있습니다. DEA의 모든 로그 파일 은% temp%\\DEA 폴더에 저장 됩니다.

수집 되는 이벤트를 결정할 수 있습니다. 수집 된 이벤트를 Microsoft에 보낼지 여부도 결정 합니다. 이벤트에는 다음과 같은 네 가지 유형이 있습니다.

- **Traceevent**: 응용 프로그램에 대 한 사용 이벤트 (예: "트리거된 캡처 중지")입니다.
- **예외**: 응용 프로그램을 사용 하는 동안 예외가 throw 되었습니다.
- **DiagnosticEvent**: 문제가 발생 하는 경우 진단에 도움이 되는 이벤트 로그 (Microsoft로 보내지지*않음* )입니다.
- **FeedbackEvent**: 응용 프로그램을 통해 제출 된 사용자 의견입니다.

이러한 단계에서는 수집 되는 이벤트와 이벤트를 Microsoft로 보낼지 여부를 선택 하는 방법을 보여 줍니다.

1. DEA가 설치 된 위치 (예: C:\\Program Files (x86)\\Microsoft Corporation\\데이터베이스 실험 도우미)로 이동 합니다.
2. 두 .config 파일 인 DEA (응용 프로그램용) 및 DEACmd .exe .config (CLI의 경우)를 엽니다.
3. 이벤트 유형 수집을 중지 하려면 *이벤트* 의 값 (예: **traceevent**)을 **false**로 설정 합니다. 이벤트 수집을 다시 시작 하려면 값을 **true**로 설정 합니다.
4. 이벤트의 로컬 복사본을 저장 하는 것을 중지 하려면 **TraceLoggerEnabled** 의 값을 **false**로 설정 합니다. 로컬 복사본 저장을 다시 시작 하려면 값을 **true**로 설정 합니다.
5. Microsoft로의 이벤트 전송을 중지 하려면 **AppInsightsLoggerEnabled** 의 값을 **false**로 설정 합니다. Microsoft로 이벤트를 다시 보내기 시작 하려면 값을 **true**로 설정 합니다.

DEA은 [Microsoft 개인 정보 취급 방침](https://aka.ms/dea-privacy)의 적용을 받습니다.

## <a name="next-steps"></a>다음 단계

[시작](database-experimentation-assistant-get-started.md) 에서는 추적을 캡처, 재생 및 분석 하는 데 필요한 단계를 안내 합니다.
