---
title: SQL Server 업그레이드에 대 한 데이터베이스 실험 도우미에서 분석 보고서 보기
description: 데이터베이스 실험 도우미에서 분석 보고서 보기
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
ms.openlocfilehash: 066297daff3393304b83b77238277f873e1c97fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050452"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미에서 분석 보고서 보기

한 후 [분석 보고서를 만들](database-experimentation-assistant-create-report.md) 에서 데이터베이스 실험 도우미 (비활성화), A에서 제공 하는 성능 통찰력을 얻고 보고서를 보려면이 문서에 설명 된 단계를 완료 / B 테스트 합니다.

## <a name="select-a-server"></a>서버 선택

비활성화를에서 메뉴 아이콘을 선택 합니다. 확장 된 메뉴에서 선택 **분석 보고서** 분석 보고서 창을 검사 목록 아이콘 옆에 있습니다.

아래 **분석 보고서**를 분석 데이터베이스를 포함 하는 SQL Server를 실행 하는 컴퓨터의 이름을 입력 합니다. **연결**을 선택합니다. 

![기존 보고서에 연결](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

모든 종속성을 누락 하는 경우는 **필수 구성 요소** 페이지 링크 설치할지를 묻는 메시지를 표시 합니다. 설치 필수 구성 요소를 선택한 후 **다시**입니다.

![필수 구성 요소 페이지](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>분석 보고서를 보려면를 선택 합니다.

분석 보고서의 목록에서 열려는 보고서를 두 번 클릭 합니다.

![기존 보고서를 보려면](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

이 예제에서는 차트에 표시 된 대로 워크 로드를 나타내는 정도에 대 한 통찰력을 얻을 수 있습니다.

![워크 로드 Rep 차트](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>보기 및 분석 보고서 이해

이 섹션에서는 분석 보고서를 통해 안내합니다.

### <a name="query-categories"></a>쿼리 범주

해당 범주에 속하는 쿼리만 표시 하려면 왼쪽된 원형 차트의 여러 분할 영역을 선택 합니다.

![보고서 원형 조각](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **쿼리 성능 저하**: B의 a 보다 더 잘 수행 하는 쿼리  
- **오류**: 1. 인스턴스가 아니라 인스턴스 B에에서 오류를 표시 하는 쿼리  
- **쿼리를 향상**: 1. 인스턴스의 인스턴스 B 보다 더 나은 실행 된 쿼리  
- **결정 되지 않은 쿼리**: 쿼리는 결정 되지 않은 성능 변경 합니다.  
- **동일한**: 쿼리는 성능 높아짐을 인스턴스 A와 B 간에

### <a name="individual-query-drill-down"></a>개별 쿼리 드릴 다운

특정 쿼리에 대 한 자세한 정보를 보려면 쿼리 템플릿 링크를 선택할 수 있습니다.

![쿼리 드릴 다운](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

특정 쿼리에 대 한 요약 비교를 열려면 쿼리를 선택 합니다.

![비교 요약](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

쿼리를 실행 하는 인스턴스 A와 B를 볼 수 있습니다. 또한 쿼리 모양을 템플릿을 볼 수 있습니다. 테이블을 인스턴스 A와 B에 관련 된 쿼리 정보를 표시 합니다.

### <a name="error-queries"></a>오류 쿼리

비교 요약 보고서에 확장 가능한 **오류 정보** 하 고 **쿼리 계획 정보** 섹션입니다. 오류를 표시 하 고 두 인스턴스 모두에 대 한 정보를 계획 하는 섹션입니다.

이러한 종류의 오류를 표시 하려면 오류 (빨간색) 원형 차트를 선택 합니다.
- **기존 오류**: 1.에 있던 오류
- **새 오류**: 2.에 있던 오류
- **오류 해결**: 2. 제외한 A에는 오류

![오류 차트](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>다음 단계

- 명령 프롬프트에서 분석 보고서를 생성 하는 방법에 알아보려면 참조 [명령 프롬프트에서 실행](database-experimentation-assistant-run-command-prompt.md)합니다.

- 비활성화 및 데모를 19 분 소개의 경우 다음 동영상을 시청 합니다.

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
