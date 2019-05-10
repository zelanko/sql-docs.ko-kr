---
title: Analysis Services Adventure Works Internet Sales 자습서 (1400) | Microsoft Docs
ms.date: 05/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 39d4c0e19d89438aa08ff2f7ead24184196d5412
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65503282"
---
# <a name="adventure-works-internet-sales-tutorial-1400"></a>Adventure Works Internet Sales 자습서 (1400)

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

이 자습서 만들고에서 테이블 형식 모델을 배포 하는 방법에 대 한 단원을 제공 합니다 [1400 호환성 수준의](../tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)합니다. Analysis Services 테이블 형식 모델링을 접하는 경우이 자습서를 완료 해야 만들기 및 Visual Studio를 사용 하 여 기본 테이블 형식 모델을 배포 하는 방법에 대 한 가장 빠른 방법입니다. 필수 구성 요소를 만든 후 바로 2 ~ 3 시간이 걸립니다를 완료 합니다.  
  
## <a name="what-you-learn"></a>학습 내용   
  
-   새 테이블 형식 모델 프로젝트를 만드는 방법 합니다 **1400 호환성 수준의** SSDT 사용 하 여 Visual Studio에서.
  
-   관계형 데이터베이스에서 테이블 형식 모델 프로젝트 작업 영역 데이터베이스로 데이터를 가져오는 방법입니다.  
  
-   모델의 테이블 간에 관계를 만들고 관리하는 방법  
  
-   계산된 열, 측정값 및 중요 한 비즈니스 메트릭을 분석 하는 데 도움이 되는 핵심 성과 지표를 만드는 방법입니다.  
  
-   사용자가 더 많은 비즈니스 및 응용 프로그램별 관점을 제공 하 여 모델 데이터를 쉽게 찾아볼 수 있도록 계층 및 큐브 뷰 만들기 및 관리 하는 방법.  
  
-   다른 파티션과 독립적으로 처리할 수 있도록 테이블 데이터를 더 작은 논리적 부분으로 나누는 파티션을 만드는 방법  
  
-   사용자 멤버 기반 역할을 만들어 모델 개체 및 데이터를 보호하는 방법  
  
-   테이블 형식 모델을 배포 하는 방법에 **Azure Analysis Services** 서버 또는 **SQL Server 2017 Analysis Services** SSDT를 사용 하 여 서버.  
  
## <a name="prerequisites"></a>사전 요구 사항  

이 자습서를 완료 하려면 다음을 수행 해야 합니다.  
  
-   Azure Analysis Services 서버 또는 테이블 형식 모드에서 SQL Server 2017 Analysis Services 서버. 무료 등록 [Azure Analysis Services 평가판](https://azure.microsoft.com/services/analysis-services/) 하 고 [서버를 만듭니다](https://docs.microsoft.com/azure/analysis-services/analysis-services-create-server) 또는 무료 다운로드 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)합니다.

-   [Azure SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/create-data-warehouse-portal) 사용 하 여 합니다 **AdventureWorksDW 샘플 데이터베이스**, 또는 온-프레미스 SQL Server Data Warehouse를 사용 하 여는 [AdventureWorksDW 예제 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)합니다. AdventureWorksDW 데이터베이스를 온-프레미스 SQL Server 데이터 웨어하우스를 설치할 때 서버 버전을 사용 하 여 해당 하는 샘플 데이터베이스 버전을 사용 합니다. 

    **중요:** 온-프레미스 SQL Server Data Warehouse로 샘플 데이터베이스를 설치 하는 Azure Analysis Services 서버에 모델을 배포 하는 경우는 [온-프레미스 데이터 게이트웨이](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) 필요 합니다.

-   최신 버전의 [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx)합니다. 또는 Visual Studio 2017에 이미 있는 경우에 다운로드 고 설치할 수 있습니다 [Microsoft Analysis Services Projects](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects) 패키지 (VSIX). 이 자습서에서는 SSDT 및 Visual Studio에 대 한 참조는 동의어입니다. 

-   최신 버전의 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.    

-   와 같은 클라이언트 응용 프로그램 [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 또는 Excel입니다. 

## <a name="scenario"></a>시나리오  

이 자습서는 회사인 Adventure Works Cycles를 기반으로 합니다. Adventure Works는를 생성 하 고 자전거, 부품 및 액세서리 북아메리카, 유럽 및 아시아의 상업 시장에 대 한 배포는 대규모의 다국적 제조 회사입니다. 이 회사는 500 명입니다. 또한 Adventure Works는 시장 기반 전체에 여러 지역별 영업 팀을 사용합니다. 프로젝트가는 AdventureWorksDW 데이터베이스의 인터넷 매출 데이터를 분석 하려면 영업 및 마케팅 사용자에 대 한 테이블 형식 모델을 만드는 것입니다.  
  
이 자습서를 완료 하려면 다양 한 단원을 완료 해야 합니다. 각 단원에는 작업이 있습니다. 순서로 각 태스크를 완료 하는 것은 단원을 완료 해야 합니다. 특정 단원에 있을 수 있습니다 유사한 결과 얻는 몇 가지 작업이 있지만 각 작업을 완료 하는 방법을 하는 것은 약간 다릅니다. 이 메서드는 방법이 종종 둘 이상의 작업을 완료 하는 데 문제를 해결할 수 이전 단원 및 작업에서 배운 기술을 사용 하 여 보여 줍니다.  
  
이 단원의 목적은 SSDT에 포함 된 기능을 많이 사용 하 여 기본 테이블 형식 모델을 작성 하는 과정을 안내 하는 경우 각 단원은 이전 단원에 기반을 두고 있으므로 단원을 순서대로 완료해야 합니다.
  
이 자습서는 Azure portal, SSMS를 사용 하 여 클라이언트 응용 프로그램 모델 데이터를 이동할 서버 또는 데이터베이스 관리의 서버를 관리 하는 방법에 대 한 단원을 제공 하지 않습니다. 


## <a name="lessons"></a>단원  

이 자습서에는 다음 단원이 포함되어 있습니다.  
  
|단원|소요되는 예상 시간|  
|----------|------------------------------|  
|[1-새 테이블 형식 모델 프로젝트 만들기](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)|10분|  
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

이 단원에서는 자습서를 완료 하는 데 필요한 되지 않지만 더 나은 이해 고급 테이블 형식 모델 제작 기능 하는 데 도움이 될 수 있습니다.  
  
|단원|소요되는 예상 시간|  
|----------|------------------------------|  
|[정보 행](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)|10분|
|[동적 보안](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)|30분|
|[비정형된 계층](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)|20분| 

  
## <a name="next-steps"></a>다음 단계  

시작 하려면 참조 [1 단원: 새 테이블 형식 모델 프로젝트를 만들](../tutorial-tabular-1400/as-lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
  
  

