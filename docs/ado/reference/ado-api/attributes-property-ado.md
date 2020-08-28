---
description: Attributes 속성(ADO)
title: Attributes 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Attributes
- Field20::Attributes
- _Parameter::Attributes
helpviewer_keywords:
- Attributes property [ADO]
ms.assetid: acc15d40-68a6-4ba9-85bd-12d331aecaa6
author: rothja
ms.author: jroth
ms.openlocfilehash: ceb141b0ecdbc278e324f19f3bd4b3d7ed1b4eb6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975944"
---
# <a name="attributes-property-ado"></a>Attributes 속성(ADO)
개체의 특성을 하나 이상 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **Long** 값을 설정 하거나 반환 합니다.  
  
 [Connection](./connection-object-ado.md) 개체의 경우 **Attributes** 속성은 읽기/쓰기가 가능 하 고 해당 값은 하나 이상의 [XactAttributeEnum](./xactattributeenum.md) 값의 합이 될 수 있습니다. 기본값은 0입니다.  
  
 [매개 변수](./parameter-object.md) 개체의 경우 **Attributes** 속성은 읽기/쓰기가 가능 하 고 해당 값은 하나 이상의 [ParameterAttributesEnum](./parameterattributesenum.md) 값의 합이 될 수 있습니다. 기본값은 **Adparamsigned**입니다.  
  
 [Field](./field-object.md) 개체의 경우 **Attributes** 속성은 하나 이상의 [FieldAttributeEnum](./fieldattributeenum.md) 값의 합계인 수 있습니다. 일반적으로 읽기 전용입니다. 그러나 [레코드](./record-object-ado.md)의 [fields](./fields-collection-ado.md) 컬렉션에 추가 된 새 **field** 개체의 경우 **필드** 의 [Value](./value-property-ado.md) 속성을 지정 하 고 **필드** 컬렉션의 [Update](./update-method.md) 메서드를 호출 하 여 데이터 공급자가 새 **필드** 를 성공적으로 추가한 후에만 **특성** 을 읽고 쓸 수 있습니다.  
  
 [속성](./property-object-ado.md) 개체의 경우 **Attributes** 속성은 읽기 전용 이며 해당 값은 하나 이상의 [PropertyAttributesEnum](./propertyattributesenum.md) 값의 합이 될 수 있습니다.  
  
## <a name="remarks"></a>설명  
 **Attributes** 속성을 사용 하 여 **연결** 개체, **매개 변수** 개체, **필드** 개체 또는 **속성** 개체의 특성을 설정 하거나 반환할 수 있습니다.  
  
 여러 특성을 설정 하는 경우 적절 한 상수의 합계를 사용할 수 있습니다. 호환 되지 않는 상수를 포함 하 여 속성 값을 합계로 설정 하면 오류가 발생 합니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽 **연결** 개체에서는이 속성을 사용할 수 없습니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [연결 개체(ADO)](./connection-object-ado.md)  
        [Field 개체](./field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 개체](./parameter-object.md)  
        [속성 개체(ADO)](./property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [특성 및 이름 속성 예제 (VB)](./attributes-and-name-properties-example-vb.md)   
 [특성 및 이름 속성 예제 (VC + +)](./attributes-and-name-properties-example-vc.md)   
 [AppendChunk 메서드 (ADO)](./appendchunk-method-ado.md)   
 [BeginTrans, CommitTrans 및 RollbackTrans 메서드 (ADO)](./begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [GetChunk 메서드(ADO)](./getchunk-method-ado.md)