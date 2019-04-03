---
title: Data Migration Assistant 통합된 평가 보고서를 Power BI (SQL Server)를 사용 하 여 분석 | Microsoft Docs
description: 가져온 했으며 SQL Server에 통합 하는 데이터 마이그레이션 평가 보고서를 분석 하려면 Power BI를 사용 하는 방법 알아보기
ms.custom: ''
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
manager: craigg
ms.openlocfilehash: c00196468b846174bb73c8d82c691f482aa8b21e
ms.sourcegitcommit: 1a4aa8d2bdebeb3be911406fc19dfb6085d30b04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58872074"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Power BI를 사용 하 여 Data Migration Assistant에서 만든 통합된 평가 보고서 분석

이 문서는 Power BI 보고서 통합된 마이그레이션 평가 분석를 만드는 방법을 설명 합니다.

Data Migration Assistant에서 만든 마이그레이션 평가 통합 하는 방법에 대 한 내용은 [평가 보고서 통합](../dma/dma-consolidatereports.md)합니다.

## <a name="sample-power-bi-reports"></a>Power BI 보고서 샘플

이 통합된 마이그레이션 평가 대 한 Power BI 보고서의 예제를 다운로드할 수 있습니다 [Github 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)합니다.

다음과 같은 보고서에 포함 되어 있습니다. 

- [대시보드](#dashboard-report)

  스냅숏 통계 및 드릴 다운 보고서를 포함합니다.

- [온-프레미스 업그레이드 준비](#on-premises-upgrade-readiness-report)

  데이터 소스는 DMAReporting 데이터베이스에서 UpgradeSuccessRanking 뷰입니다.  이 보고서는 평가 된 데이터베이스에 대 한 백분율 업그레이드 성공 여부를 나타냅니다.

- [온-프레미스 기능 패리티](#on-premises-feature-parity-report)

  대상 SQL Server 버전에 권장 되는 기능을 보여 줍니다.

- [Azure SQL DB 업그레이드 준비](#azure-sql-db-upgrade-readiness-report)

  데이터 소스는 DMAReporting 데이터베이스에서 UpgradeSuccessRanking 뷰입니다.  이 보고서는 Azure SQL DB 마이그레이션을 평가 하는 데이터베이스에 대 한 백분율 업그레이드 성공 여부를 나타냅니다.

- [Azure SQL DB 지원 되지 않는 기능](#azure-sql-db-unsupported-features-report)

  Azure SQL DB (V12)에서 지원 되지 않는 기존 데이터베이스의 기능을 보여 줍니다.

Power BI에서 데이터 원본을 변경 하 여 사용자 환경에 맞게 이러한 보고서를 수정할 수 있습니다. 

1. 그런 다음 아래쪽 화살표를 선택 **쿼리 편집**, 선택한 **데이터 원본 설정**합니다.

   ![쿼리 메뉴에서 데이터 원본 설정 편집](../dma/media/DataSourceSettings.png)

1. 선택 **원본을 변경 하는 중...** , 서버 및 데이터베이스 값을 입력 합니다.

   ![원본, 서버 및 데이터베이스를 변경 합니다.](../dma/media/ChangeSource.png)

1. 선택 **확인**를 선택한 후 **닫기**합니다.

1. 보고서를 새로 고칩니다.

   ![Power BI 보고서를 새로 고칩니다.](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>대시보드 보고서

![대시보드 보고서](../dma/media/DashboardReport.png)

대시보드는 모든 평가 대 한 세부 정보를 보여줍니다. 인스턴스 또는 데이터베이스를 기준으로 왼쪽에 있는 슬라이서를 사용할 수 있습니다. 문제가 있는 곳을 확인 하려면 특정 범주로 드릴 다운 하려면 가로 막대형 차트를 사용할 수 있습니다.

드릴 다운 하려면 가로 막대형 차트의 오른쪽 위 모서리에 있는 아래쪽 화살표를 사용 하 여 원을 선택 합니다.

![범주를 드릴 다운](../dma/media/CategoryDrillDown.png)

드릴 다운 시퀀스는 다음 이미지와 같이 설정 됩니다 (아래 **축**). 시퀀스를 변경 하려면를 원하는 순서로 열을 끕니다.

![시각화를 가로 막대형 차트 축](../dma/media/VisualizationsAxis.png)

먼저 특정 데이터베이스에서 필터링 하 고 다음 특정 범주의 문제도 드릴 다운 하는 경우이 보기를 훨씬 더 강력해졌습니다 됩니다. HR 데이터베이스 예를 들어 선택한 다음 예에서 **SQL01** 마이그레이션 (주요 변경 내용)를 방지 하는 모든 개체를 보고 합니다.

![HR 데이터베이스에 대 한 주요 변경 내용](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>온-프레미스 준비 보고서 업그레이드

![온-프레미스 준비 보고서 업그레이드](../dma/media/OnPremisesUpgradeReadinessReport.png)

이 보고서는 데이터베이스 SQL Server의 이후 버전으로 마이그레이션하기 위해 준비 하는 방법의 스냅숏으로 표시 합니다. 이 보고서의 데이터는 dbo에서 제공 됩니다. UpgradeSuccessFactor\_DMAReporting 데이터베이스에서 온-프레미스 뷰.

인스턴스 및 데이터베이스 이름으로 필터링 하 여 맨 위에 있는 점수 카드를 사용 하 고 표시 하는 버전 데이터베이스는 너무 마이그레이션할 수 있습니다. 예를 들어, AdventureWorks 2012 데이터베이스를 필터링 할 경우 데이터베이스는 보고서에 나열 된 모든 SQL Server 버전으로 이동할 준비가 되었는지 볼 수 있습니다. 해당 데이터베이스 및 호환성 수준에 대 한 주요 변경이 없습니다 함으로써 결정 됩니다.

![AdventureWorks 데이터베이스에 대 한 업그레이드 성공 비율](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>온-프레미스 기능 패리티 보고서

![온-프레미스 기능 패리티 보고서](../dma/media/OnPremisesFeatureParityReport.png)

이 보고서를 사용 하 여 대상 SQL Server 버전에서 데이터베이스에 대해 사용할 수 있는 새로운 기능을 강조 표시 합니다.

깔때기형 차트의 기능을 선택 하면 아래쪽에 있는 데이터의 기능으로는 개체에 영향을 강조 표시 합니다. 다음 예제에서는 **저장소 절약을 위한 스트레치 데이터베이스** 기능을 선택 하 고 테이블에 나열 됩니다이 기능을 통해 이점을 얻을 수 있습니다.

![Stretch Database 대 한 기능 권장 사항](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 업그레이드 준비 상태 보고서

![Azure SQL DB 업그레이드 준비 상태 보고서](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

이 보고서는 Azure SQL Database V12로 마이그레이션하려면 데이터베이스 준비 상태를 표시 합니다. 이 보고서에서 데이터 dbo에서 가져옵니다. DMAReporting 데이터베이스 UpgradeSuccessRanking 보기입니다.

### <a name="azure-features-parity-report"></a>Azure 기능 패리티 보고서

![Azure 기능 패리티 보고서](../dma/media/AzureFeaturesParityReport.png)

이 보고서를 사용 하 여 강조 표시 하는 *인스턴스 수준 기능* Azure SQL Database V12에서 지원 되지 않습니다.

깔때기형 차트의 기능을 선택 하면 아래쪽에 있는 데이터의 인스턴스 및 지원 되지 않는 데이터베이스 기능을 나열 합니다. 다음 예제에서는이 기능을 선택 합니다. **Always on 가용성 그룹 그룹 구성은 지원 되지 않습니다 Azure SQL Database에서**합니다.  

![가용성 그룹 기능을 항상](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 지원 되지 않는 기능 보고서

![Azure SQL DB 지원 되지 않는 기능 보고서](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

이 보고서를 강조 표시 기능에 대 한 지원 되지 않습니다는 주어진 **데이터베이스** 대상 Azure SQL Database (V12) 경우입니다.

깔때기형 차트 데이터베이스 이름과 값으로 필터링 하 여 지원 되지 않는 기능 세부 정보를 볼 수 있습니다. 개체가 영향을 받고 문제를 해결 하기 위한 권장 사항 세부 정보에 포함 됩니다.

예를 들어, DTC database에서 필터링 하 고 **읽기 전용 데이터베이스를 업그레이드할 수 없습니다**, 영향을 받는 개체의 목록을 볼 수 있습니다.

![읽기 전용 데이터베이스 수 없는 업그레이드 문제](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>참고자료

[Data Migration Assistant 개요](../dma/dma-overview.md)

[Data Migration Assistant 다운로드](https://www.microsoft.com/download/details.aspx?id=53595)

[Power BI 다운로드](https://powerbi.microsoft.com/)
