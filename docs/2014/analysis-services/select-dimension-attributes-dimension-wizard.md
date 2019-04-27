---
title: 차원 특성 (차원 마법사)를 선택 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7abb4560696dba21512066a7ff0ba3153ae2319a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748095"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>차원 특성 선택(차원 마법사)
  **차원 특성 선택** 페이지를 사용하여 차원에 대해 만들 특성을 선택하고 수정할 수 있습니다.  
  
> [!NOTE]  
>  열 값을 읽을 수 없으면 마법사 창을 최대화하고 값을 읽을 수 있을 때까지 각 열 머리글의 너비를 변경하십시오.  
  
 **차원 마법사를 열려면**  
  
-   [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**에서 **프로젝트의** 차원 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 차원**을 클릭합니다.  
  
## <a name="options"></a>변수  
 (확인란이 있는 열)  
 차원에 특성을 포함시키려면 선택합니다.  
  
 특정 특성을 포함시키려면 해당 특성의 확인란을 선택합니다.  
  
 모든 특성을 포함시키려면 열 머리글의 확인란을 선택합니다.  
  
> [!NOTE]  
>  키 특성의 확인란은 선택 취소할 수 없습니다.  
  
 **특성 이름**  
 사용 가능한 특성을 나열합니다.  
  
 특성의 이름을 변경하려면 특성 이름을 클릭하고 특성의 새 이름을 입력합니다.  
  
 **검색 사용**  
 최종 사용자가 특성을 찾아보고 필터링할 수 있게 하려면 선택합니다. 키 특성에 대해**찾아보기 사용** 을 선택해야 합니다. 키가 아닌 특성의 경우에는 **찾아보기 사용** 이 기본적으로 선택되어 있지 않습니다. 따라서 키가 아닌 특성은 멤버 속성으로만 표시됩니다.  
  
 대부분의 경우 `AttributeHierarchyEnabled` 속성을 `True` 또는 `False`로 설정하여 특성을 찾아보기에 사용하거나 사용하지 못하게 합니다. 그러나 다음 세 가지 사례에서 마법사는 다른 설정을 사용합니다.  
  
|사례|설정|  
|----------|--------------|  
|차원에 부모-자식 계층이 포함되고 **찾아보기 사용** 이 선택되지 않은 경우|마법사는 `AttributeHierarchyEnabled` 속성을 `True`로 두고, 키 특성에 대해 `AttributeHierarchyVisible` 특성을 `False`로 설정합니다.|  
|차원 내의 테이블에 차원에 없는 테이블에 대한 외래 키가 포함된 경우|마법사는 외래 키를 포함되는 특성으로 선택하지만 **찾아보기 사용**은 선택하지 않습니다. 이 설정을 유지하면 특성의 `AttributeHiearchyEnabled` 속성이 `True`로 설정되고 `AttributeHieararchyVisible` 속성이 `False`로 설정됩니다.|  
|null이 허용되는 외래 키 열을 통해 도달하는 눈송이 테이블이 차원에 포함된 경우<br /><br /> 및<br /><br /> 눈송이 테이블의 키를 기반으로 한 특성에 대해 찾아보기 사용이 선택되지 않은 경우|마법사는 `AttributeHiearchyEnabled` 속성이 `True`로 설정되고 `AttributeHieararchyVisible` 속성이 `False`로 설정된 새 특성을 만듭니다.|  
  
 **특성 유형**  
 (옵션) 특성의 유형을 설정합니다. 기본값은 **Regular**입니다. 특성 유형은 특성에 포함할 정보에 대한 지침을 클라이언트 애플리케이션에 제공합니다.  
  
## <a name="see-also"></a>관련 항목  
 [차원 마법사 F1 도움말](dimension-wizard-f1-help.md)   
 [차원 &#40;Analysis Services-다차원 데이터&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [다차원 모델의 차원](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
