---
title: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미 시작
description: 데이터베이스 실험 도우미 시작
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
ms.openlocfilehash: 9fe162b2a9bc0db4a2a49648eecb76c5802f57c0
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381767"
---
# <a name="get-started-with-database-experimentation-assistant"></a>데이터베이스 실험 도우미 시작

DEA (데이터베이스 실험 도우미)는 업그레이드 또는 새 인덱스와 같은 SQL Server 환경의 변경에 대 한 A/B 테스트 솔루션입니다. DEA를 사용 하면 현재 환경에서 원본 서버의 워크 로드가 새 환경에서 어떻게 수행 될 것인지 평가할 수 있습니다. DEA 3 단계를 완료 하 여 A/B 테스트를 실행 하는 과정을 안내 합니다. 

- 캡처
- ★
- 분석

이 문서에서는 이러한 단계를 안내 합니다.

## <a name="capture"></a>캡처

SQL Server A/B 테스트의 첫 번째 단계는 원본 서버에서 추적을 캡처하는 것입니다. 원본 서버는 일반적으로 프로덕션 서버입니다. 추적 파일은 타임 스탬프를 포함 하 여 해당 서버에서 전체 쿼리 작업을 캡처합니다. 나중에이 추적이 분석을 위해 대상 서버에서 재생 됩니다. 분석 보고서는 두 대상 서버 간의 워크 로드 성능 차이에 대 한 정보를 제공 합니다.

고려 사항:

- 추적 캡처를 시작 하기 전에 추적을 캡처할 데이터베이스를 백업 해야 합니다.
- DEA 사용자는 Windows 인증을 사용 하 여 데이터베이스에 연결 하도록 구성 해야 합니다.
- SQL Server 서비스 계정에는 원본 추적 파일 경로에 대 한 액세스 권한이 있어야 합니다.
- DEA는 쿼리 성능이 향상 되는지 또는 저하 되는지 확인 하기 위해 캡처 기간 동안 쿼리를 15 번 이상 실행 해야 합니다.  

원본 서버에서 추적을 캡처하려면 다음을 수행 합니다.

1. DEA에서 왼쪽 메뉴의 카메라 아이콘을 선택 하 여 **모든 캡처** 로 이동 합니다.

   ![왼쪽 탐색 메뉴](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. 다음 정보를 입력 하거나 선택 합니다.

   - **추적 이름**: 만들려는 새 추적 파일의 파일 이름입니다. 롤오버 파일 명명 규칙을 사용 하는 추적 이름 (예: CaptureName \_NNN)을 사용 하지 마십시오.
   - **기간**: 캡처에 대 한 기간입니다.
   - **SQL Server 인스턴스 이름**: 추적을 캡처할 SQL Server 인스턴스입니다.
   - **데이터베이스 이름**: 추적을 캡처할 SQL Server를 실행 하는 컴퓨터의 데이터베이스 이름입니다. 이 인수를 비워 두면 서버의 모든 데이터베이스에서 추적이 캡처됩니다.
   - **SQL Server 컴퓨터에서 원본 추적 파일을 저장할 경로**: 추적 파일을 저장할 폴더 경로입니다.

1. 대상 데이터베이스가 백업 되었는지 확인 합니다. 그런 다음 데이터베이스 확인란을 선택 합니다.
1. **시작** 을 선택 하 여 캡처를 시작 합니다.

시작 시간, 기간 및 남은 시간을 포함 하 여 캡처의 진행 상황을 볼 수 있습니다. 이 캡처가 완료 될 때까지 기다리는 동안 새 캡처를 시작할 수도 있습니다. 캡처가 완료 되 면 출력 추적 파일을 사용 하 여 두 번째 단계를 시작 합니다. 대상 서버에서 추적 파일을 재생 합니다.

추적 캡처에 대 한 일반적인 질문은 [캡처 FAQ](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)를 참조 하세요.

## <a name="replay"></a>★

A/B 테스트 SQL Server의 두 번째 단계는 대상 서버에 캡처된 추적 파일을 재생 하는 것입니다. 그런 다음 분석을 위해 재생에서 광범위 한 추적을 수집 합니다. 

두 대상 서버에서 추적 파일을 재생 합니다. 하나는 원본 서버 (대상 1)를 모방 하 고 다른 하나는 제안 된 변경 내용 (대상 2)을 모방 합니다. 대상 1과 대상 2의 하드웨어 구성은 가능한 한 유사 하므로 제안 된 변경의 성능 효과를 정확 하 게 분석할 수 SQL Server.

고려 사항:

- 재생을 실행 하려면 컴퓨터에서 DReplay (Distributed Replay) 추적을 실행 하도록 설정 해야 합니다. 자세한 내용은 [Distributed Replay 컨트롤러 및 클라이언트 설치](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)를 참조 하세요.
- 원본 서버의 백업을 사용 하 여 대상 서버에서 데이터베이스를 복원 해야 합니다.
- SQL Server의 쿼리 캐싱은 평가 결과에 영향을 줄 수 있습니다. 평가 결과의 일관성을 향상 시키려면 서비스 응용 프로그램에서 SQL Server 서비스 (MSSQLSERVER)를 다시 시작 하는 것이 좋습니다.

추적 파일을 재생 하려면:

1. DEA에서 왼쪽 메뉴의 재생 아이콘을 선택 하 여 **모든 재생**으로 이동 합니다. 세션 중에 실행 되는 이전 재생 목록 (있는 경우)이 표시 됩니다. 새 재생을 시작 하려면 **새 재생**을 선택 합니다.

1. 다음 정보를 입력 하거나 선택 합니다.

   - **재생 이름**: 재생 추적의 파일 이름입니다.
   - **컨트롤러 컴퓨터 이름**: Distributed Replay 컨트롤러 컴퓨터의 이름입니다.
   - **컨트롤러의 원본 추적 파일 경로**: [캡처](#capture)원본 추적 파일의 파일 경로입니다.
   - **SQL Server instance name**: 원본 추적을 재생할 SQL Server 인스턴스의 이름입니다.
   - **SQL Server 컴퓨터에서 대상 추적 파일을 저장할 경로**: 결과 재생 추적 파일의 폴더 경로입니다.

1. 첫 번째 단계에서 백업을 복원 하려면이 확인란을 선택 합니다.

1. **시작** 을 선택 하 여 재생을 시작 합니다. 

재생 상태를 볼 수 있습니다. 두 대상 서버 모두에서 원본 추적을 재생 하면 분석 보고서를 생성할 준비가 된 것입니다.

재생에 대 한 일반적인 질문은 [재생 FAQ](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)를 참조 하세요.

## <a name="analysis"></a>분석

마지막 단계는 재생 추적을 사용 하 여 분석 보고서를 생성 하는 것입니다. 분석 보고서를 통해 제안 된 변경 내용의 성능 영향을 파악할 수 있습니다.

고려 사항:

- 하나 이상의 구성 요소가 없는 경우 새 분석 보고서 (인터넷 연결 필요)를 생성 하려고 하면 다운로드 링크가 있는 필수 구성 요소 페이지가 나타납니다.
- 이전 버전의 도구에서 생성 된 보고서를 보려면 먼저 스키마를 업데이트 해야 합니다.

분석 보고서를 생성 하려면:

1. 왼쪽 메뉴에서 **분석 보고서**로 이동 합니다. 보고서 데이터베이스를 저장 하는 SQL Server를 실행 하는 컴퓨터에 연결 합니다. 서버에 있는 모든 보고서의 목록이 표시 됩니다. 새 보고서를 만들려면 **새 보고서**를 선택 합니다.

1. 보고서를 생성 하는 데 필요한 정보를 입력 하거나 선택 합니다.

   - **보고서 이름**: 만들 분석 보고서의 이름입니다.
   - **대상 1 SQL Server 추적**: 대상 1에서 재생 하는 추적 파일의 경로입니다.
   - **대상 2 SQL Server 추적**: 대상 2에서 재생 하는 추적 파일의 경로입니다.

1. **시작** 을 선택 하 여 보고서를 생성 합니다. 새 보고서가 목록의 맨 위에 나타납니다. 보고서가 생성 되 면 보고서 옆의 아이콘이 녹색 확인 표시가 됩니다.

이제 A/B 테스트에서 제공 하는 정보를 얻기 위해 분석 보고서를 확인 합니다.

분석 보고서에 대 한 일반적인 질문은 [분석 FAQ](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)를 참조 하세요.

### <a name="analysis-report"></a>분석 보고서

보고서의 첫 페이지에는 실험을 실행 한 대상 서버에 대 한 버전 및 빌드 정보가 표시 됩니다. 임계값을 사용 하 여 A/B 테스트 분석의 민감도 또는 허용치를 조정할 수 있습니다. 기본적으로 임계값은 5%로 설정 됩니다. 5% 보다 크거나 같은 성능 향상은 **향상**된 것으로 분류 됩니다. 다른 성능 임계값을 사용 하 여 보고서를 평가 하려면 드롭다운 메뉴에서 옵션을 선택 합니다.

![임계값](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

두 원형 차트는 워크 로드에 대 한 두 대상 서버 간의 차이에 대 한 성능 영향을 보여 줍니다. 왼쪽 차트는 실행 횟수를 기반으로 합니다. 오른쪽 차트는 고유 쿼리를 기반으로 합니다. 5 개의 범주를 사용할 수 있습니다.

- **향상**된 기능: 통계적으로 대상 2에 대 한 쿼리를 대상 1에서 실행 하는 것이 좋습니다.
- **성능 저하**: 통계적으로 대상 1의 대상 2 보다는 쿼리가 더 이상 실행 되지 않습니다.
- **동일**: 대상 1과 대상 2 사이의 쿼리에 대해 통계적 차이가 없습니다.
- **평가할 수 없음**: 통계 분석을 위해 쿼리의 샘플 크기가 너무 작습니다. A/B 테스트 분석의 경우 DEA에는 각 대상에 대 한 실행이 30 개 이상 있어야 하는 동일한 쿼리가 필요 합니다.
- **오류**: 쿼리는 대상 중 하나에 한 번 이상 오류 발생.

![원형 차트](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

조각을 선택 하 여 특정 범주로 드릴 다운 하 고 원형 조각을 **평가할 수 없는** 성능 메트릭을 가져옵니다.

성능 변경 범주에 대 한 드릴 다운 페이지에는 해당 범주의 쿼리 목록이 표시 됩니다. **오류** 페이지에는 다음 세 개의 탭이 있습니다.

- **새 오류**: 대상 2에는 있지만 대상 1에는 표시 되지 않은 오류가 발생 했습니다.
- **기존 오류**: 대상 1과 대상 2 모두에 표시 되는 오류입니다.
- **해결 된 오류**: 대상 1에는 있지만 대상 2에는 없는 오류입니다.

   ![오류 페이지](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

해당 쿼리에 대 한 **비교 요약** 페이지로 이동할 쿼리를 선택 합니다.

**비교 요약** 페이지에는 해당 쿼리에 대 한 요약 통계가 표시 됩니다. 요약에는 실행 수, 평균 기간, 평균 CPU, 평균 읽기/쓰기 및 오류 수가 포함 됩니다.

![요약 통계](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

쿼리가 오류 쿼리 이면 오류 **정보** 탭에 오류에 대 한 자세한 정보가 표시 됩니다. **쿼리 계획 정보** 탭에는 대상 1과 대상 2의 쿼리에 사용 되는 쿼리 계획에 대 한 정보가 표시 됩니다.

![쿼리 계획](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

분석 보고서의 페이지에서 오른쪽 위에 있는 **인쇄** 단추를 선택 하 여 표시 되는 모든 항목을 인쇄 합니다.

## <a name="next-steps"></a>다음 단계

- 서버에서 발생 하는 이벤트 로그가 있는 추적 파일을 생성 하는 방법을 알아보려면 [추적 캡처](database-experimentation-assistant-capture-trace.md)를 참조 하세요.

- DEA 및 데모에 대 한 19 분의 소개는 다음 비디오를 시청 하세요.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
