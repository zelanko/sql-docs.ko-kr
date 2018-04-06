---
title: 평가 보고서 (SQL Server 데이터 Migration Assistant)를 통합 | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d0dd690a34cf2e4bf5df2d758f65da9b1123506
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="consolidate-assessment-reports-data-migration-assistant"></a>(데이터 마이그레이션 길잡이) 평가 보고서 통합

데이터 마이그레이션 길잡이 (v2.1) 부터는 무인 모드로 마이그레이션 평가 수행 하는 명령줄을 사용할 수 있습니다. 이 기능을 사용 하면 규모에는 평가 실행 합니다.  JSON 또는 CSV 파일의 형태로 평가 결과입니다.

여러 데이터베이스 데이터 Migration Assistant 명령줄 유틸리티의 단일 인스턴스화를 평가할 수 있으며 하나의 JSON 파일에 모든 평가 결과 내보낼 수 있습니다. 또는 번에 하나의 데이터베이스를 평가 하 고 나중에 SQL 데이터베이스에 이러한 여러 JSON 파일의 결과 통합 수 있습니다.

명령줄에서 데이터 마이그레이션 도우미를 실행 하는 방법에 대 한 정보를 참조 하십시오. [실행 데이터 Migration Assistant 명령줄에서](../dma/dma-commandline.md)합니다. 


## <a name="import-assessment-results-into-a-sql-server-database"></a>SQL Server 데이터베이스에 평가 결과 가져오기

이 제공 되는 PowerShell 스크립트를 사용 하 여 [Github 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) SQL Server 데이터베이스로 JSON 파일에서 평가 결과 가져옵니다.

스크립트를 실행 하는 경우 다음 정보를 제공 해야 합니다. 

- **serverName**: SQL Server 인스턴스 이름을 가져오려는 평가 하는 JSON 파일에서 결과입니다.

- **databaseName**: 결과 가져오기에 가져온 데이터베이스 이름입니다.

- **jsonDirectory**: 하나 이상의 JSON 파일에, 평가 결과 저장 하는 폴더입니다.

- **processTo**: sql Server

다음과 같이 이전 값 "함수 실행" 섹션에 추가 합니다.

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

PowerShell 스크립트 개체가 아직 존재 하지 않는 경우의 사용자가 지정한 SQL 인스턴스는 다음과 같은 개체를 만듭니다.

- **데이터베이스** -PowerShell 매개 변수에 제공 된 이름

  - 주 저장소

- **테이블** – 보고서 데이터

  - 보고에 대 한 데이터

- **테이블** -BreakingChangeWeighting

  - 모든 주요 변경 내용에 대 한 참조 테이블입니다.  여기 백분율 (%) 보다 정확 하 게 업그레이드 성공 순위에 영향을 줍니다 사용자 고유의 가중치 값을 정의할 수 있습니다.

- **보기** – UpgradeSuccessRanking\_온-프레미스

  - 마이그레이션된 온-프레미스에 각 데이터베이스에 대 한 성공의 요소를 표시 하는 보기입니다.

- **보기** – UpgradeSuccessRanking\_Azure

  - 마이그레이션된 온-프레미스에 각 데이터베이스에 대 한 성공의 요소를 표시 하는 보기입니다.

- **저장 프로시저** – JSONResults\_삽입

  - SQL Server로 JSON 파일에서 데이터를 가져오기 하는 데 사용 합니다.

- **저장 프로시저** – AzureFeatureParityResults\_삽입

  - SQL Server로 JSON 파일에서 Azure 기능 패리티 결과 가져오는 데 사용 합니다.

- **테이블 형식** – JSONResults

  - 온-프레미스 평가 대 한 JSON 결과 저장 하 고는 JSONResults를 전달 하는 데 사용\_저장된 프로시저를 삽입 합니다.

- **테이블 형식** – AzureFeatureParityResults

  - Azure 기능 평가 azure에 대 한 패리티 결과 저장 하 고는 AzureFeatureParityResults를 전달 하는 데 사용\_저장된 프로시저를 삽입 합니다.

PowerShell 스크립트를 만듭니다는 **Processed** 처리 되도록 하는 JSON 파일을 포함 하는 디렉터리 사용자가 제공한 내 디렉터리입니다.

스크립트가 완료 된 후 결과 테이블을 보고서 데이터를 가져옵니다.

### <a name="viewing-the-results-in-sql-server"></a>SQL Server에서 결과 보기

데이터가 로드 된 후에 SQL Server 인스턴스에 연결 합니다. 다음을 참조 합니다.

![SQL Server 데이터베이스에 통합 된 보고서](../dma/media/DMAReportingDatabase.png)

Dbo입니다. 보고서 데이터 테이블에는 원시 형식으로 JSON 파일의 내용을 포함합니다.

## <a name="on-premises-upgrade-success-ranking"></a>온-프레미스 업그레이드 성공 순위

데이터베이스와 해당 백분율 (%) 성공 순위 목록의 보려면 dbo를 선택 합니다. UpgradeSuccessRanking_OnPrem 보기:

![UpgradeSuccessRaning_OnPrem 뷰에서 데이터](../dma/media/UpgradeSuccessRankingView.png)

여기에서는 내용을 볼 수는 지정 된 데이터베이스에 대 한 다른 호환성 수준에 대 한 업그레이드 성공 가능성 합니다.  따라서 예를 들어 호환성 수준 100, 110, 120 및 130에 대 한 HR 데이터베이스 평가 되었습니다.  이 평가 사용 하면 시각적으로 데이터베이스에 현재 있는 현재 버전에서 최신 버전의 SQL Server로 마이그레이션 관련 작업의 양을 참조 합니다.

일반적으로 신경을 메트릭을는 지정된 된 데이터베이스에 대 한는 얼마나 많은 주요 변경 내용이 있습니다.  앞의 예에서 HR 데이터베이스 호환성 수준 100, 110, 120 및 130에 대 한 50% 업그레이드 성공 요소에 알 수 있습니다.

이 메트릭은 dbo에서 가중치 값을 변경 하 여 영향을 받을 수 있습니다. BreakingChangeWeighting 테이블입니다.

다음 예에서 HR 데이터베이스에서 구문 문제를 해결 하는 노력이 너무 많습니다 값 3에 할당 됩니다 **노력**합니다. 이 값이 1은 구문 문제를 해결 하려면 긴 사용할가 있기 때문에 **FixTime**합니다. 이 값이 2은 있기 때문에 있는 일부 비용이 변경 하는 것에 관련 된, **비용**합니다.  이 혼합된 Changerank 2로 변경 됩니다.

> [!NOTE]
> 점수 매기기는 1-5 까지의 값입니다.  1 낮은 고 5 높은 합니다. 또한는 ChangeRank은 계산된 열입니다.

![구문 문제에 대 한 값을 노력, FixTime, 고 비용](../dma/media/SyntaxIssueEffort.png)

이제이 예에서 dbo를 쿼리할 때. 주요 변경 내용에 대 한 HR 데이터베이스에 대 한 업그레이드 성공 요인인 떨어진 UpgradeSuccessRanking_OnPrem 보기.

![HR 데이터베이스에 대 한 업그레이드 성공 요소](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Azure 업그레이드 성공 순위

Azure SQL DB를 백분율 성공 차수 마이그레이션할 데이터베이스의 목록을 보려면 dbo를 선택 합니다. UpgradeSuccessRanking_Azure 보기입니다.

![UpgradeSuccessRanking_Azure 뷰에서 데이터](../dma/media/UpgradeSuccessRankingView_Azure.png)

여기 MigrationBlocker 값에 관심 있는 합니다.  100.00은 데이터베이스를 Azure SQL 데이터베이스 v 12로 이동 하기 위한 100% 성공 순위 임을 의미 합니다.

이 보기를 사용 하 여 차 마이그레이션 차단 규칙에 대 한 가중치 변경에 대 한 재정의 없습니다 현재 된다는 점입니다.

Power BI를 사용 하 여이 데이터에 대 한 보고에 대 한 자세한 내용은 참조 [PowerBI와 통합된 하면 평가 대해 보고](../dma/dma-powerbiassesreport.md)합니다.


