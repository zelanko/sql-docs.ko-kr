---
title: 테이블 형식 모델링 (Adventure Works 자습서) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 140d0b43-9455-4907-9827-16564a904268
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af4d5dfa6d59338fb9640143b387b78421375e05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067796"
---
# <a name="tabular-modeling-adventure-works-tutorial"></a>테이블 형식 모델링(Adventure Works 자습서)
  이 자습서에서는 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]를 사용하여 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Analysis Services 테이블 형식 모델을 만드는 방법을 설명하는 단원을 제공합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 다음 항목을 배웁니다.  
  
-   [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 테이블 형식 모델 프로젝트를 새로 만드는 방법  
  
-   SQL Server 관계형 데이터베이스의 데이터를 테이블 형식 모델 프로젝트로 가져오는 방법  
  
-   모델의 테이블 간에 관계를 만들고 관리하는 방법  
  
-   사용자가 모델 데이터를 분석하는 데 도움을 주는 계산, 측정값 및 핵심 성과 지표를 만들고 관리하는 방법  
  
-   비즈니스 및 애플리케이션별 뷰포인트를 통해 사용자가 모델 데이터를 쉽게 탐색할 수 있도록 도움을 주는 큐브 뷰와 계층을 만들고 관리하는 방법  
  
-   다른 파티션과 독립적으로 처리할 수 있도록 테이블 데이터를 더 작은 논리적 부분으로 나누는 파티션을 만드는 방법  
  
-   사용자 멤버 기반 역할을 만들어 모델 개체 및 데이터를 보호하는 방법  
  
-   테이블 형식 모델을 테이블 형식 모드로 실행 중인 Analysis Services의 샌드박스 또는 프로덕션 인스턴스에 배포하는 방법  
  
## <a name="tutorial-scenario"></a>자습서 시나리오  
 이 자습서는 가상 회사인 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]를 기반으로 합니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 는 북미, 유럽 및 아시아 시장에서 금속 및 합성 소재 자전거를 생산하고 판매하는 대규모 다국적 제조 회사입니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]의 본사는 워싱턴 주 보셀에 위치하고 있으며 직원 수는 500명입니다. 또한 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]는 판매 시장에 전반에 걸쳐 몇몇 지역에 영업 팀을 운영하고 있습니다.  
  
 영업과 마케팅 팀 및 경영 관리에 필요한 데이터 분석을 지원하기 위해 사용자가 AdventureWorksDW 예제 데이터베이스의 인터넷 매출 데이터를 분석할 수 있도록 테이블 형식 모델을 만들려고 합니다.  
  
 자습서를 완료하고 Adventure Works Internet Sales 테이블 형식 모델을 완성하려면 여러 단원을 완료해야 합니다. 각 단원 내에는 많은 태스크가 포함되어 있으며 단원을 완료하려면 각 태스크를 순서대로 완료해야 합니다. 특정 단원에는 비슷한 결과를 생성하는 여러 태스크가 포함되어 있지만 태스크를 완료하는 방법은 조금씩 다릅니다. 이는 특정 태스크를 완료하는 방법에는 여러 가지가 있음을 보여 주고 이전 태스크에서 배운 기술을 사용해 보도록 하기 위해서입니다.  
  
 단원의 목적은 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에 포함된 여러 가지 기능을 사용하여 메모리 내 모드로 실행되는 기본 테이블 형식 모델을 제작하는 과정을 안내하는 데 있습니다. 각 단원은 이전 단원에 기반을 두고 있으므로 단원을 순서대로 완료해야 합니다. 단원을 모두 완료하면 Adventure Works Internet Sales 예제 테이블 형식 모델이 만들어져 Analysis Services 서버에 배포되어 있을 것입니다.  
  
> [!NOTE]  
>  이 자습서에서는 배포한 테이블 형식 모델 데이터베이스를 SQL Server Management Studio를 사용하여 관리하거나 보고 클라이언트 애플리케이션을 사용하여 배포된 모델에 연결하여 모델 데이터를 탐색하는 과정을 안내하는 단원이나 정보는 제공하지 않습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 자습서를 완료하려면 다음 필수 구성 요소가 설치되어 있어야 합니다.  
  
-   테이블 형식 모드에서 실행 중인 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Analysis Services 인스턴스  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 을 참조하세요.  
  
-   AdventureWorksDW 예제 데이터베이스. 이 예제 데이터베이스에는 이 자습서를 완료하는 데 필요한 데이터가 포함되어 있습니다. 샘플 데이터베이스를 다운로드 하려면 [ https://go.microsoft.com/fwlink/?LinkID=335807 ](https://go.microsoft.com/fwlink/?LinkID=335807)합니다.  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 2003 이상(11단원의 Excel에서 분석 기능을 사용하는 데 필요)  
  
## <a name="lessons"></a>단원  
 이 자습서에는 다음 단원이 포함되어 있습니다.  
  
|단원|소요되는 예상 시간|  
|------------|--------------------------------|  
|[1단원: 새 테이블 형식 모델 프로젝트 만들기](lesson-1-create-a-new-tabular-model-project.md)|10분|  
|[2단원: 데이터 추가](lesson-2-add-data.md)|20분|  
|[3단원: 열 이름 바꾸기](rename-columns.md)|20분|  
|[4단원: 날짜 테이블로 표시](lesson-3-mark-as-date-table.md)|3분|  
|[5단원: 관계 만들기](lesson-4-create-relationships.md)|10분|  
|[6단원: 계산된 열 만들기](lesson-5-create-calculated-columns.md)|15분|  
|[7단원: 측정값 만들기](lesson-6-create-measures.md)|30분|  
|[8단원: 핵심 성과 지표 만들기](lesson-7-create-key-performance-indicators.md)|15분|  
|[9 단원: 큐브 뷰 만들기](lesson-8-create-perspectives.md)|5분|  
|[10 단원: 계층 만들기](lesson-9-create-hierarchies.md)|20분|  
|[11 단원: 파티션 만들기](lesson-10-create-partitions.md)|15분|  
|[12 단원: 역할 만들기](lesson-11-create-roles.md)|15분|  
|[단원 13: Excel에서 분석](lesson-12-analyze-in-excel.md)|20분|  
|[단원 14: Deploy](lesson-13-deploy.md)|5분|  
  
## <a name="supplemental-lessons"></a>추가 단원  
 이 자습서에는 [추가 단원](../tutorials/supplemental-lessons.md)도 포함되어 있습니다. 이 섹션의 항목은 자습서를 완료하기 위한 필수 항목은 아니지만 고급 테이블 형식 모델 제작 기능을 더 잘 이해하는 데 유용할 수 있습니다.  
  
 이 자습서에는 다음 추가 단원이 포함되어 있습니다.  
  
|단원|소요되는 예상 시간|  
|------------|--------------------------------|  
|[행 필터를 사용하여 동적 보안 구현](../tutorials/implement-dynamic-security-by-using-row-filters.md)|30분|  
|[Power View 보고서에 대 한 보고 속성 구성](supplemental-lesson-configure-reporting-properties-for-power-view-reports.md)Power View 보고서에 대 한 보고 속성 구성|30분|  
  
## <a name="next-step"></a>다음 단계  
 자습서를 시작 하려면 첫 번째 단원으로 이동 합니다. [1단원: 새 테이블 형식 모델 프로젝트를 만들](lesson-1-create-a-new-tabular-model-project.md)합니다.  
  
  
