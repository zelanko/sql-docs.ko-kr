---
title: Name 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Name
- Field20::Name
helpviewer_keywords:
- Name property [ADO]
ms.assetid: cfd0e29c-8310-44ab-85c3-5761184b865d
author: rothja
ms.author: jroth
ms.openlocfilehash: 368def89951e7d0eacca9b999b647abd949c3b10
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243234"
---
# <a name="name-property-ado"></a>Name 속성(ADO)
개체의 이름을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 개체의 이름을 나타내는 **문자열** 값을 설정 하거나 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **이름 속성을** 사용 하 여 이름을 할당 하거나 **명령**, **속성**, **필드**또는 **매개 변수** 개체의 이름을 검색 합니다.  
  
 이 값은 **명령** 개체에 대 한 읽기/쓰기 및 **속성** 개체에 대 한 읽기 전용입니다.  
  
 **필드** 개체의 경우 **이름은** 일반적으로 읽기 전용입니다. 그러나 [레코드](../../../ado/reference/ado-api/record-object-ado.md)의 [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) 컬렉션에 추가 된 새 **field** 개체의 경우 **필드** 의 [Value](../../../ado/reference/ado-api/value-property-ado.md) 속성을 지정 하 고 데이터 공급자가 **Fields** 컬렉션의 [Update](../../../ado/reference/ado-api/update-method.md) 메서드를 호출 하 여 새 **필드** 를 성공적으로 추가한 후에만 **이름이** 읽기/쓰기입니다.  
  
 [매개 변수 컬렉션에](../../../ado/reference/ado-api/parameters-collection-ado.md) 아직 추가 되지 않은 **매개 변수** 개체의 경우 **Name** 속성은 읽기/쓰기가 됩니다. 추가 된 **매개 변수** 개체 및 기타 모든 개체의 경우 **Name** 속성은 읽기 전용입니다. 이름은 컬렉션 내에서 고유 하지 않아도 됩니다.  
  
 서 수 참조로 개체의 **이름** 속성을 검색할 수 있으며, 그 후에는 개체를 이름으로 직접 참조할 수 있습니다. 예를 들어가 `rstMain.Properties(20).Name` 생성 되 면 `Updatability` 이후에이 속성을 참조할 수 있습니다 `rstMain.Properties("Updatability")` .  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [명령 개체(ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [Field 개체](../../../ado/reference/ado-api/field-object.md)  
    :::column-end:::
    :::column:::
        [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)  
        [속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [특성 및 이름 속성 예제 (VB)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vb.md)   
 [특성 및 이름 속성 예제 (VC + +)](../../../ado/reference/ado-api/attributes-and-name-properties-example-vc.md)   
