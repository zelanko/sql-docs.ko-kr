---
description: NumericScale 속성(ADO)
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
ms.openlocfilehash: 57375b89595c6ed3e5c377692709deacd8f0ff28
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773972"
---
# <a name="numericscale-property-ado"></a>NumericScale 속성(ADO)
[매개 변수](./parameter-object.md) 또는 [필드](./field-object.md) 개체에서 숫자 값의 소수 자릿수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 숫자 값이 확인 되는 소수 자릿수를 나타내는 **바이트** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **NumericScale** 속성을 사용 하 여 숫자 **매개 변수** 또는 **필드** 개체의 값을 나타내는 데 사용 되는 소수점 오른쪽 자릿수를 결정 합니다.  
  
 **매개 변수** 개체의 경우 **NumericScale** 속성은 읽기/쓰기입니다.  
  
 **Field**개체의 경우 **NumericScale** 는 일반적으로 읽기 전용입니다. 그러나 [레코드](./record-object-ado.md)의 [Fields](./fields-collection-ado.md) 컬렉션에 추가 된 새 **field** 개체의 경우에는 **필드** 의 [Value](./value-property-ado.md) 속성이 지정 된 후에만 **NumericScale** 가 읽기/쓰기이 고, 데이터 공급자는 [Fields](./fields-collection-ado.md) 컬렉션의 [Update](./update-method.md) 메서드를 호출 하 여 새 **필드** 를 성공적으로 추가 했습니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Field 개체](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 개체](./parameter-object.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [NumericScale 및 Precision 속성 예제 (VB)](./numericscale-and-precision-properties-example-vb.md)   
 [NumericScale 및 Precision 속성 예제 (VC + +)](./numericscale-and-precision-properties-example-vc.md)   
 [Precision 속성(ADO)](./precision-property-ado.md)