---
title: "Power BI (SQL Server 데이터 Migration Assistant)를 사용 하 여 보고서에 통합된 하면 평가 | Microsoft Docs"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: sql-dma
ms.tgt_pltfrm: 
ms.topic: article
keywords: 
helpviewer_keywords: Data Migration Assistant, Assess
ms.assetid: 
caps.latest.revision: 
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 62f3ed0802a0a7570109bdae99151c8c6ce4fa01
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="report-on-your-consolidated-assessments-by-using-power-bi-data-migration-assistant"></a>Power BI (데이터 마이그레이션 길잡이)를 사용 하 여 보고서에 통합된 하면 평가

이 문서에서는 통합된 마이그레이션 평가 대 한 Power BI 보고서를 만드는 방법을 설명 합니다.

참조 데이터 Migration Assistant를 사용 하 여 마이그레이션 평가 통합에 대 한 내용은 [평가 보고서 통합](../dma/dma-consolidatereports.md)합니다.

## <a name="sample-power-bi-reports"></a>Power BI 보고서 샘플

통합된 마이그레이션 평가 대 한 Power BI 보고서의 예제를 다운로드할 수 [Github 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)합니다.

다음과 같은 보고서에 포함 되어 있습니다. 

- [대시보드](#dashboard--details)

  스냅숏 통계 및 드릴 다운 보고서에 포함 되어 있습니다.

- [온-프레미스 업그레이드 준비 상태](#on-premises-upgrade-readiness--details)

  데이터 원본은 DMAReporting 데이터베이스에서 UpgradeSuccessRanking 보기입니다.  이 보고서는 평가 데이터베이스에 대 한 백분율 업그레이드 성공 여부를 나타냅니다.

- [온-프레미스 기능 패리티](#on-premise-feature-parity--details)

  대상 SQL Server 버전에 권장 되는 기능을 보여 줍니다.

- [Azure SQL DB 업그레이드 준비 상태](#azure-sql-db-upgrade-readiness--details)

  데이터 원본은 DMAReporting 데이터베이스에서 UpgradeSuccessRanking 보기입니다.  이 보고서는 Azure SQL DB 마이그레이션에 대 한 평가 하는 데이터베이스에 대 한 백분율 업그레이드 성공 여부를 나타냅니다.

- [Azure SQL DB 지원 되지 않는 기능](#azure-sql-db-unsupported-features--details)

  Azure SQL DB (V12)에서 지원 되지 않는 기존 데이터베이스의 기능을 보여 줍니다.

Power BI에서 데이터 원본을 변경 하 여 사용자 환경에서 작동 하도록 이러한 보고서를 수정할 수 있습니다. 

1. 옆에 있는 아래쪽 화살표를 선택 **쿼리 편집**를 선택 하 고 **데이터 원본 설정**합니다.

   ![쿼리 메뉴에서 데이터 원본 설정 편집](../dma/media/DataSourceSettings.png)

1. 선택 **소스 변경 중...** , 서버 및 데이터베이스 값을 입력 합니다.

   ![소스, 서버 및 데이터베이스를 변경 합니다.](../dma/media/ChangeSource.png)

1. 선택 **확인**를 선택한 후 **닫기**합니다.

1. 보고서를 새로 고칩니다.

   ![Power BI 보고서를 새로 고칩니다.](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>대시보드 보고서

![대시보드 보고서](../dma/media/DashboardReport.png)

대시보드는 모든 사용자 평가 대 한 세부 정보를 보여줍니다. 인스턴스 또는 데이터베이스를 기준으로 왼쪽에 슬라이서를 사용할 수 있습니다. 가로 막대형 차트는 문제가 있는 곳을 보려면 특정 범주로 드릴 다운에 사용할 수 있습니다.

드릴 다운, 가로 막대형 차트의 오른쪽 위 모퉁이에 있는 아래쪽 화살표와 원이 선택 합니다.

![범주를 드릴 다운](../dma/media/CategoryDrillDown.png)

다음 그림에 표시 된 것과 같이 드릴 다운 시퀀스 설정 됩니다 (아래 **축**). 순서를 변경 하려면를 원하는 순서로 열을 끕니다.

![시각화를 가로 막대형 차트 축](../dma/media/VisualizationsAxis.png)

특정 데이터베이스에 의해 먼저 필터링 하 고 다음 특정 범주의 문제 가능해져서이 보기를 훨씬 더 강력해졌습니다. HR 데이터베이스 예를 들어 선택한 다음 예에서 **SQL01** 마이그레이션 (주요 변경 내용)를 방지 하는 모든 개체를 볼 수 있습니다.

![주요 HR 데이터베이스에 대 한 변경 내용](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>온-프레미스 준비 보고서 업그레이드

![온-프레미스 준비 보고서 업그레이드](../dma/media/OnPremisesUpgradeReadinessReport.png)

이 보고서에는 어떻게 준비 데이터베이스는 SQL Server의 이후 버전으로 마이그레이션에 대 한 스냅숏을 나타냅니다. 이 보고서의 데이터는 dbo에서 가져옵니다. UpgradeSuccessFactor\_DMAReporting 데이터베이스의 온-프레미스 보기.

인스턴스 및 데이터베이스 이름으로 필터링 하 여 맨 위에 있는 점수 카드를 사용 하 여을 확인할 수 있습니다 버전 데이터베이스는 너무 마이그레이션할 수 있습니다. 예를 들어 AdventureWorks 2012 데이터베이스에 의해 필터링 하는 경우 데이터베이스가 보고서에 나열 된 모든 SQL Server 버전으로 전환할 준비가 볼 수 있습니다. 이 해당 데이터베이스와의 호환성 수준에 대 한 주요 변경이 없습니다 함으로써 결정 됩니다.

![AdventureWorks 데이터베이스에 대 한 업그레이드 성공 비율](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>온-프레미스 기능 패리티 보고서

![온-프레미스 기능 패리티 보고서](../dma/media/OnPremisesFeatureParityReport.png)

이 보고서를 사용 하 여 대상 SQL Server 버전에서 데이터베이스에 대해 사용할 수 있는 새로운 기능을 강조 표시 합니다.

깔때기형 차트에는 기능을 선택 하면 아래쪽에 있는 데이터는 개체의 기능에 영향을 강조 표시 합니다. 다음 예제에서는 **저장 공간 절약 효과 대해 스트레치 데이터베이스** 기능을 선택 하 고 테이블 나열 된이 기능에서 혜택을 얻을 수 있는 합니다.

![스트레치 데이터베이스에 권장 되는 기능](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 업그레이드 준비 상태 보고서

![Azure SQL DB 업그레이드 준비 상태 보고서](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

이 보고서는 Azure SQL 데이터베이스 v 12로 마이그레이션하려면 데이터베이스 준비 상태를 표시 합니다. 이 보고서에서 데이터 dbo에서 가져옵니다. DMAReporting 데이터베이스 UpgradeSuccessRanking 보기입니다.

### <a name="azure-features-parity-report"></a>Azure 기능 패리티 보고서

![Azure 기능 패리티 보고서](../dma/media/AzureFeaturesParityReport.png)

이 보고서를 사용 하 여는 *인스턴스 수준 기능* Azure SQL 데이터베이스 v 12에서 지원 되지 않습니다.

깔때기형 차트에는 기능을 선택 하면 인스턴스 및 지원 되지 않는 데이터베이스 기능 데이터 맨 아래에 나열 됩니다. 다음 예제에서는이 기능을 선택: **Always on 가용성 그룹 구성 Azure SQL 데이터베이스에서 지원 되지 않습니다**합니다.  

![가용성 그룹 기능을 항상](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 지원 되지 않는 기능 보고서

![Azure SQL DB 지원 되지 않는 기능 보고서](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

이 보고서를 강조 표시 기능에 대 한 지원 되지 않습니다는 주어진 **데이터베이스** 대상 Azure SQL 데이터베이스 (V12)를가 하는 경우.

깔때기형 차트의 데이터베이스 이름 및 기능 값을 필터링 하 여 지원 되지 않는 기능에 세부 정보를 볼 수 있습니다. 세부 정보에는 개체가 영향을 받는 및 문제를 해결 하기 위한 권장 사항을 포함 합니다.

예를 들어 DTC 데이터베이스에서 필터링 및 **읽기 전용 데이터베이스를 업그레이드할 수 없는**, 영향을 받는 개체의 목록을 볼 수 있습니다.

![읽기 전용 데이터베이스 수 없는 업그레이드 문제](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>관련 항목:

[데이터 마이그레이션 길잡이 개요](../dma/dma-overview.md)

[데이터 마이그레이션 길잡이 다운로드](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 다운로드](https://powerbi.microsoft.com/)
