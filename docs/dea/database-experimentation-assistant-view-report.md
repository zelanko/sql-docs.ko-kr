---
title: SQL Server 업그레이드에 대 한 분석 보고서 보기
description: 데이터베이스 실험 도우미 분석 보고서 보기
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: b72d49e691311104481637ff49d6c1e09ae0c230
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317738"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미 분석 보고서 보기

데이터베이스 실험 도우미 (DEA)를 사용 하 여 [분석 보고서를 만든](database-experimentation-assistant-create-report.md)후에는 아래 단계를 사용 하 여 A/B 테스트를 기반으로 하는 성능 정보에 대 한 보고서를 검토 합니다.

## <a name="select-a-server"></a>서버를 선택합니다.

DEA에서 메뉴 아이콘을 선택 합니다. 확장 된 메뉴에서 검사 목록 아이콘 옆에 있는 **분석 보고서** 를 선택 하 여 분석 보고서 창을 엽니다.

**분석 보고서**에서 분석 데이터베이스가 있는 SQL Server를 실행 하는 컴퓨터의 이름을 입력 한 다음 **연결**을 선택 합니다.

![기존 보고서에 연결](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

종속성이 누락 된 경우 **필수 구성 요소** 페이지에 설치를 위한 링크를 묻는 메시지가 표시 됩니다. 필요한 경우 필수 구성 요소를 설치한 후 **다시 시도**를 선택 합니다.

![필수 구성 요소 페이지](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>확인할 분석 보고서 선택

분석 보고서 목록에서 보고서를 두 번 클릭 하 여 엽니다.

![기존 보고서 보기](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

이 예제 차트에 표시 된 것 처럼 워크 로드의 표현에 대 한 정보를 얻을 수 있습니다.

![작업 담당자 차트](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>분석 보고서 보기 및 이해

이 섹션에서는 분석 보고서를 안내 합니다.

### <a name="query-categories"></a>쿼리 범주

왼쪽 원형 차트의 다른 조각을 선택 하 여 해당 범주에 속하는 쿼리만 표시 합니다.

![보고서 원형 조각](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **성능 저하 된 쿼리**: B에서 보다 더 효율적으로 수행 되는 쿼리입니다.  
- **오류**: 인스턴스 B의 오류는 표시 하지만 인스턴스 A에는 표시 되지 않는 쿼리입니다.  
- **향상 된 쿼리**: 인스턴스 B에서 보다 효율적으로 실행 되는 쿼리.  
- **확정**되지 않은 쿼리: 성능이 결정 되지 않은 쿼리가 변경 되었습니다.  
- **동일**: A와 B 인스턴스 간에 성능이 동일 하 게 높게 유지는 쿼리입니다.

### <a name="individual-query-drill-down"></a>개별 쿼리 드릴 다운

쿼리 템플릿 링크를 선택 하 여 특정 쿼리에 대 한 자세한 정보를 볼 수 있습니다.

![쿼리 드릴 다운](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

특정 쿼리를 선택 하 여 쿼리에 대 한 비교 요약을 엽니다.

![비교 요약](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

쿼리가 실행 된 A 및 B 인스턴스를 볼 수 있습니다. 또한 쿼리 형태에 대 한 템플릿도 볼 수 있습니다. 테이블은 A 및 B 인스턴스와 관련 된 쿼리 정보를 표시 합니다.

### <a name="error-queries"></a>오류 쿼리

비교 요약 보고서에는 확장 가능한 **오류 정보** 및 **쿼리 계획 정보** 섹션이 있습니다. 이 섹션에서는 두 인스턴스에 대 한 오류 및 계획 정보를 보여 줍니다.

오류 (빨간색) 원형을 선택 하 여 이러한 유형의 오류를 표시 합니다.

- **기존 오류**:에 있던 오류입니다.
- **새 오류**: B에서 발생 한 오류입니다.
- **해결 된 오류**: a에 있지만 B에는 없는 오류입니다.

![오류 차트](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="see-also"></a>참고 항목

- 명령 프롬프트에서 분석 보고서를 생성 하는 방법에 대 한 자세한 내용은 [명령 프롬프트에서 실행](database-experimentation-assistant-run-command-prompt.md)을 참조 하세요.
