---
title: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미를 사용 하 여 시작
description: 데이터베이스 실험 도우미를 사용 하 여 시작
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
manager: jroth
ms.openlocfilehash: 8f5cf6696b66504357279ab45432b4439894e4ca
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794464"
---
# <a name="get-started-with-database-experimentation-assistant"></a>데이터베이스 실험 도우미를 사용 하 여 시작

데이터베이스 실험 도우미 (비활성화)는 A / B 테스트 업그레이드 또는 새 인덱스와 같은 SQL Server 환경의 변경 내용에 대 한 솔루션입니다. 비활성화 (현재 환경)에서 원본 서버에서 워크 로드는 새 환경에서 어떻게 수행 되는지 평가 하는 데 도움이 됩니다. 비활성화 안내 실행 A / B 테스트의 세 단계를 완료 하 여: 

- 캡처
- 재생
- 분석

이 문서는 다음이 단계를 안내합니다.

## <a name="capture"></a>캡처

SQL Server의 첫 번째 단계는 원본 서버에서 추적을 캡처하는 B 테스트 합니다. 원본 서버에는 일반적으로 프로덕션 서버의 경우 추적 파일 타임 스탬프를 포함 하 여 해당 서버에 대 한 전체 쿼리 작업을 캡처합니다. 나중에이 추적 분석을 위해 대상 서버에서 재생 됩니다. 분석 보고서는 두 개의 대상 서버 간의 워크 로드의 성능 차이에 정보를 제공합니다.

고려 사항:

- 추적 캡처를 시작 하기 전에 추적을 캡처 중인지는 데이터베이스를 백업 해야 합니다.
- 비활성화 사용자는 Windows 인증을 사용 하 여 데이터베이스에 연결 하도록 구성 되어야 합니다.
- SQL Server 서비스 계정에는 원본 추적 파일 경로가 액세스를 해야합니다.

원본 서버에서 추적을 캡처하려면:

1. 비활성화로 이동 **모든 캡처** 왼쪽된 메뉴에서 카메라 아이콘을 선택 합니다.

   ![왼쪽된 탐색 메뉴](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. 입력 하거나 다음 정보를 선택 합니다.

   - **추적 이름**: 만들 새 추적 파일의 파일 이름입니다. 롤오버 파일 명명 규칙, 예를 들어 CaptureName를 사용 하는 추적 이름을 방지\_NNN 합니다.
   - **기간**: 캡처에 대 한 기간입니다.
   - **SQL Server 인스턴스 이름을**: 추적을 캡처할 하려는 SQL Server 인스턴스.
   - **데이터베이스 이름**: SQL Server를 실행 하는 컴퓨터에서 데이터베이스의 이름을의 추적을 캡처할 두는 것이 좋습니다. 빈 상태로 둔 경우 추적은 서버의 모든 데이터베이스에서 캡처됩니다.
   - **SQL Server 컴퓨터에서 원본 추적 파일을 저장할 경로를**: 추적 파일을 저장 하려는 폴더 경로입니다.

1. 대상 데이터베이스를 백업 하 고 있는지 확인 합니다. 그런 다음 데이터베이스 확인란을 선택 합니다.
1. 선택 **시작** 캡처를 시작 합니다.

시작 시간, 기간 및 남은 시간을 포함 하 여 캡처를의 진행률을 볼 수 있습니다. 또한이 캡처 완료를 기다리는 동안 새 캡처를 시작할 수 있습니다. 캡처 완료 되 면 추적 출력 파일을 사용 하 여 두 번째 단계를 시작 합니다: 대상 서버에서 추적 파일을 재생 합니다.

추적 캡처에 대 한 일반적인 질문에 대 한 참조를 [FAQ 캡처](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)합니다.

## <a name="replay"></a>재생

SQL Server의 두 번째 단계는 대상 서버에 캡처된 추적 파일을 재생 하는 B 테스트 합니다. 그런 다음 분석을 위해 재생에서 광범위 한 추적을 수집 합니다. 

두 명의 대상 서버에서 추적 파일 재생: 원본 서버 (Target 1)을 모방 하는 것을 제안 된 변경 (대상 2)를 모방 하는 것입니다. SQL Server 제안 된 변경 내용을의 성능 영향을 정확 하 게 분석할 수 있도록 대상 1-2 대상의 하드웨어 구성 가능한 한 유사 해야 합니다.

고려 사항:

- 재생을 실행 하려면 컴퓨터 실행 (DReplay) Distributed Replay 추적을 설정 해야 합니다. 자세한 내용은 [Distributed Replay controller 및 client 설치](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)합니다.
- 원본 서버에서 백업을 사용 하 여 대상 서버에서 데이터베이스를 복원 해야 합니다.
- SQL Server에 캐시 된 쿼리 평가 결과 영향을 줄 수 있습니다. 권장 SQL Server 서비스 (MSSQLSERVER)를 다시 시작 하는 평가 결과의 일관성을 개선 하기 위해 서비스 응용 프로그램에서입니다.

추적 파일을 재생 합니다.

1. 비활성화를에서 이동 하려면 왼쪽된 메뉴에서 재생 아이콘을 선택 **모든 재생**합니다. 목록 표시 있는 세션 중 실행 되는 지난 재생입니다. 새 재생을 시작 하려면 선택 **새 재생**합니다.

1. 입력 하거나 다음 정보를 선택 합니다.

   - **재생 이름**: 재생 추적 파일 이름입니다.
   - **컨트롤러 컴퓨터 이름**: Distributed Replay 컨트롤러 컴퓨터의 이름입니다.
   - **컨트롤러에서 원본 추적 파일에 대 한 경로**: 원본 추적 파일의 파일 경로 [캡처](#capture)합니다.
   - **SQL Server 인스턴스 이름을**: 원본 추적을 재생 하는 SQL Server 인스턴스의 이름입니다.
   - **SQL Server 컴퓨터에서 대상 추적 파일을 저장할 경로**: 재생 추적 파일에 대 한 폴더 경로입니다.

1. 첫 번째 단계에서 백업을 복원 하려면이 확인란을 선택 합니다.

1. 선택 **시작** 재생 합니다. 

프로그램 재생의 상태를 볼 수 있습니다. 대상 서버 모두에서 원본 추적을 재생 하는 분석 보고서를 생성할 준비가 된 것입니다.

재생에 대 한 일반적인 질문에 대 한 참조를 [FAQ 재생](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)합니다.

## <a name="analysis"></a>분석

마지막 단계는 추적 재생을 사용 하 여 분석 보고서를 생성 하는 것입니다. 분석 보고서를 제안된 된 변경의 성능에 미치는 영향에 대 한 통찰력을 얻을 수 있습니다.

고려 사항:

- 하나 이상의 구성 요소가 없는 경우 다운로드에 대 한 링크를 사용 하 여 필수 구성 요소 페이지 (인터넷 연결 필요) 새 분석 보고서를 생성 하려고 할 때 나타납니다.
- 이전 버전의 도구에서 생성 된 보고서를 보려면 먼저 스키마를 업데이트 해야 합니다.

분석 보고서를 생성 합니다.

1. 왼쪽된 메뉴에서로 이동 **분석 보고서**합니다. 보고서 데이터베이스를 저장 하는 SQL Server를 실행 하는 컴퓨터에 연결 합니다. 서버에서 모든 보고서의 목록이 표시 됩니다. 새 보고서를 만들려면 **새 보고서**합니다.

1. 입력 하거나 보고서를 생성 하는 데 필요한 정보를 선택 합니다.

   - **보고서 이름을**: 만들려는 분석 보고서의 이름입니다.
   - **1 대상 SQL Server에 대 한 추적**: 추적 파일 재생 대상 1에서의 경로입니다.
   - **2 대상 SQL Server에 대 한 추적**: 추적 파일 재생 대상 2에서의 경로입니다.

1. 선택 **시작** 보고서를 생성 합니다. 목록의 맨 위에 있는 새 보고서에 표시 됩니다. 보고서 옆의 아이콘은 보고서가 생성 되 면 녹색 확인 표시가 됩니다.

이제 통찰력을 제공 하는 분석 보고서를 보기 / B 테스트 합니다.

분석 보고서에 대 한 일반적인 질문에 대 한 참조를 [분석 FAQ](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)합니다.

### <a name="analysis-report"></a>분석 보고서

보고서의 첫 번째 페이지에서 실험 실행 된 대상 서버에 대 한 버전 및 빌드 정보가 표시 됩니다. 에 허용 오차를 민감도 맞게 임계값을 사용할 수 / B 테스트 분석 합니다. 기본적으로 임계값을 5%로 설정 됩니다. 5% 보다 더 성능이 향상 된 기능으로 분류 됩니다 **향상 된**합니다. 다양 한 성능 임계값을 사용 하 여 보고서를 평가 하려면 드롭다운 메뉴에서 옵션을 선택 합니다.

![임계값](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

원형 차트를 2 개 성능에 미치는 워크 로드에 대 한 두 개의 대상 서버 간의 차이 보여 줍니다. 왼쪽된 차트에는 실행 횟수를 기반으로 합니다. 오른쪽 차트에는 고유한 쿼리를 기반으로 합니다. 5 가지 가능한 범주가 있습니다.

- **향상 된**:  쿼리 실행 대상 1 보다 대상 2에 더 합니다.
- **성능 저하**: 쿼리 실행 대상 1 보다 대상 2에 더 합니다.
- **동일한**: 차이가 없는 통계 쿼리에 대 한 대상 1-2 대상입니다.
- **계산할 수 없습니다.** : 통계 분석 쿼리에 대 한 샘플 크기를 너무 작습니다. A / B 테스트 분석, 비활성화 사용 하려면 각 대상에서 30 개 이상의 실행 하도록 동일한 쿼리 합니다.
- **오류**: 대상 중 하나에서 한 번 이상 오류 발생 하는 쿼리.

![원형 차트](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

특정 범주를 드릴 다운을 포함 하 여 성능 메트릭을 가져올 분할 영역을 선택 합니다 **계산할 수 없습니다.** 원형 조각입니다.

성능에 대 한 드릴 다운 페이지를 해당 범주에는 쿼리 목록이 범주 표시를 변경 합니다. 합니다 **오류** 페이지에 세 개의 탭이 있습니다.

- **새 오류**: 대상 1에는 없지만 대상 2에서 표시 되는 오류입니다.
- **기존 오류**: 대상 1과 대상 2에 표시 되는 오류입니다.
- **오류 해결**: 대상 2에는 없지만 대상 1에서 표시 되는 오류입니다.

   ![오류 페이지](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

로 쿼리를 선택 하는 **Comparison Summary** 해당 쿼리에 대 한 페이지입니다.

합니다 **비교 요약** 페이지 해당 쿼리에 대 한 요약 통계를 보여 줍니다. 요약 실행 "," 평균 기간 "," 평균 CPU "," 평균 읽기/쓰기 "및" 오류 수가 포함 됩니다.

![요약 통계](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

쿼리 오류 쿼리를 사용 하는 경우는 **오류 정보** 탭 오류에 대 한 자세한 정보를 표시 합니다. 합니다 **쿼리 계획 정보** 탭 대상 1-2 대상에 대 한 쿼리에 사용 되는 쿼리 계획에 대 한 정보를 표시 합니다.

![쿼리 계획](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

분석 보고서의 페이지를 선택 합니다 **인쇄** 위쪽 단추 표시 되는 모든 항목을 인쇄할 수 있는 권한입니다.

## <a name="next-steps"></a>다음 단계

- 서버에서 발생 하는 이벤트 로그에 있는 추적 파일을 생성 하는 방법에 알아보려면 참조 [추적을 캡처](database-experimentation-assistant-capture-trace.md)합니다.

- 비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
