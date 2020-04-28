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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67947493"
---
# <a name="writetext-method"></a>WriteText 메서드
지정 된 텍스트 문자열을 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에 씁니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.WriteText Data, Options  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Data*  
 쓸 문자 텍스트를 포함 하는 **문자열** 값입니다.  
  
 *옵션*  
 선택 사항입니다. 지정 된 문자열의 끝에 줄 구분 기호 문자를 써야 하는지 여부를 지정 하는 [Streamwriteenum](../../../ado/reference/ado-api/streamwriteenum.md) 값입니다.  
  
## <a name="remarks"></a>설명  
 지정 된 문자열은 각 문자열 사이에 공백이 나 문자를 넣지 않고 **Stream** 개체에 기록 됩니다.  
  
 현재 [위치](../../../ado/reference/ado-api/position-property-ado.md) 는 쓴 데이터 다음의 문자로 설정 됩니다. **WriteText** 메서드는 스트림의 나머지 데이터를 자르지 않습니다. 이러한 문자를 잘라내는 경우 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)를 호출 합니다.  
  
 현재 [EOS](../../../ado/reference/ado-api/eos-property.md) 위치를 지나서 쓰는 경우 **스트림의** [크기가](../../../ado/reference/ado-api/size-property-ado-stream.md) 새 문자를 포함 하도록 증가 하 고 **EOS** 가 **스트림의**새 마지막 바이트로 이동 합니다.  
  
> [!NOTE]
>  **WriteText** 메서드는 텍스트 스트림과 함께 사용 됩니다 ( **adTypeText**[형식](../../../ado/reference/ado-api/type-property-ado-stream.md) ). 이진 스트림 (**형식이** **adtypebinary**) 인 경우 [Write](../../../ado/reference/ado-api/write-method.md)를 사용 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Write 메서드](../../../ado/reference/ado-api/write-method.md)
