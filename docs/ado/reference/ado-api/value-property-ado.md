---
description: Value 속성(ADO)
title: Value 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::Value
- _Parameter::Value
helpviewer_keywords:
- Value property [ADO]
ms.assetid: 48919c74-86d4-462e-99b9-8854ceb8d683
author: rothja
ms.author: jroth
ms.openlocfilehash: 719a647f42c66e73b9bd55ed0a7476dfb95934e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441595"
---
# <a name="value-property-ado"></a>Value 속성(ADO)

[필드](../../../ado/reference/ado-api/field-object.md), [매개 변수](../../../ado/reference/ado-api/parameter-object.md)또는 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체에 할당 된 값을 나타냅니다.
  
## <a name="settings-and-return-values"></a>설정 및 반환 값

개체의 값을 나타내는 **Variant** 값을 설정 하거나 반환 합니다. 기본값은 [Type](../../../ado/reference/ado-api/type-property-ado.md) 속성에 따라 달라 집니다.
  
## <a name="remarks"></a>설명

**Value** 속성을 사용 하 여 **필드** 개체에서 데이터를 설정 또는 반환 **하거나 매개 변수 개체로 매개** 변수 값을 설정 또는 반환 하거나 **속성** 개체를 사용 하 여 속성 설정을 설정 하거나 반환할 수 있습니다. **값** 속성이 읽기/쓰기 또는 읽기 전용인 지 여부는 다양 한 요인에 따라 다릅니다. 자세한 내용은 해당 개체 항목을 참조 하십시오.

ADO에서는 **Value** 속성을 사용 하 여 긴 이진 데이터를 설정 하 고 반환할 수 있습니다.
  
> [!NOTE]
> **매개 변수** 개체의 경우 ADO는 공급자에서 **값** 속성을 한 번만 읽습니다. 명령에 **값** 속성이 비어 있는 **매개 변수가** 포함 되어 있는 경우 명령에서 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 을 만드는 경우 **Value** 속성을 검색 하기 전에 먼저 **레코드 집합** 을 닫아야 합니다. 그렇지 않으면 일부 공급자의 경우 **value** 속성이 비어 있을 수 있으며, 올바른 값을 포함 하지 않습니다.
> 
> [Record](../../../ado/reference/ado-api/record-object-ado.md) 개체의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 추가 된 새 **Field** 개체의 경우 다른 **필드** 속성을 지정 하려면 먼저 **Value** 속성을 설정 해야 합니다. 먼저 **value** 속성의 특정 값이 할당 되 고 라는 **필드** 컬렉션에 대해 [업데이트](../../../ado/reference/ado-api/update-method.md) 되어야 합니다. 그런 다음 [형식](../../../ado/reference/ado-api/type-property-ado.md) 또는 [특성과](../../../ado/reference/ado-api/attributes-property-ado.md) 같은 다른 속성에 액세스할 수 있습니다.
  
## <a name="applies-to"></a>적용 대상

:::row:::
    :::column:::
        [Field 개체](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
    :::column-end:::
    :::column:::
        [속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목

[Value 속성 예제 (VB)](../../../ado/reference/ado-api/value-property-example-vb.md) 
 [Value 속성 예제 (VC + +)](../../../ado/reference/ado-api/value-property-example-vc.md) 
