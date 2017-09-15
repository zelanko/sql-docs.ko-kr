---
title: "Type 속성 (ADO 스트림) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b16d683d9e5460e5aba904a8bc4ccc7362b2287
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="type-property-ado-stream"></a>Type 속성 (ADO 스트림)
에 포함 된 데이터의 유형을 나타냅니다는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) (이진 또는 텍스트)입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) 값에 포함 된 데이터의 형식을 지정 하는 **스트림** 개체입니다. 기본값은 **adTypeText**합니다. 그러나 처음에 새 이진 데이터를 작성 한 경우 빈 **스트림**, **형식** 로 변경 됩니다 **adTypeBinary**합니다.  
  
## <a name="remarks"></a>주의  
 **형식** 현재 위치가의 시작 부분에 있는 경우에 속성은 읽기/쓰기는 **스트림** ([위치](../../../ado/reference/ado-api/position-property-ado.md) 은 0), 다른 위치에서 읽기 전용입니다.  
  
 **형식** 속성 읽기 및 쓰기에 어떤 방법을 사용 해야 결정는 **스트림**합니다. 텍스트에 대 한 **스트림을**를 사용 하 여 [ReadText](../../../ado/reference/ado-api/readtext-method.md) 및 [WriteText](../../../ado/reference/ado-api/writetext-method.md)합니다. 이진 파일에 대해 **스트림을**를 사용 하 여 [읽기](../../../ado/reference/ado-api/read-method.md) 및 [쓰기](../../../ado/reference/ado-api/write-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [RecordType 속성 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 속성(ADO)](../../../ado/reference/ado-api/type-property-ado.md)
