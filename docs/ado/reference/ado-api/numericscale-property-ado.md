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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99d27ff0348a22324ad99c515617a6831fa9f9f3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47722981"
---
# <a name="numericscale-property-ado"></a>NumericScale 속성(ADO)
숫자 값의 소수 자릿수를 나타냅니다는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md) 하거나 [필드](../../../ado/reference/ado-api/field-object.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **바이트** 소수 자릿수는 숫자 값의 수를 나타내는 값을 확인할 수 됩니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **NumericScale** 속성을 숫자 값을 나타내는 소수점 오른쪽 자릿수는 사용 될 **매개 변수** 또는 **필드** 개체입니다.  
  
 에 대 한 **매개 변수** 개체를 **NumericScale** 속성은 읽기/쓰기가 가능 합니다.  
  
 에 대 한는 **필드**개체를 **NumericScale** 일반적으로 읽기 전용입니다. 그러나에 대 한 새 **필드** 에 추가 된 개체를 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md)를 **NumericScale** 읽기/쓰기 설정한 후에 합니다 [값](../../../ado/reference/ado-api/value-property-ado.md) 속성에 대 한 합니다 **필드** 지정 된 데이터 공급자에 성공적으로 추가 하 고 **필드** 를호출하여[ 업데이트](../../../ado/reference/ado-api/update-method.md) 메서드를 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
|||  
|-|-|  
|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[Field 개체](../../../ado/reference/ado-api/field-object.md)|  
  
## <a name="see-also"></a>관련 항목  
 [NumericScale 및 Precision 속성 예제 (VB)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 및 Precision 속성 예제 (VC + +)](../../../ado/reference/ado-api/numericscale-and-precision-properties-example-vc.md)   
 [Precision 속성(ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
