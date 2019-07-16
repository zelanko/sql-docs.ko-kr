---
title: '&lt;원본 데이터 쿼리와&gt; | Microsoft Docs'
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 83dbe0c2ea6eb066f208223acd2c6062f964fcf3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938084"
---
# <a name="ltsource-data-querygt"></a>&lt;원본 데이터 쿼리&gt;
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  데이터 마이닝 모델을 학습 하 고 마이닝 모델에서 예측을 만들 하려면 외부에 있는 데이터에 액세스 해야 합니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스입니다. 사용할는 \<원본 데이터 쿼리와 > 절에 확장 DMX (Data Mining)이 외부 데이터를 정의 합니다. [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md)하십시오 [SELECT FROM &#60;모델&#62; PREDICTION JOIN &#40;DMX&#41;](../dmx/select-from-model-prediction-join-dmx.md), 및 [선택 FROM NATURAL PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) 사용 하 여 모든 문과  **\<원본 데이터 쿼리와 >** 합니다.  
  
## <a name="query-types"></a>쿼리 유형  
 일반적으로 원본 데이터를 지정하는 3가지 방법은 다음과 같습니다.  
  
 [OPENQUERY &#40;DMX&#41;](../dmx/source-data-query-openquery.md)  
 이 문은 기존 데이터 원본을 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 외부에 있는 데이터를 쿼리합니다.  
  
 하는 동안 **OPENQUERY** 함수를 비슷합니다 **OPENROWSET**를 **OPENQUERY** 다음과 같은 이점이 있습니다.  
  
-   DMX 쿼리를 작성 하기가 훨씬 쉽습니다 **OPENQUERY**합니다. 쿼리를 작성할 때마다 새 연결 문자열을 만드는 대신 데이터 원본에 있는 기존 연결 문자열을 사용할 수 있습니다. 데이터 원본 개체는 개별 사용자의 데이터 액세스를 제어할 수도 있습니다.  
  
-   관리자는 서버의 데이터에 액세스하는 방법을 더욱 자세하게 제어할 수 있습니다. 예를 들어 관리자는 서버에 로드되는 공급자 및 액세스할 수 있는 외부 데이터를 관리할 수 있습니다.  
  
 [OPENROWSET &#40;DMX&#41;](../dmx/source-data-query-openrowset.md)  
 이 문은 기존 데이터 원본을 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 외부에 있는 데이터를 쿼리합니다.  
  
 [도형 &#40;DMX&#41;](../dmx/source-data-query-shape.md)  
 이 문은 여러 데이터 원본을 쿼리하여 중첩 테이블을 만듭니다. 사용 하 여 **셰이프**, 단일 계층적 테이블에 여러 원본의 데이터를 결합할 수 있습니다. 이를 통해 테이블 안에 테이블을 포함하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 테이블 중첩 기능을 사용할 수 있습니다.  
  
 원본 데이터를 지정하는 경우 다음과 같은 옵션도 사용할 수 있습니다.  
  
-   유효한 DMX 문  
  
-   유효한 MDX(Multidimensional Expressions) 문  
  
-   저장 프로시저를 반환하는 테이블  
  
-   XMLA(XML for Analysis) 행 집합  
  
-   행 집합 매개 변수  
  
## <a name="see-also"></a>관련 항목  
 [Data Mining Extensions &#40;DMX&#41; 데이터 조작 문](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining Extensions &#40;DMX&#41; 문 참조](../dmx/data-mining-extensions-dmx-statements.md)   
 [중첩 테이블 &#40;Analysis Services-데이터 마이닝&#41;](../analysis-services/data-mining/nested-tables-analysis-services-data-mining.md)  
  
  
