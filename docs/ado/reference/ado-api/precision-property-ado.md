---
title: Precision 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Precision
- Field20::Precision
helpviewer_keywords:
- Precision property [ADO]
ms.assetid: 1fa38e78-6b5b-414d-ba0a-3dd26b29b766
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9819567ebe48a7654ee7a90f516ba14c8062bdcf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027862"
---
# <a name="precision-property-ado"></a>Precision 속성(ADO)
숫자 값에 대 한 전체 자릿수를 나타냅니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 개체 또는 숫자 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환 된 **바이트** 값을 나타내는 데 사용 되는 최대 자릿수를 나타내는 값입니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **정밀도** 숫자에 대 한 값을 나타내는 데 사용 되는 숫자의 최대 수를 확인 하는 속성 **매개 변수** 또는 **필드** 개체입니다.  
  
 값은 읽기/쓰기를 **매개 변수** 개체입니다.  
  
 에 대 한는 **필드**개체를 **정밀도** 일반적으로 읽기 전용입니다. 그러나에 대 한 새 **필드** 에 추가 된 개체를 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md)를 **정밀도** 만 읽기/쓰기 후는 [값](../../../ado/reference/ado-api/value-property-ado.md) 에 대 한 속성을 **필드** 지정 된 데이터 공급자에 성공적으로 추가 하 고 **필드** 를호출하여[업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 **필드** 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>관련 항목  
 [NumericScale 및 Precision 속성 예제 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 및 Precision 속성 예제 (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [NumericScale 속성(ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)
