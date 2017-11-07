---
title: "Analysis Services 자습서 시나리오 | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 933a07504d0237d67becb2d98e1f5271548cb14a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-tutorial-scenario"></a>Analysis Services Tutorial 시나리오
이 자습서는 가상 회사인 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]를 기반으로 합니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 는 북미, 유럽 및 아시아 시장에서 금속 및 합성 소재 자전거를 생산하고 판매하는 대규모 다국적 제조 회사입니다. [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 의 본사는 워싱턴 주 보셀에 위치하고 있으며 직원 수는 500명입니다. 또한 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 는 판매 시장에 전반에 걸쳐 몇몇 지역에 영업 팀을 운영하고 있습니다.  
  
[!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 는 최근에 멕시코에 위치한 소규모 제조업체인 Importadores Neptuno를 인수했습니다. Importadores Neptuno는 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 제품 라인에서 중요한 여러 가지 하위 구성 요소를 제조합니다. 이러한 하위 구성 요소는 Bothell로 운송된 후 최종 제품 조립에 사용됩니다. 2005년에 Importadores Neptuno는 여행용 자전거 제품 그룹의 유일한 제조업체이자 유통업체가 되었습니다.  
  
회계 연도를 성공적으로 마무리한 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 는 우수 고객 중심으로 광고를 제공해 시장 점유율을 높이고 외부 웹 사이트를 통해 제품 사용 가능성을 높이며 생산 비용을 절감하여 판매 비용을 낮추려고 합니다.  
  
## <a name="current-analysis-environment"></a>현재 분석 환경  
판매와 마케팅 팀 및 경영 관리에 필요한 데이터 분석을 지원하기 위해 이 회사는 현재 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 데이터베이스의 트랜잭션 데이터 및 판매 할당량과 같은 스프레드시트의 비트랜잭션 정보를 가져오고 이 정보를 **AdventureWorksDW2012** 관계형 데이터 웨어하우스로 통합합니다. 그러나 관계형 데이터 웨어하우스에는 다음과 같은 문제가 있습니다.  
  
-   보고서가 정적입니다. 사용자는 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 피벗 테이블을 사용하여 수행할 수 있는 작업처럼 자세한 정보를 얻기 위해 보고서의 데이터를 대화형으로 탐색할 수 없습니다. 많은 사용자에게는 미리 정의된 보고서의 기존 세트로 충분하지만 보다 고급 사용자에게는 대화형 쿼리와 특수한 보고서 작성을 위해 데이터베이스에 대한 직접 쿼리 액세스가 필요합니다. 그러나 **AdventureWorksDW2012** 데이터베이스의 복잡성 때문에 사용자가 효과적인 쿼리 작성 방법에 익숙해지는 데 상당한 시간이 필요합니다.  
  
-   쿼리 성능은 크게 다릅니다. 예를 들어 일부 쿼리는 몇 초만에 빠르게 결과를 반환하지만 다른 쿼리는 결과 반환에 몇 분이 걸립니다.  
  
-   집계 테이블은 관리하기가 어렵습니다. [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 의 데이터 웨어하우스 팀은 쿼리 응답 시간을 향상시키기 위해 **AdventureWorksDW2012** 데이터베이스에 몇 개의 집계 테이블을 작성했습니다. 예를 들어 월간 판매를 요약하는 테이블을 작성했습니다. 그러나 이러한 집계 테이블은 쿼리 성능을 크게 향상시키는 반면 시간에 따라 테이블을 유지하기 위해 구축한 인프라는 오류가 쉽게 발생합니다.  
  
-   복잡한 계산 논리가 보고서 정의에 포함되어 있고 보고서 간에 공유되기가 어렵습니다. 이 비즈니스 논리는 각 보고서마다 별도로 생성되므로 보고서 간 요약 정보가 다를 수도 있습니다. 따라서 경영진의 데이터 웨어하우스 보고서에 대한 신뢰성이 제한적이었습니다.  
  
-   서로 다른 비즈니스 단위에 속한 사용자는 서로 다른 데이터 보기에 관심을 갖습니다. 그룹과 관련이 없는 데이터 요소는 각 그룹에게 혼란을 주거나 방해가 됩니다.  
  
-   계산 논리는 특히 특수 보고서를 필요로 하는 사용자에게 문제가 됩니다. 이러한 사용자는 보고서마다 계산 논리를 별도로 정의해야 하므로 계산 논리 정의 방법을 중앙 집중식으로 제어할 수 없습니다. 예를 들어 사용자가 이동 평균법 같은 기본 통계 기법을 사용해야 함을 알고 있어도 그러한 계산 구성 방법을 모를 경우에는 이러한 기법을 사용하지 않습니다.  
  
-   관련 정보 집합을 결합하기가 어렵습니다. 판매 및 판매 할당량과 같은 두 가지 관련 정보 집합을 결합한 특수화된 쿼리는 비즈니스 사용자가 구성하기 어렵습니다. 해당 쿼리로 인해 데이터베이스 사용량이 크게 증가되므로 회사에서 사용자가 데이터 웨어하우스 팀의 주제 간 공통 영역 데이터 집합을 요청해야 합니다. 따라서 여러 주제 영역의 데이터를 결합하는 미리 정의된 보고서 수는 매우 적습니다. 또한 사용자는 이러한 보고서의 복잡성으로 인해 해당 보고서를 수정하려 하지 않습니다.  
  
-   보고서는 주로 미국의 비즈니스 정보를 기준으로 합니다. 미국이 아닌 지사의 사용자는 이 기준에 만족하지 못하고 다른 통화와 다른 언어로 보고서를 보려 합니다.  
  
-   정보는 감사하기가 어렵습니다. 재무 부서에서는 대량 쿼리할 데이터 원본으로 현재 **AdventureWorksDW2012** 데이터베이스만 사용합니다. 데이터를 개별 스프레드시트에 다운로드하고 데이터 준비와 스프레드시트 조작에 상당한 시간을 소비합니다. 따라서 회사 전체에서 기업 재무 보고서를 준비, 감사 및 관리하기가 어렵습니다.  
  
## <a name="the-solution"></a>솔루션  
최근 데이터 웨어하우스 팀은 현재 분석 시스템의 설계를 검토했습니다. 검토에는 현재의 문제와 향후 요구 사항에 대한 차이점 분석이 포함됩니다. 데이터 웨어하우스 팀은 **AdventureWorksDW2012** 데이터베이스가 일치된 차원과 대리 키가 있는 잘 설계된 차원 데이터베이스임을 확인했습니다. 일치된 차원이 제공되므로 시간 차원이나 제품 차원과 같은 여러 데이터 마트에 차원을 사용할 수 있습니다. 대리 키는 차원과 팩트 테이블을 연결하는 인공 키로 고유성을 확보하고 성능을 향상시키는 데 사용됩니다. 또한 데이터 웨어하우스 팀은 현재 **AdventureWorksDW2012** 데이터베이스의 기준 테이블을 로드하고 관리하는 데 큰 문제가 없음을 확인했습니다. 따라서 이 팀은 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 를 사용하여 다음을 수행하도록 결정했습니다.  
  
-   분석적인 분석 및 보고를 위해 공통 메타데이터 계층을 통해 통합된 데이터 액세스를 제공합니다.  
  
-   사용자의 데이터 보기를 단순화하여 대화형 미리 정의된 쿼리 및 미리 정의된 보고서의 개발 속도를 높입니다.  
  
-   여러 주제 영역의 데이터를 결합하는 쿼리를 올바르게 구성합니다.  
  
-   집계를 관리합니다.  
  
-   복잡한 계산을 저장하고 다시 사용합니다.  
  
-   미국 외부에 있는 비즈니스 사용자에게 지역화된 경험을 제공합니다.  
  
Analysis Services 자습서의 단원에서는 이러한 모든 목표에 맞는 큐브 데이터베이스를 작성하는 데 필요한 지침을 제공합니다. 시작하려면 첫 번째 단원인 [1단원: 새 테이블 형식 모델 프로젝트를 만들기](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)로 이동하세요.  
  
## <a name="see-also"></a>참고 항목  
[다차원 모델링&#40;Adventure Works 자습서&#41;](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
  
  

