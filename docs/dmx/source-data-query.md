---
title: "&lt;원본 데이터 쿼리와&gt; | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords:
- data sources [DMX]
- predictions [DMX]
- source data query element
- queries [DMX], source data
- external data access [DMX]
- <source data query> element
- training mining models
ms.assetid: 9dce5e37-1354-4d28-87c2-f9c419cb5b09
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 7e950bdcc5b6e2b683ac1a63a79353c97c88dec1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="ltsource-data-querygt"></a>&lt;원본 데이터 쿼리&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  데이터 마이닝 모델을 학습 하려면 마이닝 모델에서 예측을 만드는 외부에 있는 데이터에 액세스 해야는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다. 사용 된 \<원본 데이터 쿼리와 > 절에 확장 DMX (Data Mining)이 외부 데이터를 정의 합니다. [INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md), [SELECT FROM &#60; 모델 &#62; 예측 조인 &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md), 및 [선택 FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) 모든 문을 사용 하 여  **\<원본 데이터 쿼리와 >**합니다.  
  
## <a name="query-types"></a>쿼리 유형  
 일반적으로 원본 데이터를 지정하는 3가지 방법은 다음과 같습니다.  
  
 [OPENQUERY &#40; DMX &#41;](../dmx/source-data-query-openquery.md)  
 이 문은 기존 데이터 원본을 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 외부에 있는 데이터를 쿼리합니다.  
  
 반면 **OPENQUERY** 와 유사한 기능을 **OPENROWSET**, **OPENQUERY** 다음과 같은 이점을 제공 합니다.  
  
-   DMX 쿼리는 훨씬 쉽게 작성할 수 **OPENQUERY**합니다. 쿼리를 작성할 때마다 새 연결 문자열을 만드는 대신 데이터 원본에 있는 기존 연결 문자열을 사용할 수 있습니다. 데이터 원본 개체는 개별 사용자의 데이터 액세스를 제어할 수도 있습니다.  
  
-   관리자는 서버의 데이터에 액세스하는 방법을 더욱 자세하게 제어할 수 있습니다. 예를 들어 관리자는 서버에 로드되는 공급자 및 액세스할 수 있는 외부 데이터를 관리할 수 있습니다.  
  
 [OPENROWSET&#40; DMX &#41;](../dmx/source-data-query-openrowset.md)  
 이 문은 기존 데이터 원본을 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 외부에 있는 데이터를 쿼리합니다.  
  
 [셰이프 &#40; DMX &#41;](../dmx/source-data-query-shape.md)  
 이 문은 여러 데이터 원본을 쿼리하여 중첩 테이블을 만듭니다. 사용 하 여 **셰이프**, 단일 계층적 테이블에 여러 원본의 데이터를 결합할 수 있습니다. 이를 통해 테이블 안에 테이블을 포함하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 테이블 중첩 기능을 사용할 수 있습니다.  
  
 원본 데이터를 지정하는 경우 다음과 같은 옵션도 사용할 수 있습니다.  
  
-   유효한 DMX 문  
  
-   유효한 MDX(Multidimensional Expressions) 문  
  
-   저장 프로시저를 반환하는 테이블  
  
-   XMLA(XML for Analysis) 행 집합  
  
-   행 집합 매개 변수  
  
## <a name="see-also"></a>관련 항목:  
 [Data Mining Extensions &#40; DMX &#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40; DMX &#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [중첩된 테이블 &#40; Analysis Services-데이터 마이닝 &#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
