---
title: "테이블 형식 모델링 (Adventure Works 자습서) | Microsoft Docs"
ms.custom: 
ms.date: 04/19/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
keywords:
- Analysis Services
- "테이블 형식 모델"
- "자습서"
- SSAS
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 811b5df37a88fa7a03eec2b9bc05acb87ec67bcc
ms.contentlocale: ko-kr
ms.lasthandoff: 09/27/2017

---
# <a name="tabular-modeling-adventure-works-tutorial"></a>테이블 형식 모델링(Adventure Works 자습서)
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

이 자습서에는 Analysis Services 테이블 형식 모델을 만드는 방법에 단원에서 제공 된 [1200 호환성 수준](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md) 를 사용 하 여 [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt), Analysis services 모델을 배포 하 고 온-프레미스 서버 또는 Azure입니다.  
 
SQL Server 2017 또는 Azure Analysis Services를 사용 하는 모델 수준에서 1400 호환성 생성, 사용 하려는 경우는 [Azure Analysis Services-Adventure Works 자습서](https://review.docs.microsoft.com/azure/analysis-services/tutorials/aas-adventure-works-tutorial?branch=master)합니다. 이 업데이트 된 버전 새, 최신 데이터 가져오기 기능을 사용 하 여 연결 하 고 원본 데이터를 가져올 하 고 파티션을 구성 하는 M 언어를 사용 합니다.
 
  
## <a name="what-youll-learn"></a>학습 내용   
  
-   SSDT에서 새 테이블 형식 모델 프로젝트를 만들 하는 방법.
  
-   SQL Server 관계형 데이터베이스의 데이터를 테이블 형식 모델 프로젝트로 가져오는 방법  
  
-   모델의 테이블 간에 관계를 만들고 관리하는 방법  
  
-   사용자가 모델 데이터를 분석하는 데 도움을 주는 계산, 측정값 및 핵심 성과 지표를 만들고 관리하는 방법  
  
-   비즈니스 및 응용 프로그램별 뷰포인트를 통해 사용자가 모델 데이터를 쉽게 탐색할 수 있도록 도움을 주는 큐브 뷰와 계층을 만들고 관리하는 방법  
  
-   다른 파티션과 독립적으로 처리할 수 있도록 테이블 데이터를 더 작은 논리적 부분으로 나누는 파티션을 만드는 방법  
  
-   사용자 멤버 기반 역할을 만들어 모델 개체 및 데이터를 보호하는 방법  
  
-   Analysis Services 서버 온-프레미스 또는 Azure에서 테이블 형식 모델을 배포 하는 방법입니다.  
  
## <a name="scenario"></a>시나리오  
이 자습서에서는 Adventure Works Cycles 가상의 회사를 기반으로 합니다. Adventure Works에서 북미, 유럽 및 아시아 시장에 판매를 금속 및 합성 소재 하는 대규모 다국적 제조 회사입니다. 워싱턴 주 보 셀에에서 본사가 고 있으며 직원 수 500 명입니다. 또한 Adventure Works에서는 여러 지역에 영업 팀 시장에 전반를 사용합니다.  
  
영업과 마케팅 팀 및 경영 관리에 필요한 데이터 분석을 지원하기 위해 사용자가 AdventureWorksDW 예제 데이터베이스의 인터넷 매출 데이터를 분석할 수 있도록 테이블 형식 모델을 만들려고 합니다.  
  
자습서를 완료하고 Adventure Works Internet Sales 테이블 형식 모델을 완성하려면 여러 단원을 완료해야 합니다. 각 단원 내에는 많은 태스크가 포함되어 있으며 단원을 완료하려면 각 태스크를 순서대로 완료해야 합니다. 특정 단원에 있을 수 있습니다는 비슷한 결과 수행 하는 몇 가지 작업 동안 각 작업을 완료 하는 방법은 약간 다릅니다. 이 여러 가지 방법으로 특정 작업을 완료 하 고 이전 작업에서 배운 기술을 사용해 보도록 하기 종종 임을 나타낼 수 있습니다.  
  
단원의 목적은 여러 SSDT에 포함 된 기능을 사용 하 여 메모리 내 모드로 실행 되는 기본 테이블 형식 모델 제작 하는 과정을 안내 하는 합니다. 각 단원은 이전 단원에 기반을 두고 있으므로 단원을 순서대로 완료해야 합니다. 모든 단원을 완료 했으면, 작성 및 Analysis Services 서버에서 Adventure Works Internet Sales 예제 테이블 형식 모델 배포 있어야 합니다.  
  
이 자습서에서는 배포한 테이블 형식 모델 데이터베이스를 SQL Server Management Studio를 사용하여 관리하거나 보고 클라이언트 응용 프로그램을 사용하여 배포된 모델에 연결하여 모델 데이터를 탐색하는 과정을 안내하는 단원이나 정보는 제공하지 않습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
이 자습서를 완료 하려면 다음 필수 구성 요소가 필요 합니다.  
  
-   최신 버전의 [! 포함[ssBIDevStudioFull](../ssdt/download-sql-server-data-tools-ssdt.md)합니다.

-   SQL Server Management Studio의 최신 버전입니다. [최신 버전 가져오기](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다. 
  
-   와 같은 클라이언트 응용 프로그램 [Power BI Desktop](https://powerbi.microsoft.com/desktop/) 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel입니다.    
  
-   Adventure Works DW 2014 샘플 데이터베이스에서 SQL Server 인스턴스. 이 예제 데이터베이스에는 이 자습서를 완료하는 데 필요한 데이터가 포함되어 있습니다. [최신 버전 가져오기](http://go.microsoft.com/fwlink/?LinkID=335807)합니다.  
  

-   Azure Analysis Services 또는 SQL Server 2016 또는 이상의 Analysis Services 인스턴스에서 사용자 모델을 배포 합니다. [Azure Analysis Services에 무료 평가판에 등록](https://azure.microsoft.com/services/analysis-services/)합니다.
  
## <a name="lessons"></a>단원  
이 자습서에는 다음 단원이 포함되어 있습니다.  
  
|단원|소요되는 예상 시간|  
|----------|------------------------------|  
|[1단원: 새 테이블 형식 모델 프로젝트를 만들기](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)|10분|  
|[2단원: 데이터 추가](../analysis-services/lesson-2-add-data.md)|20분|  
|[3단원: 날짜 테이블로 표시](../analysis-services/lesson-3-mark-as-date-table.md)|3분|  
|[4 단원: 관계 만들기](../analysis-services/lesson-4-create-relationships.md)|10분|  
|[5 단원: 계산된 열 만들기](../analysis-services/lesson-5-create-calculated-columns.md)|15분|
|[6 단원: 측정값 만들기](../analysis-services/lesson-6-create-measures.md)|30분|  
|[7단원: 핵심 성과 지표 만들기](../analysis-services/lesson-7-create-key-performance-indicators.md)|15분|  
|[8 단원: 큐브 뷰 만들기](../analysis-services/lesson-8-create-perspectives.md)|5분|  
|[9 단원: 계층 만들기](../analysis-services/lesson-9-create-hierarchies.md)|20분|  
|[10 단원: 파티션 만들기](../analysis-services/lesson-10-create-partitions.md)|15분|  
|[11 단원: 역할 만들기](../analysis-services/lesson-11-create-roles.md)|15분|  
|[12단원: Excel에서 분석](../analysis-services/lesson-12-analyze-in-excel.md)|20분| 
|[13단원: 배포](../analysis-services/lesson-13-deploy.md)|5분|  
  
## <a name="supplemental-lessons"></a>추가 단원  
이 자습서에는 [추가 단원](http://msdn.microsoft.com/library/2018456f-b4a6-496c-89fb-043c62d8b82e)도 포함되어 있습니다. 이 섹션의 항목은 자습서를 완료하기 위한 필수 항목은 아니지만 고급 테이블 형식 모델 제작 기능을 더 잘 이해하는 데 유용할 수 있습니다.  
  
|단원|소요되는 예상 시간|  
|----------|------------------------------|  
|[행 필터를 사용하여 동적 보안 구현](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md)|30분|  

  
## <a name="next-step"></a>다음 단계  
자습서를 시작하려면 첫 번째 단원인 [1단원: 새 테이블 형식 모델 프로젝트를 만들기](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)로 이동하세요.  
  
  
  


