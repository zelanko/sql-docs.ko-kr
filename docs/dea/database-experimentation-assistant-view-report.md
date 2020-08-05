---
title: SQL Server 업그레이드에 대 한 분석 보고서 보기
description: 데이터베이스 실험 도우미 (DEA)에서 성능 정보에 대 한 분석 보고서를 보고 이해 하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 02/04/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 5850f3f78590b5ceccea49033b401055180d715e
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565492"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>데이터베이스 실험 도우미 분석 보고서 보기

데이터베이스 실험 도우미 (DEA)를 사용 하 여 [분석 보고서를 만든](database-experimentation-assistant-create-report.md)후에는 수행한 A/B 테스트에 따라 성능 정보에 대 한 보고서를 검토할 수 있습니다.

## <a name="open-an-existing-analysis-report"></a>기존 분석 보고서 열기

1. DEA에서 목록 아이콘을 선택 하 고, 서버 이름 및 인증 유형을 지정 하 고, 시나리오에 적절 하 게 **연결 암호화** 및 **서버 인증서 신뢰** 확인란을 선택 하거나 선택 취소 한 다음 **연결**을 선택 합니다.

   ![보고서를 사용 하 여 서버에 연결](./media/database-experimentation-assistant-view-report/dea-connect-to-server-with-report-files.png)

2. **분석 보고서** 화면의 왼쪽에서 보려는 보고서에 대 한 항목을 선택 합니다.

   ![기존 보고서 파일 열기](./media/database-experimentation-assistant-view-report/dea-select-report-to-view.png)

## <a name="view-and-understand-the-analysis-report"></a>분석 보고서 보기 및 이해

이 섹션에서는 분석 보고서를 안내 합니다.

보고서의 첫 페이지에서 실험을 실행 한 대상 서버의 버전 및 빌드 정보에 대 한 정보가 표시 됩니다. 임계값을 사용 하면 A/B 테스트 분석의 민감도 또는 허용 오차를 조정할 수 있습니다. 기본적으로 임계값은 5%; (으)로 설정 됩니다. >= 5% 인 성능 향상은 ' 향상 '으로 분류 됩니다.  드롭다운을 사용 하 여 다른 성능 임계값으로 보고서를 평가할 수 있습니다.

**내보내기** 단추를 선택 하 여 보고서의 데이터를 CSV 파일로 내보낼 수 있습니다.  분석 보고서의 페이지에서 **인쇄** 를 선택 하 여 현재 화면에 표시 되는 항목을 인쇄할 수 있습니다.

### <a name="query-distribution"></a>쿼리 배포

- 원형 차트의 다른 조각을 선택 하 여 해당 범주에 속하는 쿼리만 표시 합니다.

   ![보고서 범주를 원형 조각으로](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

  - **성능 저하**: 목표 1 보다는 목표 2에서 더 나쁜 쿼리가 수행 됩니다.
  - **오류**: 하나 이상의 대상에 대 한 오류를 한 번 이상 보여 주는 쿼리입니다.
  - **향상**된 기능: 대상 1 보다는 대상 2에서 더 잘 수행 된 쿼리입니다.
  - **평가할 수 없음**: 통계 분석을 위해 샘플 크기가 너무 작은 쿼리 A/B 테스트 분석의 경우 DEA에는 각 대상에 대해 최소 15 개의 실행을 포함 하는 동일한 쿼리가 필요 합니다.
  - **동일**: 대상 1과 대상 2 간에 통계적 차이가 없는 쿼리

  오류 쿼리 (있는 경우)는 별도의 차트에 표시 됩니다. 유형별로 오류를 분류 하는 가로 막대형 차트 및 오류 ID 별로 오류를 분류 하는 원형 차트입니다.

   ![오류 쿼리 차트](./media/database-experimentation-assistant-view-report/dea-error-query-charts.png)

  다음과 같은 네 가지 유형의 오류를 사용할 수 있습니다.

  - **기존 오류**: 대상 1과 대상 2 모두에 존재 하는 오류입니다.
  - **새 오류**: 대상 2에서 새로운 오류가 발생 했습니다.
  - **해결 된 오류**: 대상 1에는 있지만 대상 2에서 확인 된 오류입니다.
  - **업그레이드 차단**: 대상 서버에 대 한 업그레이드를 차단 하는 오류입니다.

  차트에서 막대 또는 원형 섹션을 클릭 하면 범주가 드릴 다운 되 고 범주를 **평가할 수 없는** 경우에도 성능 메트릭이 표시 됩니다.

  또한 대시보드는 빠른 성능 개요를 제공 하기 위해 향상 된 상위 5 개 및 저하 된 쿼리를 보여 줍니다.

### <a name="individual-query-drill-down"></a>개별 쿼리 드릴 다운

특정 쿼리에 대 한 자세한 정보는 쿼리 템플릿 링크를 선택할 수 있습니다.

![특정 쿼리로 드릴 다운](./media/database-experimentation-assistant-view-report/dea-query-drill-down-report.png)

- 관련 비교 요약을 열려면 특정 쿼리를 선택 합니다.

   ![비교 요약](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

   실행 수, 평균 기간, 평균 CPU, 평균 읽기/쓰기 및 오류 수와 같은 해당 쿼리에 대 한 요약 통계를 찾을 수 있습니다.  쿼리가 오류 쿼리 이면 오류 **정보** 탭에 오류에 대 한 자세한 정보가 표시 됩니다.  **쿼리 계획 정보** 탭에서 대상 1 및 대상 2의 쿼리에 사용 되는 쿼리 계획에 대 한 정보를 찾을 수 있습니다.

   > [!NOTE]
   > 확장 이벤트를 분석 하는 경우 (. XEL) 파일, 쿼리 계획 정보는 사용자 컴퓨터의 메모리 압력을 제한 하기 위해 수집 되지 않습니다.

## <a name="see-also"></a>참고 항목

- 명령 프롬프트에서 분석 보고서를 생성 하는 방법에 대 한 자세한 내용은 [명령 프롬프트에서 실행](database-experimentation-assistant-run-command-prompt.md)을 참조 하세요.
