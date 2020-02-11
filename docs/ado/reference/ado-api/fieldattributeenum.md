---
title: FieldAttributeEnum | Microsoft Docs
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
ms.openlocfilehash: 0d375ed3dd4ea7ae7e2e5405d1feec962c5f56ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918700"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
[Field](../../../ado/reference/ado-api/field-object.md) 개체의 특성을 하나 이상 지정 합니다.  
  
|지속적임|값|Description|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|공급자가 필드 값을 캐시 하 고 이후 읽기가 캐시에서 수행 됨을 나타냅니다.|  
|**adFldFixed**|0x10|필드에 고정 길이 데이터가 포함 되어 있음을 나타냅니다.|  
|**adFldIsChapter**|0x2000|필드에이 부모 필드와 관련 된 특정 자식 레코드 집합을 지정 하는 챕터 값이 포함 되어 있음을 나타냅니다. 일반적으로 챕터 필드는 데이터 셰이핑 또는 필터와 함께 사용 됩니다.|  
|**adFldIsCollection**|0x40000|필드에서 레코드가 나타내는 리소스가 텍스트 파일과 같은 단순한 리소스가 아닌 다른 리소스 (예: 폴더)의 컬렉션 임을 지정 함을 나타냅니다.|  
|**adFldKeyColumn**|0x8000|필드에서 열의 기본 키 전체 또는 일부를 지정 함을 나타냅니다.|  
|**adFldIsDefaultStream**|0x20000|필드에 레코드가 나타내는 리소스에 대 한 기본 스트림이 포함 되어 있음을 나타냅니다. 예를 들어, 기본 스트림은 루트 URL이 지정 될 때 자동으로 제공 되는 웹 사이트의 루트 폴더에 대 한 HTML 콘텐츠가 될 수 있습니다.|  
|**adFldIsNullable**|0x20|필드에 null 값이 허용 됨을 나타냅니다.|  
|**adFldIsRowURL**|0x10000|필드에 레코드가 나타내는 데이터 저장소의 리소스 이름을 지정 하는 URL이 포함 되어 있음을 나타냅니다.|  
|**adFldLong**|0x80|필드가 긴 이진 필드 임을 나타냅니다. 또한 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 메서드를 사용할 수 있음을 나타냅니다.|  
|**adFldMayBeNull**|0x40|필드에서 null 값을 읽을 수 있음을 나타냅니다.|  
|**adFldMayDefer**|0x2|필드가 지연 됨을 나타냅니다. 즉, 필드 값이 전체 레코드를 사용 하 여 데이터 원본에서 검색 되지 않고 명시적으로 액세스 하는 경우에만 해당 됩니다.|  
|**adFldNegativeScale**|0x4000|필드가 음수 배율 값을 지 원하는 열의 숫자 값을 나타내는지 여부를 나타냅니다. 배율은 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 속성으로 지정 됩니다.|  
|**adFldRowID**|0x100|필드에 쓸 수 없는 영구 행 식별자가 포함 되어 있고 행 (예: 레코드 번호, 고유 식별자 등)을 식별 하는 것을 제외 하 고 의미 있는 값을 포함 하지 않음을 나타냅니다.|  
|**adFldRowVersion**|0x200|필드에 업데이트를 추적 하는 데 사용 되는 특정 시간 또는 날짜 스탬프가 포함 되어 있음을 나타냅니다.|  
|**adFldUnknownUpdatable**|0x8|필드에 쓸 수 있는지 여부를 공급자가 결정할 수 없음을 나타냅니다.|  
|**adFldUnspecified 되지 않음**|-1 0xFFFFFFFF|공급자가 필드 특성을 지정 하지 않음을 나타냅니다.|  
|**adFldUpdatable 가능**|0x4|필드에 쓸 수 있음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|지속적임|  
|--------------|  
|AdoEnums. FieldAttribute 지연 됨|  
|AdoEnums. FieldAttribute|  
|AdoEnums. FieldAttribute. ISNULLABLE|  
|AdoEnums. FieldAttribute|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums. FieldAttribute|  
|AdoEnums. FieldAttribute. ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums. FieldAttribute|  
|AdoEnums. FieldAttribute|  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Append 메서드(ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Attributes 속성(ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
