---
title: 반 가산적 동작 정의 (비즈니스 인텔리전스 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.semiadditivememberdetection.f1
ms.assetid: e57080ba-ce96-40f8-bca7-6701d1725b3c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 161e2cb9dd9eeae4f2ed369b77ab0799ae12a33a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081999"
---
# <a name="define-semiadditive-behavior-business-intelligence-wizard"></a>반가산적 동작 정의(비즈니스 인텔리전스 마법사)
  
  **반가산적 동작 정의** 페이지를 사용하여 측정값에 대한 반가산적 동작을 설정 또는 해제할 수 있습니다. 반가산적 동작은 큐브에 포함된 측정값이 시간 차원에 대해 집계되는 방법을 결정합니다.  
  
> [!NOTE]  
>  표준 버전에서 제공되는 LastChild를 제외하고, 반가산적 동작은 비즈니스 인텔리전스 또는 엔터프라이즈 버전에서만 사용할 수 있습니다. 또한 반가산적 동작이 측정값에 대해서만 정의되고 차원에 대해서는 정의되지 않기 때문에 차원 디자이너에서 시작되거나 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 솔루션 탐색기에서 차원을 마우스 오른쪽 단추로 클릭하여 시작된 비즈니스 인텔리전스 마법사에는 이 페이지가 없습니다.  
  
## <a name="options"></a>옵션  
 **반 가산적 동작 해제**  
 큐브에 포함된 모든 측정값의 반가산적 동작을 해제합니다.  
  
 **마법사에서 반 가산적 멤버가 \<포함 된 차원 이름> account 차원을 검색 했습니다. 서버는 각 계정 유형에 지정 된 반 가산적 동작에 따라이 차원의 멤버를 집계 합니다.**  
 반가산적 멤버를 포함하는 계정 차원에 대한 반가산적 동작을 설정합니다. 이 옵션을 선택하면 계정 차원을 참조하는 측정값 그룹의 모든 측정값 집계 함수가 `ByAccount`로 설정됩니다.  
  
 계정 차원에 대한 자세한 내용은 [부모-자식 유형 차원의 재무 계정 만들기](multidimensional-models/database-dimensions-finance-account-of-parent-child-type.md)를 참조하세요.  
  
 **개별 측정값에 대한 반가산적 동작 정의**  
 반가산적 동작을 설정하고 특정 측정값에 대한 반가산적 집계 함수를 지정합니다. 이 집계 함수는 해당 측정값을 포함하는 측정값 그룹이 참조하는 모든 차원에 적용됩니다.  
  
 **측정값 그룹**  
 큐브에 포함된 측정값의 이름을 표시합니다.  
  
 **반가산적 함수**  
 선택한 측정값에 대한 집계 함수를 선택합니다. 다음 표에서는 사용 가능한 집계 함수를 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|**AverageOfChildren**|측정값의 자식 평균을 반환하여 집계됩니다.|  
|`ByAccount`|계정 차원에 지정된 특성의 계정 유형과 연결된 집계 함수에 의해 집계됩니다.|  
|`Count`|
  `Count` 함수를 사용하여 집계됩니다.|  
|`DistinctCount`|
  `DistinctCount` 함수를 사용하여 집계됩니다.|  
|**FirstChild**|시간 차원에 대해 측정값의 첫 번째 자식 멤버를 반환하여 집계됩니다.|  
|**FirstNonEmpty**|시간 차원에 대해 측정값의 첫 번째 비어 있지 않은 멤버를 반환하여 집계됩니다.|  
|**LastChild**|시간 차원에 대해 측정값의 마지막 자식 멤버를 반환하여 집계됩니다.|  
|**LastNonEmpty**|시간 차원에 대해 측정값의 마지막 비어 있지 않은 멤버를 반환하여 집계됩니다.|  
|`Max`|
  `Max` 함수를 사용하여 집계됩니다.|  
|`Min`|
  `Min` 함수를 사용하여 집계됩니다.|  
|**없음을**|집계가 수행되지 않습니다.|  
|`Sum`|
  `Sum` 함수를 사용하여 집계됩니다.|  
  
> [!NOTE]  
>  이 옵션에 대해 선택한 사항은 **개별 측정값에 대한 반가산적 동작 정의** 를 선택한 경우에만 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [비즈니스 인텔리전스 마법사 F1 도움말](business-intelligence-wizard-f1-help.md)   
 [큐브 디자이너 &#40;Analysis Services 다차원 데이터&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [차원 디자이너 &#40;Analysis Services 다차원 데이터&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
