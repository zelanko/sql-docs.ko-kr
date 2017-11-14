---
title: "전체 자릿수 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce6c07fa24f146664ffe5433869e4edf45abdd69
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="precision-property-ado"></a>전체 자릿수 속성 (ADO)
숫자 값에 대 한 전체 자릿수 수준을 나타냅니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 또는 한 숫자 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **바이트** 값을 나타내기 위해 사용 되는 최대 자릿수를 나타내는 값입니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **정밀도** 숫자에 대 한 값을 나타내는 데 사용 되는 최대 자릿수를 결정 하는 속성 **매개 변수** 또는 **필드** 개체입니다.  
  
 에 값은 읽기/쓰기는 **매개 변수** 개체입니다.  
  
 에 대 한는 **필드**개체 **정밀도** 일반적으로 읽기 전용입니다. 그러나에 대 한 새로운 **필드** 에 추가 된 개체는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md), **정밀도** 만 읽기/쓰기가 후의 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성에 대 한는 **필드** 지정 된 데이터 공급자가 성공적으로 새 추가 하 고 **필드** 는 를호출하여[업데이트](../../../ado/reference/ado-api/update-method.md) 의 메서드는 **필드** 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [NumericScale 및 전체 자릿수 속성 예제 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 및 전체 자릿수 속성 예 (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 속성(ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)

