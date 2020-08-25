---
description: AppendChunk 메서드(ADO)
title: AppendChunk 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: rothja
ms.author: jroth
ms.openlocfilehash: 0df71772820d5871c32e40827400b8cdd40db99d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776482"
---
# <a name="appendchunk-method-ado"></a>AppendChunk 메서드(ADO)
대량 텍스트 또는 이진 데이터 [필드](./field-object.md)또는 [매개 변수](./parameter-object.md) 개체에 데이터를 추가 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>매개 변수  
 *object*  
 **필드** 또는 **매개 변수** 개체입니다.  
  
 *데이터*  
 개체에 추가할 데이터를 포함 하는 **Variant** 입니다.  
  
## <a name="remarks"></a>설명  
 **필드** 또는 **매개 변수** 개체에 대해 **AppendChunk** 메서드를 사용 하 여 긴 이진 또는 문자 데이터로 채웁니다. 시스템 메모리가 제한 된 경우에는 **AppendChunk** 메서드를 사용 하 여 전체 값이 아닌 부분에서 긴 값을 조작할 수 있습니다.  
  
## <a name="field"></a>필드  
 **Field** 개체의 [Attributes](./attributes-property-ado.md) 속성에서 **adfldlong** 비트가 **true**로 설정 된 경우 해당 필드에 대해 **AppendChunk** 메서드를 사용할 수 있습니다.  
  
 **Field** 개체에 대 한 첫 번째 **AppendChunk** 호출은 필드에 데이터를 쓰고 기존 데이터를 덮어씁니다. 후속 **AppendChunk** 는 기존 데이터에 add를 호출 합니다. 한 필드에 데이터를 추가 하 고 현재 레코드의 다른 필드 값을 설정 하거나 읽는 경우 ADO는 첫 번째 필드에 데이터를 추가 하는 작업이 완료 된 것으로 가정 합니다. 첫 번째 필드에서 **AppendChunk** 메서드를 다시 호출 하는 경우 ADO는 호출을 새 **AppendChunk** 작업으로 해석 하 고 기존 데이터를 덮어씁니다. 첫 번째 **레코드 집합** 개체의 클론이 아닌 다른 [레코드 집합](./recordset-object-ado.md) 개체의 필드에 액세스 하면 **AppendChunk** 작업이 중단 되지 않습니다.  
  
 **Field** 개체에서 **AppendChunk** 를 호출할 때 현재 레코드가 없는 경우 오류가 발생 합니다.  
  
> [!NOTE]
>  **AppendChunk** 메서드는 [RECORD 개체 (ADO)](./record-object-ado.md) 개체의 **필드** 개체에 대해 작동 하지 않습니다. 작업을 수행 하지 않으며 런타임 오류를 생성 합니다.  
  
## <a name="parameter"></a>매개 변수  
 **매개 변수** 개체의 **Attributes** 속성에서 **adparamlong** 비트가 **true**로 설정 된 경우 해당 매개 변수에 대해 **AppendChunk** 메서드를 사용할 수 있습니다.  
  
 **매개 변수** 개체에 대 한 첫 번째 **AppendChunk** 호출은 데이터를 매개 변수에 쓰고 기존 데이터를 덮어씁니다. **매개 변수** 개체에 대 한 후속 **AppendChunk** 호출은 기존 매개 변수 데이터에 추가 합니다. Null 값을 전달 하는 **AppendChunk** 호출은 모든 매개 변수 데이터를 삭제 합니다.  
  
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
 [AppendChunk 및 GetChunk 메서드 예제 (VB)](./appendchunk-and-getchunk-methods-example-vb.md)   
 [AppendChunk 및 GetChunk 메서드 예제 (VC + +)](./appendchunk-and-getchunk-methods-example-vc.md)   
 [Attributes 속성 (ADO)](./attributes-property-ado.md)   
 [GetChunk 메서드(ADO)](./getchunk-method-ado.md)