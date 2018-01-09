---
title: "SQL Server Management Studio에서 DMX 쿼리 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- templates [Analysis Services], queries
- SQL Server Management Studio [Analysis Services], DMX queries
- predictions [Analysis Services], DMX prediction queries
- predictions [DMX]
- prediction queries [DMX]
- queries [DMX], prediction queries
- mining models [Analysis Services], DMX
ms.assetid: 568ce40a-1f53-47eb-8c79-14347cdfde83
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: edb3f0ab17369a4a1df4a69d80e07bfa1ff84012
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="create-a-dmx-query-in-sql-server-management-studio"></a>SQL Server Management Studio에서 DMX 쿼리 만들기
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예측 쿼리, 내용 쿼리 및 마이닝 모델과 마이닝 구조에 대 한 데이터 정의 쿼리를 만드는 데 도움이 되는 기능 집합을 제공 합니다.  
  
-   그래픽 예측 쿼리 작성기는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 예측 쿼리를 작성하고 데이터 집합을 모델에 매핑하는 프로세스를 간소화하는 데 사용됩니다.  
  
-   템플릿 탐색기에서 제공되는 쿼리 템플릿을 사용하면 다양한 유형의 예측 쿼리를 비롯하여 많은 종류의 DMX 쿼리를 빠르게 만들 수 있습니다. 내용 쿼리, 중첩된 데이터 집합에 사용되는 쿼리, 마이닝 구조에서 사례를 반환하는 쿼리 및 데이터 정의 쿼리에 대한 템플릿이 제공됩니다.  
  
-   MDX 및 DMX 쿼리 창의 메타데이터 탐색기는 쿼리 작성기에 끌어 놓을 수 있는 사용 가능한 모델 및 구조 목록과 DMX 함수 목록을 제공합니다. 이 기능을 사용하면 입력하지 않고도 개체 이름을 즉시 가져올 수 있습니다.  
  
 이 항목에서는 메타데이터 탐색기 및 DMX 쿼리 편집기를 사용하여 DMX 쿼리를 작성하는 방법에 대해 설명합니다.  
  
##  <a name="BKMK_Templates"></a> DMX 쿼리 템플릿  
 기본 DMX 쿼리를 만들기 위한 템플릿은 템플릿 탐색기에서 찾아볼 수 있습니다. **DMX** 폴더에는 다음 범주로 나누어진 데이터 마이닝 템플릿이 포함되어 있습니다.  
  
-   **모델 콘텐츠**  
  
-   **모델 관리**  
  
-   **예측 쿼리**  
  
-   **구조 콘텐츠**  
  
 자주 실행하는 쿼리나 명령에 대한 사용자 지정 템플릿을 만들 수도 있습니다.  
  
## <a name="xmla-query-templates"></a>XMLA 쿼리 템플릿  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 XMLA 쿼리에 대한 템플릿도 제공합니다.  
  
 XMLA와 DMX를 사용하여 수행할 수 있는 쿼리 유형은 일부 중첩됩니다. 예를 들어 DMX 또는 데이터 마이닝 스키마 행 집합을 사용하여 몇 가지 모델 내용 쿼리를 만들 수 있지만 스키마 행 집합에 DMX 내용 쿼리에 노출되지 않는 정보가 포함되어 있는 경우도 있습니다.  
  
 DMX와 XMLA의 작업 처리 방식에는 몇 가지 중요한 차이점도 있습니다. 예를 들어 XMLA를 사용하여 전체 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 백업과 같은 관리 작업을 수행할 수 있지만 단일 마이닝 모델을 백업하려면 DMX에서 제공하는 간단한 명령인 [EXPORT&#40;DMX&#41;](../../dmx/export-dmx.md)를 사용하는 것이 보다 적절합니다.  
  
##  <a name="BKMK_Building_Queries"></a> DMX 쿼리 작성 및 실행  
  
#### <a name="open-a-new-dmx-query-window"></a>새 DMX 쿼리 창 열기  
  
1.  **에서** 새 쿼리 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 클릭한 다음 **새 Analysis Server DMX 쿼리**를 선택합니다.  
  
2.  **서버에 연결** 대화 상자가 나타나면 작업할 마이닝 모델이 포함된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스를 선택합니다.  
  
#### <a name="open-template-explorer"></a>템플릿 탐색기 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 **보기** 메뉴에서 **템플릿 탐색기**를 선택합니다.  
  
2.  **에 적용되는 템플릿을 트리 뷰로 보려면** Analysis Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]를 클릭합니다.  
  
#### <a name="apply-a-template-to-build-a-query"></a>쿼리를 작성할 템플릿을 적용합니다.  
  
-   적절한 쿼리 유형을 마우스 오른쪽 단추로 클릭하고 **열기**를 선택합니다.  
  
-   또는 템플릿을 쿼리 편집기로 끌어 옵니다.  
  
-   **쿼리**메뉴에서 **템플릿 매개 변수 값 지정** 옵션을 사용하여 쿼리 매개 변수를 채울 수도 있습니다.  
  
 템플릿에서 특정 쿼리 유형을 만드는 방법에 대한 예는 다음 항목을 참조하십시오.  
  
 [템플릿에서 단일 예측 쿼리 작성](../../analysis-services/data-mining/create-a-singleton-prediction-query-from-a-template.md)  
  
 [마이닝 모델에 내용 쿼리 만들기](../../analysis-services/data-mining/create-a-content-query-on-a-mining-model.md)  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 쿼리 도구](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [DMX&#40;Data Mining Extensions&#41; 참조](../../dmx/data-mining-extensions-dmx-reference.md)  
  
  
