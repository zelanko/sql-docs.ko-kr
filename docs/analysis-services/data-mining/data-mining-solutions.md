---
title: "데이터 마이닝 솔루션 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], about data mining
- data mining [Analysis Services], development
ms.assetid: 84f6548d-ebb0-4e10-9b29-66253fa0a04a
caps.latest.revision: "64"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7d296518a6a41af88d194e8cb23b2abc371b497b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-solutions"></a>데이터 마이닝 솔루션
  데이터 마이닝 솔루션은 하나 이상의 데이터 마이닝 프로젝트가 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 솔루션입니다.  
  
 이 섹션의 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 사용하여 통합 데이터 마이닝 솔루션을 디자인하고 구현하는 방법에 대해 설명합니다. 데이터 마이닝 디자인 프로세스와 관련 도구에 대한 개요는 [Data Mining Concepts](../../analysis-services/data-mining/data-mining-concepts.md)를 참조하십시오.  
  
 데이터 마이닝에 유용한 추가 프로젝트 형식에 대한 자세한 내용은 [데이터 마이닝 솔루션 관련 프로젝트](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)를 참조하세요.  
  
 [관계형 마이닝 모델과 다차원 솔루션](#bkmk_RelMD)  
  
 [데이터 마이닝 솔루션 배포](#bkmk_Deploy)  
  
 [솔루션 연습](#bkmk_Walkthru)  
  
##  <a name="bkmk_RelMD"></a>관계형 마이닝 모델과 다차원 솔루션  
 데이터 마이닝 솔루션은 다차원 데이터(즉, 기존 큐브)나 순수 관계형 데이터(예: 데이터 웨어하우스의 테이블 및 뷰) 또는 텍스트 파일, Excel 통합 문서 또는 기타 외부 데이터 원본을 기반으로 할 수 있습니다.  
  
-   기존 다차원 데이터베이스 솔루션 내에 데이터 마이닝 개체를 만들 수 있습니다.  
  
     일반적으로 이미 만든 큐브를 데이터 원본으로 사용하여 데이터 마이닝을 수행하려는 경우에 이와 같은 솔루션을 만듭니다. 큐브를 기반으로 하는 모델을 이동 및 백업할 때는 큐브도 이동하거나 복사해야 합니다.  
  
-   데이터 마이닝 개체(지원되는 데이터 원본 및 데이터 원본 뷰 포함)만 포함하고 관계형 데이터 원본만 사용하는 데이터 마이닝 솔루션을 만들 수 있습니다.  
  
     이는 일반적으로 관계형 데이터 원본에 대해 처리 및 쿼리가 가장 빠르기 때문에 데이터 마이닝 모델을 만들 때 가장 선호되는 방법입니다. 또한 EXPORT 및 IMPORT 명령을 사용하여 서버 간에 모델을 쉽게 이동 및 백업할 수 있습니다.  
  
##  <a name="bkmk_Deploy"></a> 데이터 마이닝 솔루션 배포  
 솔루션을 배포하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스는 다차원 개체 및 데이터 마이닝 개체를 지원하는 모드에서 실행되고 있어야 합니다. 즉 데이터 마이닝 개체를 테이블 형식 모델 또는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터를 호스팅하는 인스턴스에 배포할 수는 없습니다.  
  
 따라서 Visual Studio에서 데이터 마이닝 솔루션을 만드는 경우 반드시 **Analysis Services 다차원 및 데이터 마이닝 프로젝트**템플릿을 사용하십시오.  
  
 솔루션을 배포하면 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 솔루션 파일과 같은 이름의 데이터베이스에 데이터 마이닝에 사용되는 개체가 만들어집니다.  
  
 관계형 솔루션 및 다차원 솔루션을 배포하는 방법에 대한 자세한 내용은 [데이터 마이닝 솔루션 배포](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)를 참조하세요.  
  
##  <a name="bkmk_Walkthru"></a> 솔루션 연습  
 데이터 마이닝 마법사를 사용하여 데이터 마이닝 솔루션을 만드는 방법에 대해 간략하게 설명합니다.  
  
 [관계형 마이닝 구조 만들기](../../analysis-services/data-mining/create-a-relational-mining-structure.md)  
 관계형 데이터, 텍스트 파일 및 기타 데이터 원본 뷰에 통합될 수 있는 원본에서 마이닝 구조를 만듭니다.  
  
 [OLAP 마이닝 구조 만들기](../../analysis-services/data-mining/create-an-olap-mining-structure.md)  
 OLAP 큐브의 데이터를 기반으로 하는 마이닝 구조를 만듭니다. OLAP 데이터에서 만든 모델을 데이터 마이닝 차원으로 저장하거나 데이터 및 모델 집합을 새 큐브로 저장할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 마이닝 프로젝트](../../analysis-services/data-mining/data-mining-projects.md)  
  
 [데이터 마이닝 개체 처리](../../analysis-services/data-mining/processing-data-mining-objects.md)  
  
 [데이터 마이닝 솔루션 관련 프로젝트](../../analysis-services/data-mining/related-projects-for-data-mining-solutions.md)  
  
 [데이터 마이닝 솔루션 배포](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)  
  
## <a name="related-tasks-and-topics"></a>관련 태스크 및 항목  
 데이터 원본 및 마이닝 구조를 포함하여 기본 데이터 마이닝 솔루션을 만든 후에는 새 모델을 추가하고, 모델을 테스트 및 비교하고, 예측을 만들고, 데이터 하위 집합을 시험하여 솔루션을 빌드할 수 있습니다.  
  
 자세한 내용은 다음 링크를 참조하십시오.  
  
|태스크|항목|  
|-----------|------------|  
|만든 모델을 테스트하고, 학습 데이터의 품질에 대한 유효성을 검사하고, 데이터 마이닝 모델의 정확도를 나타내는 차트를 만듭니다.|[테스트 및 유효성 검사&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)|  
|구조 및 관련 모델을 데이터로 채워 모델을 학습합니다. 모델을 새 데이터로 업데이트 및 확장합니다.|[데이터 마이닝 개체 처리](../../analysis-services/data-mining/processing-data-mining-objects.md)|  
|학습 데이터에 필터를 적용하거나, 다른 알고리즘을 선택하거나, 고급 알고리즘 매개 변수를 설정하여 마이닝 모델을 사용자 지정합니다.|[마이닝 모델 및 구조 사용자 지정](../../analysis-services/data-mining/customize-mining-models-and-structure.md)|  
|모델을 학습하는 데 사용되는 데이터에 필터를 적용하여 마이닝 모델을 사용자 지정합니다.|[구조에 마이닝 모델 추가&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/add-mining-models-to-a-structure-analysis-services-data-mining.md)|  
|데이터 마이닝 솔루션을 업데이트하고 관리합니다.|Link TBD|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 자습서&#40;Analysis Services&#41;](../../analysis-services/data-mining-tutorials-analysis-services.md)  
  
  
