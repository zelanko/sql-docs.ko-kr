---
title: 측정값 그룹 바인딩 대화 상자 (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.measuregroupbindings.f1
helpviewer_keywords:
- Measure Group Bindings dialog box
ms.assetid: ed642780-5350-438e-af73-b9ceab3f876d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 24faef5cd2e65ae89cc200f3461133d00cc81716
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059943"
---
# <a name="measure-group-bindings-dialog-box-analysis-services---multidimensional-data"></a>측정값 그룹 바인딩 대화 상자(Analysis Services - 다차원 데이터)
  **관계 정의** 대화 상자에서 액세스할 수 있는 **측정값 그룹 바인딩** 대화 상자를 사용하여 큐브 차원의 모든 특성에 대해 Null 처리 옵션을 지정할 수 있을 뿐만 아니라 일반 차원 관계에 대해 큐브 차원의 비세분성 특성과 측정값 그룹 열 간의 직접 관계를 생성 및 수정할 수 있습니다.  
  
## <a name="options"></a>변수  
 **측정값 그룹 테이블**  
 선택한 측정값 그룹에 대한 팩트 테이블의 이름을 표시합니다.  
  
 **특성**  
 특성 및 차원 테이블이 포함된 표를 표시합니다. 만들 특성을 선택하거나 선택한 특성에 대해 **관계** 에서 속성을 수정합니다. 표에는 다음 열이 있습니다.  
  
|옵션|정의|  
|------------|----------------|  
|**특성 이름**|특성 이름을 표시합니다.|  
|**차원 테이블**|특성이 기준으로 하는 차원 테이블의 이름을 표시합니다.|  
  
 **관계**  
 선택한 특성에 대한 차원 테이블 열과 선택한 측정값 그룹에 대한 팩트 테이블 열 간의 관계와 이 관계에 대한 Null 처리 옵션을 나타내는 표를 표시합니다. 표에는 다음 열이 있습니다.  
  
|옵션|정의|  
|------------|----------------|  
|**차원 열**|**특성** 에서 선택한 특성이 기준으로 하는 차원 테이블의 열을 표시합니다.|  
|**측정값 그룹 열**|차원에서 상속한 측정값 그룹 관계를 사용하려면 **차원에서 상속** 을 선택하고 관계를 명시적으로 정의하려면 측정값 그룹이 기준으로 하는 팩트 테이블의 열을 선택합니다.|  
|**Null 처리**|특성에 대한 Null 처리 옵션을 선택합니다. Null 처리 옵션에 대한 자세한 내용은 [NullProcessing 요소&#40;ASSL&#41;](scripting/properties/nullprocessing-element-assl.md)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [관계 정의 대화 상자 &#40;Analysis Services-다차원 데이터&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
