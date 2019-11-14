---
title: Power BI를 사용 하 여 통합 평가 보고서 분석
titleSuffix: Data Migration Assistant
description: Power BI를 사용 하 여에서 가져와서 통합 한 데이터 마이그레이션 평가 보고서를 분석 하는 방법에 대해 알아봅니다 SQL Server
ms.custom: seo-lt-2019
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
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056502"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Power BI를 사용 하 여 Data Migration Assistant 만든 통합 평가 보고서 분석

이 문서에서는 통합 마이그레이션 평가를 분석 하는 Power BI 보고서를 만드는 방법을 설명 합니다.

Data Migration Assistant에서 만든 마이그레이션 평가를 통합 하는 방법에 대 한 자세한 내용은 [평가 보고서 통합](../dma/dma-consolidatereports.md)을 참조 하세요.

## <a name="sample-power-bi-reports"></a>샘플 Power BI 보고서

이 [GitHub 리포지토리에서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant)통합 마이그레이션 평가를 위해 Power BI 보고서의 예를 다운로드할 수 있습니다.

포함 되는 보고서는 다음과 같습니다. 

- [대시보드와](#dashboard-report)

  스냅숏 통계와 드릴 다운 보고서를 포함 합니다.

- [온-프레미스 업그레이드 준비](#on-premises-upgrade-readiness-report)

  데이터 원본은 DMAReporting 데이터베이스의 UpgradeSuccessRanking 뷰입니다.  이 보고서는 평가 된 데이터베이스에 대 한 업그레이드 성공 비율을 표시 합니다.

- [온-프레미스 기능 패리티](#on-premises-feature-parity-report)

  대상 SQL Server 버전에 대 한 기능 권장 사항을 표시 합니다.

- [Azure SQL DB 업그레이드 준비](#azure-sql-db-upgrade-readiness-report)

  데이터 원본은 DMAReporting 데이터베이스의 UpgradeSuccessRanking 뷰입니다.  이 보고서는 Azure SQL DB 마이그레이션에 대해 평가 된 데이터베이스의 업그레이드 성공 비율을 보여 줍니다.

- [Azure SQL DB 지원 되지 않는 기능](#azure-sql-db-unsupported-features-report)

  V12 (Azure SQL DB)에서 지원 되지 않는 기존 데이터베이스의 기능을 보여 줍니다.

Power BI에서 데이터 원본을 변경 하 여 사용자 환경에서 작동 하도록 이러한 보고서를 수정할 수 있습니다. 

1. **쿼리 편집**옆에 있는 아래쪽 화살표를 선택 하 고 **데이터 원본 설정**을 선택 합니다.

   ![쿼리 편집 메뉴, 데이터 원본 설정](../dma/media/DataSourceSettings.png)

1. **원본 변경 ...** 을 선택 하 고 서버 및 데이터베이스 값을 입력 합니다.

   ![원본, 서버 및 데이터베이스 변경](../dma/media/ChangeSource.png)

1. **확인**을 선택 하 고 **닫기**를 선택 합니다.

1. 보고서를 새로 고칩니다.

   ![Power BI 보고서 새로 고침](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>대시보드 보고서

![대시보드 보고서](../dma/media/DashboardReport.png)

대시보드는 모든 평가에 대 한 세부 정보를 표시 합니다. 왼쪽의 슬라이서를 사용 하 여 인스턴스 또는 데이터베이스를 기준으로 필터링 할 수 있습니다. 가로 막대형 차트를 사용 하 여 특정 범주를 드릴 다운 하 여 문제가 발생 한 위치를 확인할 수 있습니다.

드릴 다운 하려면 가로 막대형 차트의 오른쪽 위 모퉁이에 있는 아래쪽 화살표를 사용 하 여 원을 선택 합니다.

![범주 드릴 다운](../dma/media/CategoryDrillDown.png)

드릴 다운 시퀀스는 다음 이미지 ( **축**아래)와 같이 설정 됩니다. 시퀀스를 변경 하려면 열을 원하는 순서로 끌어 옵니다.

![시각화, 가로 막대형 차트 축](../dma/media/VisualizationsAxis.png)

이 보기는 먼저 특정 데이터베이스를 기준으로 필터링 한 다음 특정 범주 문제를 드릴 다운할 때 훨씬 더 강력 하 게 됩니다. 다음 예에서는 마이그레이션 (주요 변경 사항)을 방지 하는 모든 개체를 **로** 인스턴스를 위해 HR 데이터베이스를 선택 합니다.

![HR 데이터베이스의 주요 변경 내용](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>온-프레미스 업그레이드 준비 보고서

![온-프레미스 업그레이드 준비 보고서](../dma/media/OnPremisesUpgradeReadinessReport.png)

이 보고서에는 데이터베이스를 최신 버전의 SQL Server로 마이그레이션하는 방법에 대 한 스냅숏이 표시 됩니다. 이 보고서의 데이터는 dbo에서 가져옵니다. DMAReporting 데이터베이스의 UpgradeSuccessFactor\_온-프레미스 view.

인스턴스 및 데이터베이스 이름을 기준으로 필터링 하 고 위쪽의 점수 카드를 사용 하 여 데이터베이스를 마이그레이션할 수 있는 버전을 확인할 수 있습니다. 예를 들어 AdventureWorks 2012 데이터베이스를 기준으로 필터링 하는 경우 데이터베이스를 보고서에 나열 된 모든 SQL Server 버전으로 이동할 준비가 된 것을 볼 수 있습니다. 이는 해당 데이터베이스 및 호환성 수준에 대 한 주요 변경 내용이 없는지 확인 하 여 결정 됩니다.

![AdventureWorks 데이터베이스에 대 한 업그레이드 성공 비율](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>온-프레미스 기능 패리티 보고서

![온-프레미스 기능 패리티 보고서](../dma/media/OnPremisesFeatureParityReport.png)

이 보고서를 사용 하 여 대상 SQL Server 버전의 데이터베이스에 사용할 수 있는 새로운 기능을 강조 표시할 수 있습니다.

깔때기형 차트에서 기능을 선택 하는 경우 아래쪽의 데이터는 기능의 영향을 받는 개체를 강조 표시 합니다. 다음 예제에서는 **저장소 절약을 위한 스트레치 데이터베이스** 기능을 선택 하 고이 기능을 사용할 수 있는 테이블이 나열 됩니다.

![Stretch Database에 대 한 기능 권장 사항](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Azure SQL DB 업그레이드 준비 보고서

![Azure SQL DB 업그레이드 준비 보고서](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

이 보고서는 Azure SQL Database V12로 마이그레이션할 데이터베이스 준비 상태를 표시 합니다. 이 보고서의 데이터는 dbo에서 가져옵니다. DMAReporting 데이터베이스의 UpgradeSuccessRanking 뷰입니다.

### <a name="azure-features-parity-report"></a>Azure 기능 패리티 보고서

![Azure 기능 패리티 보고서](../dma/media/AzureFeaturesParityReport.png)

이 보고서를 사용 하 여 Azure SQL Database V12에서 지원 하지 않는 *인스턴스 수준 기능* 을 강조 표시 합니다.

깔때기형 차트에서 기능을 선택 하면 아래쪽의 데이터에 지원 되지 않는 인스턴스 및 데이터베이스 기능이 나열 됩니다. 다음 예제에서는이 기능을 선택 합니다. **Always On 가용성 그룹 구성은 Azure SQL Database에서 지원 되지 않습니다**.  

![Always on 가용성 그룹 기능](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Azure SQL DB 지원 되지 않는 기능 보고서

![Azure SQL DB 지원 되지 않는 기능 보고서](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

이 보고서는 대상이 Azure SQL Database 될 때 지정 된 **데이터베이스** 에 대해 지원 되지 않는 기능을 강조 표시 합니다 (V12).

깔때기형 차트에서 데이터베이스 이름 및 기능 값을 기준으로 필터링 하 여 지원 되지 않는 기능에 대 한 세부 정보를 볼 수 있습니다. 세부 정보에는 영향을 받는 개체와 문제 해결에 대 한 권장 사항이 포함 됩니다.

예를 들어 DTC 데이터베이스 및 **읽기 전용 데이터베이스**에의 한 필터링을 업그레이드할 수 없는 경우 영향을 받는 개체의 목록을 볼 수 있습니다.

![읽기 전용 데이터베이스는 업그레이드할 수 없습니다.](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>참고 항목

[Data Migration Assistant 개요](../dma/dma-overview.md)

[다운로드 Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)

[다운로드 Power BI](https://powerbi.microsoft.com/)
