---
title: 업그레이드 하는 SQL Server에 대 한 데이터베이스 실험 도우미 솔루션의 개요
description: 데이터베이스 실험 도우미의 개요
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 1c2a28a5dc83d22a327bf797358d5edae69eb82b
ms.sourcegitcommit: 9ea11d738503223b46d2be5db6fed6af6265aecc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/07/2019
ms.locfileid: "56987829"
---
# <a name="overview-of-database-experimentation-assistant"></a>데이터베이스 실험 도우미의 개요

데이터베이스 실험 도우미 (비활성화)에 SQL Server 업그레이드에 대 한 실험 솔루션입니다. 비활성화는 특정 워크 로드에 대 한 SQL Server의 대상된 버전을 평가할 수 있습니다. 이전 SQL Server 버전 (2005부터 시작)에서 SQL Server의 최신 버전으로 업그레이드 하는 고객 도구에서 제공 하는 분석 메트릭을 사용 하 여 수 있습니다. 

비활성화 분석 메트릭은 다음과 같습니다.
- 호환성 오류가 있는 쿼리
- 성능이 저하 된 쿼리 및 쿼리 계획
- 다른 작업 부하 비교 데이터

비교 데이터 신뢰도 높은 및 업그레이드 환경이 성공적 이면 발생할 수 있습니다.

비활성화 하는 데모 19 분 소개의 경우 다음 동영상을 시청 합니다.

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]

## <a name="get-dea"></a>비활성화를 가져오기

비활성화를 설치 하려면 [다운로드](https://www.microsoft.com/download/details.aspx?id=54090) 도구의 최신 버전입니다. 그런 다음 실행 합니다 **DatabaseExperimentationAssistant.exe** 파일입니다.

## <a name="solution-architecture-for-comparing-workloads"></a>워크 로드를 비교 하기 위한 솔루션 아키텍처

다음 다이어그램은 작업 부하 비교에 대 한 솔루션 아키텍처를 보여 줍니다. SQL Server 2008에서 SQL Server 2016로 업그레이드 하는 동안 비활성화 및 Distributed Replay를 사용 하는 작업 부하 비교 합니다.

![작업 부하 비교 솔루션 아키텍처](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>필수 구성 요소 비활성화

다음은 비활성화를 실행 하기 위한 일부 필수 구성 요소입니다.
- 최소 하드웨어 요구 사항: 3.5GB RAM 사용 하 여 단일 코어 컴퓨터입니다.
- 이상적인 하드웨어 요구 사항: 8 코어 CPU (3.5GB RAM 이상). 프로세서 8 개 이상의 코어가 있는 비활성화는 런타임을 개선 하지 않습니다.
- 성능 추적 크기의 추가 33 %A, B 및 보고서 분석 데이터베이스가 필요 합니다.

## <a name="configure-dea"></a>비활성화를 구성 합니다.

환경 필수 구성 요소 아키텍처에서는 비활성화를 설치 하는 권장 *Distributed Replay controller와 동일한 컴퓨터에*입니다. 이 방법은 컴퓨터 간 호출을 방지 하 고 구성을 간소화 합니다.

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>비활성화를 사용 하 여 작업 부하 비교에 대 한 필수 구성

비활성화는 Windows 인증을 사용 하 여 데이터베이스 서버에 연결 합니다. Windows 인증을 사용 하 여 비활성화를 실행 하는 사용자 데이터베이스 서버 (원본, 대상 및 분석)에 연결할 수 있는지 확인 해야 합니다.

**구성 요구 사항 캡처**:

*   비활성화를 실행 하는 사용자는 Windows 인증을 사용 하 여 원본 데이터베이스 서버에 연결할 수 있습니다.
*   비활성화를 실행 하는 사용자에 원본 데이터베이스 서버에 대 한 sysadmin 권한이 있습니다.
*   원본 데이터베이스 서버를 실행 하는 서비스 계정 추적 폴더 경로에 쓰기 액세스할 수 있습니다.

자세한 내용은 참조는 [FAQ 캡처](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**재생 구성 요구 사항**: 

*   비활성화를 실행 하는 사용자는 Windows 인증을 사용 하 여 대상 데이터베이스 서버에 연결할 수 있습니다.
*   비활성화를 실행 하는 사용자에 대상 데이터베이스 서버에 대 한 sysadmin 권한이 있습니다.
*   대상 데이터베이스 서버를 실행 하는 서비스 계정 추적 폴더 경로에 쓰기 액세스할 수 있습니다.
*   Distributed Replay client를 실행 하는 서비스 계정 Windows 인증을 사용 하 여 대상 데이터베이스 서버를 연결할 수 있습니다.
*   비활성화는 COM 인터페이스를 사용 하 여 Distributed Replay controller와 통신 합니다. Distributed Replay 컨트롤러에서 들어오는 요청에 대 한 TCP 포트가 열려 있는지 확인 합니다.

자세한 내용은 참조는 [FAQ를 재생 합니다.](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**분석 구성 요구 사항**: 

*   비활성화를 실행 하는 사용자는 Windows 인증을 사용 하 여 분석 데이터베이스 서버에 연결할 수 있습니다.
*   비활성화를 실행 하는 사용자에 원본 데이터베이스 서버에 대 한 sysadmin 권한이 있습니다.

자세한 내용은 참조는 [분석 FAQ](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>원격 분석 설정

비활성화가 Microsoft에 원격 분석 정보를 보낼 수 있는 인터넷 사용 기능을 합니다. Microsoft 제품 환경을 개선 하기 위해 원격 분석을 수집 합니다. 원격 분석은 선택 사항입니다. 수집 되는 정보는 로컬 감사를 위해 컴퓨터에 저장 됩니다. 항상 수집 되는 항목을 볼 수 있습니다. 비활성화에서 모든 로그 파일은 %temp% 저장 됩니다\\비활성화 폴더입니다.

수집할 이벤트를 결정할 수 있습니다. 또한 수집 된 이벤트를 Microsoft로 보낼지 여부를 결정 합니다. 네 가지 유형의 이벤트는

*   **TraceEvent**: 응용 프로그램 (예: "트리거 중지 캡처")에 대 한 이벤트를 사용 합니다.
*   **Exception**: 응용 프로그램 사용 하는 동안 throw 된 예외입니다.
*   **DiagnosticEvent**: 문제가 발생할 때 진단을 지원 하기 위해 이벤트 로그 (*되지* Microsoft로 전송) 합니다.
*   **FeedbackEvent**: 응용 프로그램을 통해 제출 된 사용자 피드백

이러한 단계 수집할 이벤트를 선택 하는 방법을 보여 줍니다. Microsoft로 이벤트가 전송 되는 여부 및:

1.  비활성화를 설치한 위치로 이동 (예: c:\\프로그램 파일 (x86)\\Microsoft Corporation\\데이터베이스 실험 도우미).
2.  두.config 파일을 엽니다. (응용 프로그램)에 대 한 DEA.exe.config 및 DEACmd.exe.config (CLI)에 대 한 합니다.
3.  이벤트의 유형 수집을 중지 하려면 값을 설정 *이벤트* (예를 들어 **TraceEvent**)를 **false**합니다. 이벤트를 다시 수집을 시작 하려면 값을 설정 **true**합니다.
4.  이벤트의 로컬 복사본을 저장을 중지 하려면 값을 설정 **TraceLoggerEnabled** 하 **false**합니다. 다시 로컬 복사본을 저장 하려면 값을 설정 **true**합니다.
5.  Microsoft로 이벤트를 보내지 않으려면 값을 설정 **AppInsightsLoggerEnabled** 하 **false**합니다. 다시 Microsoft로 이벤트를 전송 하려면 값을 설정 **true**합니다.

비활성화가 적용 된 [Microsoft 개인정보취급방침](https://aka.ms/dea-privacy).

## <a name="next-steps"></a>다음 단계

[시작](database-experimentation-assistant-get-started.md) 캡처를 재생 하 고 추적을 분석 하는 데 필요한 단계를 안내 합니다.
