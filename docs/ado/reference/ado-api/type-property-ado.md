---
title: Type 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Type
- Field20::Type
helpviewer_keywords:
- Type property [ADO]
ms.assetid: 8a4c079f-9f4f-4545-801d-85983b8db71e
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33bf90a2ac3101cbf582449f2b5495f110a37a62
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282572"
---
# <a name="type-property-ado"></a>Type 속성 (ADO)
작업 형식 또는 데이터 형식을 나타내는 [매개 변수](../../../ado/reference/ado-api/parameter-object.md), [필드](../../../ado/reference/ado-api/field-object.md), 또는 [속성](../../../ado/reference/ado-api/property-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 에 대 한 **매개 변수** 개체는 **형식** 속성은 읽기/쓰기가 가능 합니다. 새 **필드** 에 추가 된 개체는 [필드](../../../ado/reference/ado-api/fields-collection-ado.md) 의 컬렉션을 [레코드](../../../ado/reference/ado-api/record-object-ado.md), **형식** 은 읽기/쓰기는 한후에[ 값](../../../ado/reference/ado-api/value-property-ado.md) 속성에 대 한는 **필드** 지정 된 데이터 공급자가 성공적으로 새 추가 하 고 **필드** 호출 하 여는 [업데이트](../../../ado/reference/ado-api/update-method.md)의 메서드는 **필드** 컬렉션입니다.  
  
 다른 모든 개체에 대 한는 **형식** 속성은 읽기 전용입니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Field 개체](../../../ado/reference/ado-api/field-object.md)|[Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)|[속성 개체(ADO)](../../../ado/reference/ado-api/property-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목  
 [형식 속성 예제 (필드) (VB)](../../../ado/reference/ado-api/type-property-example-field-vb.md)   
 [형식 속성 예제 (속성) (VC + +)](../../../ado/reference/ado-api/type-property-example-property-vc.md)   
 [RecordType 속성 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 속성(ADO 스트림)](../../../ado/reference/ado-api/type-property-ado-stream.md)
