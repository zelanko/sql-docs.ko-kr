---
title: SaveToFile 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9beb8a1e2bfcc307c93b293a35dcac26cf0847a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="savetofile-method"></a>SaveToFile 메서드
이진 내용을 저장 한 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 파일에 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>매개 변수  
 *FileName*  
 A **문자열** 대상 파일의 정규화 된 이름을 포함 하는 값의 내용을 **스트림** 저장 됩니다. 유효한 모든 로컬 위치에 저장할 수 있습니다 또는 UNC 값을 통해 액세스할 수 있는 모든 위치입니다.  
  
 *SaveOptions*  
 A [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) 하 여 새 파일을 만들어야 하는지 여부를 지정 하는 값 **SaveToFile**아직 없는 경우. 기본값은 **adSaveCreateNotExists**합니다. 이 옵션으로 지정 된 파일이 존재 하지 않는 경우 오류가 발생을 지정할 수 있습니다. 지정할 수 **SaveToFile** 기존 파일의 현재 내용을 덮어씁니다.  
  
> [!NOTE]
>  기존 파일을 덮어쓰면 (때 **adSaveCreateOverwrite** 설정), **SaveToFile** 새 다음에 나오는 원래 기존 파일의 모든 바이트를 자릅니다 [EOS](../../../ado/reference/ado-api/eos-property.md)합니다.  
  
## <a name="remarks"></a>주의  
 **SaveToFile** 의 내용을 복사 하는 데 사용 될 수 있습니다는 **스트림** 로컬 파일에는 개체입니다. 내용이 나 속성의 변경 내용이 없는지는 **스트림** 개체입니다. **스트림** 개체가 호출 하기 전에 열려 있어야 **SaveToFile**합니다.  
  
 이 메서드는의 연결을 변경 하지 않습니다는 **스트림** 원본의 개체입니다. **스트림** 개체 원래 URL과 연결 됩니다 또는 **레코드** 를 열 때 해당 원본이 있습니다.  
  
 이후에 **SaveToFile** 작업, 현재 위치 ([위치](../../../ado/reference/ado-api/position-property-ado.md)) 스트림이 스트림 (0)의 시작 부분으로 설정 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
