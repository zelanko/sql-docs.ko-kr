---
title: DataSourceType 요소 (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3e50b2070a4665df9fd64a09609b4f3d34ecf494
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="datasourcetype-element-xmla"></a>DataSourceType 요소(XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  나타냅니다 여부는 [위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) 에 대 한 지정 된 요소는 [복원](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) 또는 [동기화](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) 로컬 또는 원격 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*원격*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[위치](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 **DataSourceType** 요소는 **Location** 요소에 정의된 데이터 원본이 로컬 데이터 원본 또는 원격 데이터 원본을 포함하는지를 결정합니다. 백업 및 원격 파티션을 복원 하는 방법에 대 한 자세한 내용은 참조 [Backing Up, Restoring, 및 데이터베이스 동기화 & #40; XMLA & #41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*로컬*|**Location** 요소는 로컬 데이터 원본을 정의합니다. 이 값을 사용하면 **Restore** 및 **Synchronize** 명령이 **Location** 요소에 정의된 정보를 사용하여 **File** 명령의 **Backup** 요소에 지정된 백업 파일 또는 **Source** 명령의 **Synchronize** 요소에 지정된 데이터베이스에서 검색되고 **DataSourceID** 요소의 **Location** 요소에서 식별되는 데이터 원본을 업데이트합니다.<br /><br /> 이 값을 사용하면 ROLAP(관계형 OLAP) 저장소를 사용하는 개체가 복원 또는 동기화된 후 해당 데이터 및 메타데이터에 대해 다른 데이터베이스를 사용할 수 있습니다.<br /><br /> 참고: 차원 테이블 또는 쓰기 저장 테이블의 데이터 같은 ROLAP 데이터는 복원 말거나 동기화 합니다. ROLAP 개체의 메타데이터만 복원 또는 동기화됩니다.|  
|*원격*|**Location** 요소는 원격 데이터 원본을 정의합니다. 이 값을 사용하면 **Restore** 및 **Synchronize** 명령이 **Location** 요소에 정의된 정보를 사용하여 **File** 명령의 **Backup** 요소에 지정된 백업 파일 또는 **Source** 명령의 **Synchronize** 요소에 지정된 데이터베이스에서 검색되고 **DataSourceID** 요소의 **Location** 요소에서 식별되는 데이터 원본을 업데이트합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [ConnectionString 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)   
 [DataSourceID 요소 &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)   
 [속성 & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
