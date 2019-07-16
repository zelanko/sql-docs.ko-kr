---
title: WriteText 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_WriteText
- _Stream::WriteText
helpviewer_keywords:
- WriteText method [ADO]
ms.assetid: 7a669048-13f4-4574-a2b1-985e089729d5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64b7d8fd3f2220562e3695d6e31c83261daa2e60
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947493"
---
# <a name="writetext-method"></a>WriteText 메서드
에 지정 된 텍스트 문자열을 쓰고를 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *데이터*  
 A **문자열** 쓸 문자에 텍스트를 포함 하는 값입니다.  
  
 *옵션*  
 (선택 사항) A [StreamWriteEnum](../../../ado/reference/ado-api/streamwriteenum.md) 지정된 된 문자열의 끝 줄 구분 기호 문자를 작성 해야 하는지 여부를 지정 하는 값입니다.  
  
## <a name="remarks"></a>설명  
 지정 된 문자열에 기록 되는 **Stream** 중간 공백이 나 문자 각 문자열 사이 없는 개체입니다.  
  
 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 기록된 된 데이터를 다음에 설정 됩니다. 합니다 **WriteText** 메서드 스트림에서 데이터의 나머지 부분을 잘라내지 않습니다. 이러한 문자를 truncate 하려는 경우 호출할 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)합니다.  
  
 현재 이전 작성 하는 경우 [EOS](../../../ado/reference/ado-api/eos-property.md) 위치를 [크기](../../../ado/reference/ado-api/size-property-ado-stream.md) 의 합니다 **Stream** 늘어납니다 새 문자가 포함 될 및 **EOS** 새 마지막 바이트를 이동 합니다 **Stream**합니다.  
  
> [!NOTE]
>  **WriteText** 메서드는 텍스트 스트림 사용 됩니다 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 는 **adTypeText**). 이진 스트림에 대 한 (**형식** 됩니다 **adTypeBinary**)를 사용 하 여 [작성](../../../ado/reference/ado-api/write-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Write 메서드](../../../ado/reference/ado-api/write-method.md)
