---
title: 가져오기 및 Data Migration Assistant 평가 보고서 (SQL Server) 통합 | Microsoft Docs
description: Data Migration Assistant에서 평가 보고서를 SQL Server 데이터베이스를 가져오는 고 여러 보고서를 통합 하는 방법을 알아봅니다
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: be9fc224093f0d5ae14372d4674a52589a2d4801
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781774"
---
# <a name="import-and-consolidate-data-migration-assistant-assessment-reports"></a>가져오기 및 Data Migration Assistant 평가 보고서 통합

Data Migration Assistant v2.1부터 무인 모드로 마이그레이션 평가 수행 하는 명령줄을 사용할 수 있습니다. 이 기능을 사용 하면 대규모로 평가 실행 하도록 도와줍니다. 평가 결과 JSON 또는 CSV 파일의 형식에서입니다.

Data Migration Assistant 명령줄 유틸리티의 단일 인스턴스화에서 여러 데이터베이스를 평가 하 고 모든 평가 결과를 단일 JSON 파일로 내보낼 수 있습니다. 또는 시간에 하나의 데이터베이스를 평가 하 고 나중에 SQL 데이터베이스에 이러한 여러 JSON 파일에서 결과 통합 합니다.

명령줄에서 Data Migration Assistant를 실행 하는 방법에 대 한 자세한 내용은 [실행 Data Migration Assistant 명령줄에서](../dma/dma-commandline.md)합니다. 

## <a name="import-assessment-results-into-a-sql-server-database"></a>평가 결과 SQL Server 데이터베이스 가져오기

이 사용할 수 있는 PowerShell 스크립트를 사용 하 여 [Github 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) SQL Server 데이터베이스에 JSON 파일에서 평가 결과 가져오려고 합니다.

> [!NOTE]
> PowerShell v5 이상이 필요 합니다.

스크립트를 실행 하는 경우 다음 정보를 제공 해야 합니다. 

- **serverName**: SQL Server 인스턴스 이름을 가져오려는 평가 JSON 파일에서 발생 합니다.

- **databaseName**: 결과를 가져오지는 데이터베이스 이름입니다.

- **jsonDirectory**: 평가 결과 하나 이상의 JSON 파일에 저장 된 폴더입니다.

- **processTo**: sql Server

위의 값 "함수 실행" 섹션에서 다음과 같이 추가 합니다.

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

PowerShell 스크립트는 개체가 아직 존재 하지 않습니다 하는 경우 사용자가 지정한 SQL 인스턴스에 다음 개체를 만듭니다.

- **데이터베이스** – PowerShell 매개 변수에서 제공 된 이름

  - 기본 리포지토리

- **테이블** – 보고서 데이터

  - 보고에 대 한 데이터

- **테이블** -BreakingChangeWeighting

  - 모든 주요 변경 내용에 대 한 참조 테이블입니다. 여기에 보다 정확한 백분율 (%) 업그레이드 성공 순위 영향을 주는 고유한 가중치 값을 정의할 수 있습니다.

- **뷰** – UpgradeSuccessRanking\_온-프레미스

  - 각 데이터베이스 마이그레이션된 온-프레미스에 대 한 성공 비율을 표시 하는 보기입니다.

- **뷰** – UpgradeSuccessRanking\_Azure

  - 각 데이터베이스 마이그레이션된 온-프레미스에 대 한 성공 비율을 표시 하는 보기입니다.

- **저장 프로시저** – JSONResults\_삽입

  - SQL Server에 JSON 파일에서 데이터를 가져오기 하는 데 사용 합니다.

- **저장 프로시저** – AzureFeatureParityResults\_삽입

  - SQL Server에 JSON 파일에서 Azure 기능 패리티 결과 가져오는 데 사용 합니다.

- **테이블 형식** – JSONResults

  - 온-프레미스 평가 대 한 JSON 결과 저장 하 고는 JSONResults를 전달 하는 데\_Insert 저장된 프로시저

- **테이블 형식** – AzureFeatureParityResults

  - Azure 기능에 대 한 azure 평가 패리티 결과 저장 하 고는 AzureFeatureParityResults 전달할 데\_Insert 저장된 프로시저

PowerShell 스크립트를 만듭니다는 **처리** 처리할 수 있는 JSON 파일을 포함 하는 사용자가 제공한 디렉터리 내 디렉터리입니다.

스크립트를 완료 한 후 보고서 데이터 테이블에 결과 가져옵니다.

### <a name="viewing-the-results-in-sql-server"></a>SQL Server에서 결과 보기

데이터가 로드 된 후에 SQL Server 인스턴스에 연결 합니다. 다음 그림에 나와 있는 것 처럼 화면 표시 됩니다.

![SQL Server 데이터베이스에 통합 된 보고서](../dma/media/DMAReportingDatabase.png)

Dbo입니다. 보고서 데이터 테이블에 원시 형식으로 JSON 파일의 내용을 포함합니다.

## <a name="on-premises-upgrade-success-ranking"></a>온-프레미스 업그레이드 성공 순위

데이터베이스와 해당 백분율 (%) 성공 순위 목록을 보려면 dbo를 선택 합니다. UpgradeSuccessRanking_OnPrem 보기:

![UpgradeSuccessRaning_OnPrem 뷰에서 데이터](../dma/media/UpgradeSuccessRankingView.png)

여기서 볼 수 있습니다 지정된 된 데이터베이스에 대 한 다양 한 호환성 수준에 대 한 업그레이드 성공 가능성은. 따라서 예를 들어 호환성 수준 100, 110, 120 및 130에 대 한 HR 데이터베이스 평가 되었습니다. 이 평가 통해 시각적으로 현재 데이터베이스가 현재 버전에서 SQL Server의 이후 버전으로의 마이그레이션에 관련 된 작업의 양을 확인할 수 있습니다.

일반적으로 중요 한 메트릭은 얼마나 많은 주요 변경 사항이 지정된 된 데이터베이스입니다. 앞의 예제에서 HR 데이터베이스에 호환성 수준 100, 110, 120 및 130에 대 한 50% 업그레이드 성공 비율을 확인할 수 있습니다.

이 메트릭은 dbo에 가중치 값을 변경 하 여 영향을 받을 수 있습니다. BreakingChangeWeighting 테이블입니다.

다음 예제에서는 HR 데이터베이스의 구문 문제를 해결 하는 관련 된 작업으로 간주 됩니다 높은 값 3에 할당 됩니다 **노력**합니다. 1 값은 구문 문제를 해결 하려면 긴 수행 하지 않습니다, 않으므로 **FixTime**합니다. 2의 값이 할당 하므로 약간의 비용 변경 과정에 참여 합니다 **비용**합니다. 이 값을 사용 하 여 혼합된 Changerank이 2로 변경 합니다.

> [!NOTE]
> 점수 매기기 소수 자릿수가 1-5 켜져 있습니다.  1 가장 낮은 고 5 가장 높은 합니다. 또한는 ChangeRank 계산된 열입니다.

![구문 문제에 대 한 노력과 FixTime, 비용 값](../dma/media/SyntaxIssueEffort.png)

이제이 예에서 dbo를 쿼리 하는 경우. UpgradeSuccessRanking_OnPrem 보기의 주요 변경 내용에 대 한 HR 데이터베이스에 대 한 업그레이드 성공 비율을 삭제 했습니다.

![HR 데이터베이스에 대 한 업그레이드 성공 비율](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Azure 업그레이드 성공 순위

Azure SQL DB 및 백분율 성공 차수로 마이그레이션하려는 데이터베이스의 목록을 보려면 dbo를 선택 합니다. UpgradeSuccessRanking_Azure 뷰입니다.

![UpgradeSuccessRanking_Azure 뷰에서 데이터](../dma/media/UpgradeSuccessRankingView_Azure.png)

여기서 관심 MigrationBlocker 값입니다. 100.00은 Azure SQL Database v12로 데이터베이스 이동에 대 한 100% 성공 순위를 의미 합니다.

이 보기를 사용 하 여 차이점은 마이그레이션 차단 규칙에 대 한 가중치를 변경 하는 것에 대 한 재정의 없습니다 현재입니다.

Power BI를 사용 하 여이 데이터에 대 한 보고에 대 한 내용은 참조 하세요 [PowerBI 사용 하 여 통합된 평가 대해 보고](../dma/dma-powerbiassesreport.md)합니다.
