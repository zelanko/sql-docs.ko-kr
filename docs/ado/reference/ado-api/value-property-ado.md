---
title: "Value 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 17e3c9f28e42dbd70118bb29a330514a9c29e013
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="value-property-ado"></a>Value 속성 (ADO)
에 할당 된 값을 나타냅니다는 [필드](../../../ado/reference/ado-api/field-object.md), [매개 변수](../../../ado/reference/ado-api/parameter-object.md), 또는 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **Variant** 개체의 값을 나타내는 값입니다. 기본값에 따라 다릅니다는 [형식](../../../ado/reference/ado-api/type-property-ado.md) 속성입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **값** 속성을 설정 하거나 데이터를 반환할 **필드** 개체를 설정 하거나 매개 변수 값을 반환할 **매개 변수** 개체를 설정 하거나 속성 설정을 반환 하려면 또는 **속성** 개체입니다. 여부는 **값** 속성은 읽기/쓰기 또는 읽기 전용 다양 한 요소에 따라 좌우??? 자세한 내용은 해당 개체 항목을 참조 하십시오.  
  
 ADO 설정 하 고 사용 하 여 긴 이진 데이터를 반환할 수 있습니다는 **값** 속성입니다.  
  
> [!NOTE]
>  에 대 한 **매개 변수** 개체, ADO 읽기는 **값** 속성 공급자에서 한 번만 합니다. 명령을 포함 하는 경우는 **매개 변수** 인 **값** 속성은 비어 있으며 만들면는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 명령에서 확인을 먼저 닫아야는 ** 레코드 집합** 검색 하기 전에 **값** 속성입니다. 일부 공급자에 대 한 고, 그렇지는 **값** 속성을 비어 있을 수 있습니다 및 올바른 값이 포함 되지 않습니다.  
>   
>  새 **필드** 에 추가 된 개체는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 개체는 **값** 속성을 설정 해야 다른 모든 하기 전에 **필드** 속성을 지정할 수 있습니다. 먼저, 특정 값에 대 한는 **값** 속성이 할당 해야 하 고 [업데이트](../../../ado/reference/ado-api/update-method.md) 에 **필드** 이라는 컬렉션. 그런 다음 같은 다른 속성과 [형식](../../../ado/reference/ado-api/type-property-ado.md) 또는 [특성](../../../ado/reference/ado-api/attributes-property-ado.md) 액세스할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [값 속성 예제 (VB)](../../../ado/reference/ado-api/value-property-example-vb.md)   
 [Value 속성 예제(VC++)](../../../ado/reference/ado-api/value-property-example-vc.md)   

