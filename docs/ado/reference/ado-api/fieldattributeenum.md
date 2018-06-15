---
title: 파생 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36f972b9fb1f9592c6a9809b415e5570990a9057
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278632"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
하나 이상의 특성을 지정 하는 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
|상수|값|Description|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|공급자 필드 값을 캐시 하는 캐시에서 후속 읽기 했는지 나타냅니다.|  
|**adFldFixed**|0x10|고정 길이 데이터 필드에 포함 되어 있음을 나타냅니다.|  
|**adFldIsChapter**|0x2000|이 부모 필드에 관련 된 특정 자식 레코드 집합을 지정 하는 장 값을 필드에 포함 되어 있음을 나타냅니다. 일반적으로 장 필드는 데이터 셰이핑 또는 필터를 함께 사용 됩니다.|  
|**adFldIsCollection**|0x40000|필드에 레코드로 표시 되는 리소스는 텍스트 파일 등의 간단한 리소스 대신 폴더 등의 다른 리소스의 컬렉션 임을 지정 함을 나타냅니다.|  
|**adFldKeyColumn**|0x8000|열의 기본 키의 전체 또는 일부 필드를 지정 함을 나타냅니다.|  
|**adFldIsDefaultStream**|0x20000|필드에 레코드로 표시 되는 리소스에 대 한 기본 스트림이 있음을 나타냅니다. 예를 들어 기본 스트림을 루트 URL을 지정 하는 경우 자동으로 제공 되는 웹 사이트에서 루트 폴더의 HTML 콘텐츠를 수 있습니다.|  
|**adFldIsNullable**|0x20|필드가 null 값을 받아들이는 것을 나타냅니다.|  
|**adFldIsRowURL**|0x10000|필드에 레코드로 표시 되는 데이터 저장소에서 리소스의 이름을 지정 하는 URL이 포함 되어 있음을 나타냅니다.|  
|**adFldLong**|0x80|필드 길이의 이진 필드 임을 나타냅니다. 사용할 수 있는 나타냅니다는 [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) 및 [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) 메서드.|  
|**adFldMayBeNull**|0x40|필드에서 null 값을 읽을 수 있는지를 나타냅니다.|  
|**adFldMayDefer**|0x2|필드 지연 됨을 나타냅니다.-즉, 필드 값 전체 레코드와 하지만 명시적으로 액세스 하는 경우에 데이터 원본에서 검색 되지 않는다는 합니다.|  
|**adFldNegativeScale**|0x4000|필드 음수 크기 조정 값을 사용할 수 있는 열에서 숫자 값을 나타낸다는 것을 의미 합니다. 눈금으로 지정 된 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 속성입니다.|  
|**adFldRowID**|0x100|필드 (예: a 레코드 번호, 고유 식별자 및 등)은 행을 식별에 의미가 있으며에 쓸 수 없는 영구 행 식별자가 포함 되어 있음을 나타냅니다.|  
|**adFldRowVersion**|0x200|일부 종류의 업데이트를 추적 하는 데 사용 되는 시간 또는 날짜 스탬프 필드에 포함 되어 있음을 나타냅니다.|  
|**adFldUnknownUpdatable**|0x8|필드에 쓸 수 있으면 공급자 확인할 수 없음을 나타냅니다.|  
|**adFldUnspecified**|-1 0xFFFFFFFF|공급자의 필드 특성을 지정 하지 않는 것을 나타냅니다.|  
|**adFldUpdatable**|0x4|필드에 쓸 수 있는지를 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>해당 하는 ADO/WFC  
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
