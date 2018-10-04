---
title: Type 속성 (ADO Stream) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e4df670c5fe6ca42015e7e85445dafde47738f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637041"
---
# <a name="type-property-ado-stream"></a>Type 속성(ADO 스트림)
에 포함 된 데이터의 형식을 나타내는 합니다 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) (이진 또는 텍스트)입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) 에 포함 된 데이터의 형식을 지정 하는 값을 **Stream** 개체입니다. 기본값은 **adTypeText**합니다. 그러나 이진 데이터는 처음에 새에 기록 하는 경우 빈 **Stream**의 **유형** 로 변경 됩니다 **adTypeBinary**합니다.  
  
## <a name="remarks"></a>Remarks  
 **형식** 속성은 읽기/쓰기 시작 부분에는 현재 위치 하는 경우에 합니다 **Stream** ([위치](../../../ado/reference/ado-api/position-property-ado.md) 0), 및 다른 위치에서 읽기 전용입니다.  
  
 **형식** 속성을 읽고 쓰기 위한 메서드를 사용할지 결정 합니다 **Stream**합니다. 텍스트에 대 한 **스트림을**를 사용 하 여 [ReadText](../../../ado/reference/ado-api/readtext-method.md) 하 고 [WriteText](../../../ado/reference/ado-api/writetext-method.md)합니다. 이진 **스트림을**를 사용 하 여 [읽기](../../../ado/reference/ado-api/read-method.md) 및 [작성](../../../ado/reference/ado-api/write-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [RecordType 속성 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 속성(ADO)](../../../ado/reference/ado-api/type-property-ado.md)
