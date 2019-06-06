---
title: 파생 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e0f6984c464c08518c7b3143986a041b195cce69
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695068"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
하나 이상의 특성을 지정 하는 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|필드 값을 캐시 하는 공급자 및 후속 읽기는 캐시에서 수행 함을 나타냅니다.|  
|**adFldFixed**|0x10|고정 길이 데이터를 필드에 포함 되어 있는지를 나타냅니다.|  
|**adFldIsChapter**|0x2000|필드에이 부모 필드와 관련 된 특정 자식 레코드 집합을 지정 하는 장 값이 있음을 나타냅니다. 일반적으로 장 필드 데이터 셰이핑 또는 필터를 사용 하 여 사용 됩니다.|  
|**adFldIsCollection**|0x40000|필드 레코드에서 표시 되는 리소스는 텍스트 파일과 같은 간단한 리소스를 보다는 폴더와 같은 다른 리소스의 컬렉션을 지정 함을 나타냅니다.|  
|**adFldKeyColumn**|0x8000|열의 기본 키의 전체 또는 일부 필드 지정 함을 나타냅니다.|  
|**adFldIsDefaultStream**|0x20000|필드에 레코드로 표시 되는 리소스에 대 한 기본 스트림이 있음을 나타냅니다. 예를 들어, 기본 스트림에 루트 URL을 지정 하는 경우 자동으로 제공 되는 웹 사이트의 루트 폴더의 HTML 콘텐츠를 수 있습니다.|  
|**adFldIsNullable**|0x20|필드에 null 값 허용 하는지 나타냅니다.|  
|**adFldIsRowURL**|0x10000|필드에 레코드로 표시 되는 데이터 저장소에서 리소스의 이름을 지정 하는 URL이 포함 되어 있음을 나타냅니다.|  
|**adFldLong**|0x80|필드 길이의 이진 필드 임을 나타냅니다. 사용할 수 있는 나타내기도 합니다 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 메서드.|  
|**adFldMayBeNull**|0x40|필드에서 null 값을 읽을 수 있는지를 나타냅니다.|  
|**adFldMayDefer**|0x2|지연 된 있는 필드 임을 나타냅니다 인 필드 값을 명시적으로 액세스 하는 경우에 하지만 전체 레코드를 사용 하 여 데이터 원본에서 검색 되지 합니다.|  
|**adFldNegativeScale**|0x4000|필드 음수 소수 자릿수 값을 지 원하는 열에서 숫자 값을 나타낸다는 것을 나타냅니다. 확장 된 합니다 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 속성입니다.|  
|**adFldRowID**|0x100|필드에 식별 (예: 레코드 번호, 고유 식별자 및 등)의 행만 의미가 있고 쓸 수 없는 영구 행 식별자가 포함 됨을 나타냅니다.|  
|**adFldRowVersion**|0x200|일부 종류의 업데이트를 추적 하는 데 사용 되는 시간 또는 날짜 스탬프 필드에 포함 되도록 나타냅니다.|  
|**adFldUnknownUpdatable**|0x8|공급자 수 없는 경우 필드에 작성할 수 있습니다 결정 함을 나타냅니다.|  
|**adFldUnspecified**|-1 0xFFFFFFFF|공급자에서 필드 특성을 지정 하지 않았는지를 나타냅니다.|  
|**adFldUpdatable**|0x4|필드에 쓸 수 있는지 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 해당  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Append 메서드(ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
