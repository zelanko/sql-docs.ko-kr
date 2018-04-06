---
title: 데이터 마이닝 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
ms.assetid: b1c912da-72f6-4d96-89c8-55a2c4f19e88
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 6ccc1faad28913133cc0870899f20b443fc28eb7
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="data-mining-ssas"></a>데이터 마이닝(SSAS)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지났습니다 예측 분석에서 선두 2000 버전의 데이터 마이닝을 제공 하 여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝의 조합은 데이터 정리 및 준비, 기계 학습 및 보고를 포함하는 예측 분석에 대한 통합된 플랫폼을 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝에는 EM 및 K-means 클러스터링 모델, 신경망, 로지스틱 회귀 분석 및 선형 회귀, 의사 결정 트리 및 naive bayes 분류자를 비롯하여 여러 표준 알고리즘이 포함됩니다. 모든 모델은 모델을 개발하고 구체화하고 평가할 수 있도록 시각화를 통합했습니다.  비즈니스 인텔리전스 솔루션에 데이터 마이닝을 통합하면 복잡한 문제에 대한 지능형 의사 결정을 수행할 수 있습니다.  
  
## <a name="benefits-of-data-mining"></a>데이터 마이닝의 장점  
 데이터 마이닝(예측 분석 및 기계 학습이라고도 함)은 다양한 연구 결과를 기반으로 하는 통계 원칙을 사용하여 데이터에서 패턴을 검색합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 데이터 마이닝 알고리즘을 데이터에 적용하면 추세를 예측하고 패턴을 식별하여 규칙과 권장 사항을 만들 수 있으며 복잡한 데이터 집합에서 이벤트의 시퀀스를 분석하여 새로운 통찰력을 얻을 수 있습니다.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 데이터 마이닝은 강력하고도 사용하기 쉬우며, 많은 사용자들이 분석 및 보고에 자주 사용하는 도구와 통합되어 있습니다.  
  
## <a name="key-data-mining-features"></a>주요 데이터 마이닝 기능  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝은 통합 데이터 마이닝 솔루션을 지원하여 다음과 같은 기능을 제공합니다.  
  
-   여러 데이터 원본: 데이터 마이닝을 위해 스프레드시트 및 텍스트 파일을 포함하여 모든 테이블 형식 데이터 원본을 사용할 수 있습니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 만든 OLAP 큐브를 쉽게 마이닝할 수도 있습니다. 그러나 메모리 내 데이터베이스에서 데이터를 사용할 수 없습니다.  
  
-   통합 데이터 정리, 데이터 관리 및 보고: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에서 데이터 프로파일링 및 정리를 위한 도구를 제공합니다. 모델링 준비 과정에서 데이터 정리를 위한 ETL 프로세스를 작성할 수 있으며, ssISnoversion은 쉽게 모델을 다시 학습하고 업데이트할 수도 있습니다.  
  
-   사용자 지정 가능한 다양한 알고리즘: 클러스터링, 신경망 및 의사 결정 트리와 같은 알고리즘 제공 외에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝은 고유의 사용자 지정 플러그 인 알고리즘의 개발을 지원합니다.  
  
-   모델 테스트 인프라: 교차 유효성 검사, 분류표, 리프트 차트 및 산점도와 같은 중요한 통계 도구를 사용하여 모델과 데이터 집합을 테스트합니다. 테스트 및 학습 집합을 간편하게 만들고 관리합니다.  
  
-   쿼리 및 드릴스루: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝은 예측 쿼리를 응용 프로그램에 통합하기 위한 DMX 언어를 제공합니다. 모델에서 자세한 통계 및 패턴을 검색하고 사례 데이터로 드릴스루할 수도 있습니다.  
  
-   클라이언트 도구: SQL Server에서 제공하는 개발 및 디자인 스튜디오 외에도 Excel용 데이터 마이닝 추가 기능을 사용하여 모델을 만들고 쿼리하며 찾아볼 수 있습니다. 또한 웹 서비스를 포함한 사용자 지정 클라이언트를 만듭니다.  
  
-   스크립팅 언어 지원 및 관리되는 API: 모든 데이터 마이닝 개체는 완전히 프로그래밍할 수 있습니다. 스크립팅은 MDX, XMLA, 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에 대한 PowerShell 확장을 통해 가능합니다. 빠른 쿼리 및 스크립팅을 위해 DMX(Data Mining Extensions) 언어를 사용합니다.  
  
-   보안 및 배포: 모델 및 구조 데이터의 드릴스루에 대한 별도의 사용 권한을 포함하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 통해 역할 기반 보안을 제공합니다. 사용자가 패턴에 액세스하거나 예측을 수행할 수 있도록 다른 서버에 모델을 간편하게 배포  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 마이닝의 주요 기능 및 관련 태스크를 소개합니다.  
  
-   [데이터 마이닝 개념](../../analysis-services/data-mining/data-mining-concepts.md)  
  
-   [데이터 마이닝 알고리즘&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)  
  
-   [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
-   [마이닝 모델&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
-   [테스트 및 유효성 검사&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
-   [데이터 마이닝 쿼리](../../analysis-services/data-mining/data-mining-queries.md)  
  
-   [데이터 마이닝 솔루션](../../analysis-services/data-mining/data-mining-solutions.md)  
  
-   [데이터 마이닝 도구](../../analysis-services/data-mining/data-mining-tools.md)  
  
-   [데이터 마이닝 아키텍처](../../analysis-services/data-mining/data-mining-architecture.md)  
  
-   [보안 개요&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/security-overview-data-mining.md)  
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)  
  
  
