---
title: "열 속성 (SSAS 테이블 형식) | Microsoft Docs"
ms.custom: 
ms.date: 05/23/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.columnprop.f1
ms.assetid: 4046c1a3-46c7-47db-b355-52e9c2f23671
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: ce23f4ec3f28ed2057ac2433615b1ab4fb98938a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="column-properties-ssas-tabular"></a>열 속성(SSAS 테이블 형식)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]이 항목에서는 테이블 형식 모델 열 속성을 설명 합니다.  
  
>  [!NOTE]  
>  일부 속성은 모든 호환성 수준에서 지원 되지 않습니다.    
  
##  <a name="bkmk_properties"></a> 열 속성  
**고급**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**표시 폴더**||클라이언트 응용 프로그램 필드 목록에서 열 구성을 위한 단일 또는 중첩 폴더입니다.|  

**Basic**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**열 이름**||모델에 저장되고 보고 클라이언트 필드 목록에 표시되는 열의 이름입니다.|  
|**데이터 형식**|가져오는 동안 자동으로 결정됩니다.|이 열의 데이터에 사용할 표시 형식을 지정합니다. 이 속성에는 다음과 같은 옵션이 있습니다.<br /><br /> **일반**<br /><br /> **10진수**<br /><br /> **정수**<br /><br /> **Currency**<br /><br /> **백분율**<br /><br /> **공학**<br /><br /> 데이터 형식을 설정한 후 각 형식과 관련된 속성을 설정할 수 있습니다. 예를 들어 **통화** 형식을 선택하는 경우 표시되는 소수 자릿수를 설정하고 천 단위 구분 기호를 선택한 다음 통화 기호를 선택할 수 있습니다.<br /><br /> <br /><br /> 열 값에 이미지가 포함된 경우 **대표 이미지**를 참조하세요.|  
|**데이터 형식**|가져오는 동안 자동으로 결정됩니다.|열에 포함된 모든 값의 데이터 형식을 지정합니다.|  
|**Description**||열에 대한 텍스트 설명입니다.<br /><br /> 일부 보고 클라이언트에서는 최종 사용자가 필드 목록의 이 열 위에 커서를 두면 설명이 도구 설명으로 나타납니다.|  
|**숨김**|False|보고 클라이언트 필드 목록에서 열이 숨겨지는지 여부를 지정합니다.<br /><br /> 이 열을 숨기려면 이 속성을 **True** 로 설정합니다. 예를 들어 식별자나 키가 포함된 열은 일반적으로 최종 사용자에게 유용하지 않습니다.<br /><br /> 보고 클라이언트에서 열을 숨기는 경우 모델 데이터에서는 해당 필드가 표시됩니다. 모델에 대한 쿼리를 만드는 경우 해당 필드가 여전히 표시됩니다. 숨겨진 열을 그룹화나 정렬에 계속 사용할 수 있습니다.<br /><br /> **숨김** 속성은 어떠한 형태의 데이터 보안도 제공하지 않습니다. 데이터를 보호하려면 역할에서 행 필터를 사용합니다. 자세한 내용은 [역할&#40;SSAS 테이블 형식&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)을 참조하세요.|  
|**열 기준 정렬**||이 열의 값을 정렬할 다른 열을 지정합니다. 두 열 간의 관계가 존재해야 합니다.<br /><br /> 이 값은 기존 열의 이름이어야 합니다. 수식 또는 측정값을 지정할 수 없습니다.|  

 **기타**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**인코딩 힌트**|기본값|처리를 최적화 하기 위해 인코딩을 지정 합니다. 값 인코딩을 집계에 일반적으로 사용 되는 숫자 열에 대 한 쿼리 성능을 향상 시킬 수 있습니다. 해시 인코딩을 group by 열 (대개 차원 테이블 값) 및 외래 키입니다. 문자열 열은 항상 인코딩된 해시입니다.|  

 **보고 속성**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|기본 이미지|False|행 데이터를 표시하는 이미지를 제공하는 열을 지정합니다(예: 직원 레코드의 사진 ID).|  
|기본 레이블|False|행 데이터를 표시하도록 표시 이름을 제공하는 열을 지정합니다(예: 직원 레코드의 직원 이름).|  
|이미지 URL/데이터 범주(SP1)|False|이 열의 값을 서버의 이미지에 대한 하이퍼링크로 지정합니다. 예를 들면 `http://localhost/images/image1.jpg`과 같습니다.|  
|고유한 행 유지|False|중복된 경우에도 고유한 값으로 처리되어야 하는 값을 제공하는 열을 지정합니다(예: 이름이 같은 직원이 여러 명 있는 경우의 직원 이름과 성).|  
|행 식별자|False|열을 내부 그룹화 키로 사용할 수 있도록 고유한 값만 포함하는 열을 지정합니다.|  
|요약 기준|기본값|이 열이 필드 목록에 추가될 때 보고 클라이언트 도구에서 열 계산에 대한 집계 함수 SUM을 적용하도록 지정합니다. 기본 계산을 변경하려면 드롭다운 목록에서 기본 계산을 선택합니다. 이 속성은 집계할 수 있는 형식의 열에만 적용됩니다.|  
|테이블 세부 정보 위치|기본 필드 집합 없음|보고 클라이언트에서 테이블 시각화 환경을 개선할 수 있도록 이 열 또는 측정값을 단일 테이블의 필드 집합에 추가할 수 있도록 지정합니다.|  
  
##  <a name="bkmk_config_prop"></a> 열 속성 설정 구성  
  
1.  모델 디자이너의 테이블에서 열을 선택합니다.  
  
2.  **속성** 창에서 속성을 클릭한 다음 값을 입력하거나 아래쪽 화살표를 클릭하여 설정 옵션을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Power View 보고 속성](../../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md)   
 [열 숨기기 또는 고정](../../analysis-services/tabular-models/hide-or-freeze-columns-ssas-tabular.md)   
 [테이블에 열 추가](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)  
  
  
