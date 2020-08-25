---
description: Type 속성(ADO 스트림)
title: Type 속성 (ADO 스트림) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: rothja
ms.author: jroth
ms.openlocfilehash: 5aebb29d8434c152c0a95f04a5eb083847cf9877
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777112"
---
# <a name="type-property-ado-stream"></a>Type 속성(ADO 스트림)
[스트림에](./stream-object-ado.md) 포함 된 데이터의 형식 (이진 또는 텍스트)을 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 **스트림** 개체에 포함 된 데이터의 형식을 지정 하는 [StreamTypeEnum](./streamtypeenum.md) 값을 설정 하거나 반환 합니다. 기본값은 **adTypeText**입니다. 그러나 처음에는 이진 데이터를 비어 있는 새 **스트림에**쓰면 **형식이** **adtypebinary**로 변경 됩니다.  
  
## <a name="remarks"></a>설명  
 **형식** 속성은 현재 위치가 **스트림의** 시작 부분에 있는 경우 ([위치](./position-property-ado.md) 는 0) 다른 위치에서 읽기 전용 인 경우에만 읽기/쓰기입니다.  
  
 **Type** 속성은 **스트림을**읽고 쓰는 데 사용할 메서드를 결정 합니다. 텍스트 **스트림의**경우 [ReadText](./readtext-method.md) 및 [WriteText](./writetext-method.md)를 사용 합니다. 이진 **스트림의**경우 [읽기](./read-method.md) 및 [쓰기](./write-method.md)를 사용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [RecordType 속성 (ADO)](./recordtype-property-ado.md)   
 [Type 속성(ADO)](./type-property-ado.md)