---
title: DataSourceType 요소 (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DataSourceType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords:
- DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c911f2a0e224cb8ccc9e7fa5b32a89a972fd1c26
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207673"
---
# <a name="datasourcetype-element-xmla"></a>DataSourceType 요소(XMLA)
  나타냅니다 여부를 [위치](location-element-xmla.md) 에 대 한 지정 된 요소를 [복원](../xml-elements-commands/restore-element-xmla.md) 또는 [동기화](../xml-elements-commands/synchronize-element-xmla.md) 로컬 또는 원격 명령입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*원격*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[위치](location-element-xmla.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `DataSourceType` 요소는 `Location` 요소에 정의된 데이터 원본이 로컬 데이터 원본 또는 원격 데이터 원본을 포함하는지를 결정합니다. 백업 및 원격 파티션을 복원 하는 방법에 대 한 자세한 내용은 참조 하세요. [Backing Up, Restoring, and 데이터베이스 동기화 &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*로컬*|`Location` 요소는 로컬 데이터 원본을 정의합니다. 이 값을 사용하면 `Restore` 및 `Synchronize` 명령이 `Location` 요소에 정의된 정보를 사용하여 `File` 명령의 `Backup` 요소에 지정된 백업 파일 또는 `Source` 명령의 `Synchronize` 요소에 지정된 데이터베이스에서 검색되고 `DataSourceID` 요소의 `Location` 요소에서 식별되는 데이터 원본을 업데이트합니다.<br /><br /> 이 값을 사용하면 ROLAP(관계형 OLAP) 저장소를 사용하는 개체가 복원 또는 동기화된 후 해당 데이터 및 메타데이터에 대해 다른 데이터베이스를 사용할 수 있습니다. **참고:** 차원 테이블 또는 쓰기 저장 테이블의 데이터와 같은 ROLAP 데이터를 복원 하거나 동기화 되지 않습니다. ROLAP 개체의 메타데이터만 복원 또는 동기화됩니다.|  
|*원격*|`Location` 요소는 원격 데이터 원본을 정의합니다. 이 값을 사용하면 `Restore` 및 `Synchronize` 명령이 `Location` 요소에 정의된 정보를 사용하여 `File` 명령의 `Backup` 요소에 지정된 백업 파일 또는 `Source` 명령의 `Synchronize` 요소에 지정된 데이터베이스에서 검색되고 `DataSourceID` 요소의 `Location` 요소에서 식별되는 데이터 원본을 업데이트합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [ConnectionString 요소 &#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [DataSourceID 요소 &#40;XMLA&#41;](id-element-xmla.md)   
 [속성 &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
