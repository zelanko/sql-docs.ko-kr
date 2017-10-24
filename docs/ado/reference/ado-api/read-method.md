---
title: "Read 메서드 | Microsoft Docs"
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
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 23eeee5244ccb92159c2afbc3ffb55fb586ff2f9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="read-method"></a>Read 메서드
이진 파일에서 지정 된 바이트 수를 읽고 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *NumBytes*  
 (선택 사항) A **긴** 파일에서 읽을 바이트 수를 지정 하는 값 또는 [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) 값 **adReadAll**, 기본값입니다.  
  
## <a name="return-value"></a>반환 값  
 **읽기** 메서드는 지정된 된 수의 바이트 또는에서 전체 스트림을 읽습니다는 **스트림** 개체 하 고 결과 데이터를 반환할는 **Variant**합니다.  
  
## <a name="remarks"></a>주의  
 경우 *NumBytes* 보다 많은 바이트 수에 남아 있는 **스트림**, 남아 있는 바이트만 반환 됩니다. 로 지정 된 길이 일치 하도록 읽은 데이터는 채워지지 않습니다 *NumBytes*합니다. 왼쪽에서 읽을 바이트가 없을 경우 null 값을 가진 variant 반환 됩니다. **읽기** 뒤로 읽는 데 사용할 수 없습니다.  
  
> [!NOTE]
>  *NumBytes* 항상 바이트를 측정 합니다. 텍스트에 대 한 **스트림** 개체 ([형식](../../../ado/reference/ado-api/type-property-ado-stream.md) 은 **adTypeText**)를 사용 하 여 [ReadText](../../../ado/reference/ado-api/readtext-method.md)합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [ReadText 메서드](../../../ado/reference/ado-api/readtext-method.md)

