---
title: Analysis Services Adventure Works 자습서 (1400) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28aa401eb037fecadca17ededf041ab82a4bc498
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044577"
---
# <a name="tabular-modeling-1400-compatibility-level"></a>테이블 형식 모델링 (1400 호환성 수준)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 자습서를 만들고 테이블 형식 모델에 배포 하는 방법에 단원에서 제공 된 [1400 호환성 수준이](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)합니다. Analysis Services 및 테이블 형식 모델링에 익숙하지 않다면이 자습서를 완료 가장 빠른 방법은 만들어 Visual Studio를 사용 하 여 기본 테이블 형식 모델을 배포 하는 방법을 배울 수 있습니다. 사전 요구 사항이 충족 되 면 내부를 완료 하려면 2 ~ 3 시간 수행 해야 합니다.  
  
## <a name="what-you-learn"></a>정보   
  
-   새 테이블 형식 모델 프로젝트를 만드는 방법의 **1400 호환성 수준이** Visual Studio에서 SSDT로 합니다.
  
-   관계형 데이터베이스에서 테이블 형식 모델 프로젝트 작업 영역 데이터베이스로 데이터를 가져오기 하는 방법.  
  
-   모델의 테이블 간에 관계를 만들고 관리하는 방법  
  
-   계산된 열, 측정값 및 중요 한 비즈니스 메트릭을 분석 하는 데 도움이 되는 핵심 성과 지표를 만드는 방법  
  
-   큐브 뷰 및 사용자가 더 많은 비즈니스 및 응용 프로그램별 뷰포인트를 제공 하 여 모델 데이터를 쉽게 찾아볼 수 있도록 계층 만들기 및 관리 하는 방법.  
  
-   다른 파티션과 독립적으로 처리할 수 있도록 테이블 데이터를 더 작은 논리적 부분으로 나누는 파티션을 만드는 방법  
  
-   사용자 멤버 기반 역할을 만들어 모델 개체 및 데이터를 보호하는 방법  
  
-   테이블 형식 모델을 배포 하는 방법 한 **Azure Analysis Services** 서버 또는 **SQL Server 2017 Analysis Services** SSDT를 사용 하 여 서버입니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  

이 자습서를 완료 하려면 다음을 수행 해야 합니다.  
  
-   Azure Analysis Services 서버 또는 테이블 형식 모드에서 SQL Server 2017 Analysis Services 서버입니다. 무료 등록 [Azure Analysis Services 평가판](https://azure.microsoft.com/services/analysis-services/) 및 [서버 만들기](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) 무료 다운로드 또는 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)합니다.

-   [Azure SQL 데이터 웨어하우스](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) 와 **AdventureWorksDW 예제 데이터베이스**, 또는로 온-프레미스 SQL Server 데이터 웨어하우스는 [AdventureWorksDW 예제 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)합니다. AdventureWorksDW 데이터베이스는 온-프레미스 SQL Server 데이터 웨어하우스를 설치할 때 서버 버전으로 해당 하는 샘플 데이터베이스 버전을 사용 합니다. 

    **중요:** 온-프레미스 SQL Server 데이터 웨어하우스를 예제 데이터베이스를 설치 하는 Azure Analysis Services 서버에 모델을 배포 하는 경우는 [온-프레미스 데이터 게이트웨이](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) 가 필요 합니다.

-   최신 버전의 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)합니다. Visual Studio 2017 이미 있는 경우에 다운로드 및 설치할 수 있습니다 또는 [Microsoft Analysis Services 프로젝트](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) 패키지 (VSIX). 이 자습서에 대 한 SSDT 및 Visual Studio에 대 한 참조는 동의어입니다. 

-   최신 버전의 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.    

-   와 같은 클라이언트 응용 프로그램 [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 또는 Excel입니다. 

## <a name="scenario"></a>시나리오  

이 자습서에서는 Adventure Works Cycles 가상의 회사를 기반으로 합니다. Adventure Works를 생성 하 고 자전거, 파트 및에서 북미, 유럽 및 아시아 시장에 판매에 대 한 보조 프로그램을 배포 하는 대규모의 다국적 제조 회사입니다. 고 있으며 직원 수는 500 명입니다. 또한 Adventure Works에서는 여러 지역에 영업 팀 시장에 전반를 사용합니다. 프로젝트는 영업 및 마케팅 사용자가 AdventureWorksDW 데이터베이스의 인터넷 매출 데이터를 분석 하는 테이블 형식 모델을 만드는 것입니다.  
  
자습서를 완료 하려면 다양 한 단원을 완료 해야 합니다. 각 단원에는 작업이 있습니다. 순서로 각 작업을 완료 하는 단원을 완료 해야 합니다. 특정 단원에 있을 수 있습니다는 비슷한 결과 수행 하는 몇 가지 작업 동안 각 작업을 완료 하는 방법은 약간 다릅니다. 이 메서드는 여러 가지 방법으로 작업을 완료 하 고 이전 단원 및 작업에서 배운 기술을 사용해 보도록 하기 방식은 표시 합니다.  
  
단원의 목적은 여러 SSDT에 포함 된 기능을 사용 하 여 기본 테이블 형식 모델 제작 하는 과정을 안내 하는 합니다. 각 단원은 이전 단원에 기반을 두고 있으므로 단원을 순서대로 완료해야 합니다.
  
이 자습서에서는 SSMS를 사용 하 여 또는 클라이언트 응용 프로그램을 사용 하 여 모델 데이터를 검색 하 여 서버 또는 데이터베이스를 관리 하는 Azure 포털의 서버를 관리 하는 방법에 대 한 학습을 제공 하지 않습니다. 


## <a name="lessons"></a>단원  

이 자습서에는 다음 단원이 포함되어 있습니다.  
  
|단원|소요되는 예상 시간|  
|----------|------------------------------|  
|[1-새로운 테이블 형식 모델 프로젝트 만들기](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10분|  
|[2 - 데이터 가져오기](../tutorial-tabular-1400/as-lesson-2-get-data.md)|10분|  
|[3 - 날짜 테이블로 표시](../tutorial-tabular-1400/as-lesson-3-mark-as-date-table.md)|3분|  
|[4 - 관계 만들기](../tutorial-tabular-1400/as-lesson-4-create-relationships.md)|10분|  
|[5 - 계산 열 만들기](../tutorial-tabular-1400/as-lesson-5-create-calculated-columns.md)|15분|
|[6 - 측정값 만들기](../tutorial-tabular-1400/as-lesson-6-create-measures.md)|30분|  
|[7-핵심 성과 지표 (KPI) 만들기](../tutorial-tabular-1400/as-lesson-7-create-key-performance-indicators.md)|15분|  
|[8 - 큐브 뷰 만들기](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md)|5분|  
|[9 - 계층 만들기](../tutorial-tabular-1400/as-lesson-9-create-hierarchies.md)|20분|  
|[10 - 파티션 만들기](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)|15분|  
|[11 - 역할 만들기](../tutorial-tabular-1400/as-lesson-11-create-roles.md)|15분|  
|[12 - Excel에서 분석](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)|5분| 
|[13 - 배포](../tutorial-tabular-1400/as-lesson-13-deploy.md)|5분|  
  
## <a name="supplemental-lessons"></a>추가 단원  

이러한 단원 자습서를 완료 하려면 필요 하지 않지만 더 나은 이해 고급 테이블 형식 모델 제작 기능에에서 도움이 될 수 있습니다.  
  
|단원|소요되는 예상 시간|  
|----------|------------------------------|  
|[정보 행](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10분|
|[동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30분|
|[비정형된 계층 구조](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20분| 

  
## <a name="next-steps"></a>다음 단계  

시작 하려면 참조 [1 단원: 새 테이블 형식 모델 프로젝트 만들기](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
  
  

