---
title: NumericScale 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::NumericScale
- Field20::NumericScale
helpviewer_keywords:
- NumericScale property [ADO]
ms.assetid: 29a02992-64be-4fcd-be13-445cba205893
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d05fcf200934bedae4a7092268e6323482848324
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="numericscale-property-ado"></a>NumericScale 속성 (ADO)
숫자 값의 소수 자릿수를 나타냅니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 또는 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **바이트** 소수 자릿수는 숫자 값의 수를 나타내는 값을 해결 됩니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **NumericScale** 속성을 소수점 오른쪽 자릿수는 숫자에 대 한 값을 나타낼 때를 **매개 변수** 또는 **필드** 개체입니다.  
  
 에 대 한 **매개 변수** 개체는 **NumericScale** 속성은 읽기/쓰기가 가능 합니다.  
  
 에 대 한는 **필드**개체 **NumericScale** 일반적으로 읽기 전용입니다. 그러나에 대 한 새로운 **필드** 에 추가 된 개체는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md), **NumericScale** 은 읽기/쓰기 후에는 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성에 대 한는 **필드** 지정 된 데이터 공급자가 성공적으로 새 추가 하 고 **필드** 는 를호출하여[ 업데이트](../../../ado/reference/ado-api/update-method.md) 의 메서드는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[Field 개체](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [NumericScale 및 전체 자릿수 속성 예제 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 및 전체 자릿수 속성 예 (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Precision 속성(ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
