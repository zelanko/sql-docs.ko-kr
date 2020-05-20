---
title: NumericScale 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
author: rothja
ms.author: jroth
ms.openlocfilehash: 3970ab8d8f446c4269e4b79c306d2dd9d2cf0426
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762332"
---
# <a name="numericscale-property-ado"></a>NumericScale 속성(ADO)
[매개 변수](../../../ado/reference/ado-api/parameter-object.md) 또는 [필드](../../../ado/reference/ado-api/field-object.md) 개체에서 숫자 값의 소수 자릿수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 숫자 값이 확인 되는 소수 자릿수를 나타내는 **바이트** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **NumericScale** 속성을 사용 하 여 숫자 **매개 변수** 또는 **필드** 개체의 값을 나타내는 데 사용 되는 소수점 오른쪽 자릿수를 결정 합니다.  
  
 **매개 변수** 개체의 경우 **NumericScale** 속성은 읽기/쓰기입니다.  
  
 **Field**개체의 경우 **NumericScale** 는 일반적으로 읽기 전용입니다. 그러나 [레코드](../../../ado/reference/ado-api/record-object-ado.md)의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 추가 된 새 **field** 개체의 경우에는 **필드** 의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성이 지정 된 후에만 **NumericScale** 가 읽기/쓰기이 고, 데이터 공급자는 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션의 [Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출 하 여 새 **필드** 를 성공적으로 추가 했습니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[Field 개체](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>참고 항목  
 [NumericScale 및 Precision 속성 예제 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 및 Precision 속성 예제 (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Precision 속성(ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
