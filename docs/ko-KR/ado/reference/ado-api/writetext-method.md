---
title: WriteText 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dda7b8a8aa215f43cadfc080a1d0df24b7c94e0d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="writetext-method"></a>WriteText 메서드
에 지정 된 텍스트 문자열을 쓰고는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *데이터*  
 A **문자열** 쓸 문자에 텍스트를 포함 하는 값입니다.  
  
 *옵션*  
 (선택 사항) A [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) 지정된 된 문자열의 끝에 줄 구분 기호 문자를 작성 해야 하는지 여부를 지정 하는 값입니다.  
  
## <a name="remarks"></a>주의  
 지정 된 문자열에 기록 되는 **스트림** 중간 공백이 나 각 문자열 사이 문자 없이 개체입니다.  
  
 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 기록된 된 데이터를 뒤의 문자로 설정 됩니다. **WriteText** 메서드 나머지 스트림에서 데이터를 잘라내지 않습니다. 이러한 문자를 truncate 하려면 호출 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)합니다.  
  
 현재 이전 작성 하는 경우 [EOS](../../../ado/reference/ado-api/eos-property.md) 위치는 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 의 **스트림** 새 문자가 있으면 이러한 문자가 증가 시켜 및 **EOS** 새 마지막 바이트에 들어왔다는 **스트림**합니다.  
  
> [!NOTE]
>  **WriteText** 메서드 텍스트 스트림 함께 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeText**). 이진 스트림에 대 한 (**형식** 은 **adTypeBinary**)를 사용 하 여 [쓰기](../../../ado/reference/ado-api/write-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Write 메서드](../../../ado/reference/ado-api/write-method.md)
