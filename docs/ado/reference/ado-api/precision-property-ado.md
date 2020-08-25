---
description: Precision 속성(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 59a42a7f577ae8f4712e679853d53939fd6f6ed1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773142"
---
# <a name="precision-property-ado"></a>Precision 속성(ADO)
[매개 변수](./parameter-object.md) 개체 또는 숫자 [필드](./field-object.md) 개체의 숫자 값에 대 한 전체 자릿수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 값을 나타내는 데 사용 되는 최대 자릿수를 나타내는 **바이트** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Precision** 속성을 사용 하 여 숫자 **매개 변수** 또는 **Field** 개체의 값을 나타내는 데 사용 되는 최대 자릿수를 확인 합니다.  
  
 값은 **매개 변수** 개체에 대 한 읽기/쓰기입니다.  
  
 **필드**개체의 경우 **전체 자릿수** 는 일반적으로 읽기 전용입니다. 그러나 [레코드](./record-object-ado.md)의 [Fields](./fields-collection-ado.md) 컬렉션에 추가 된 새 **field** 개체의 경우 **필드** 의 [Value](./value-property-ado.md) 속성을 지정 하 고 데이터 공급자가 **Fields** 컬렉션의 [Update](./update-method.md) 메서드를 호출 하 여 새 **필드** 를 성공적으로 추가한 후에만 **전체 자릿수가** 읽기/쓰기입니다.  
  
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
 [NumericScale 속성(ADO)](./numericscale-property-ado.md)