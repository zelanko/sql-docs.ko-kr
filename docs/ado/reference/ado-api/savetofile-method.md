---
title: SaveToFile 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2e56178ad306d5b39c2445c391c3bbabe4fc424
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917031"
---
# <a name="savetofile-method"></a>SaveToFile 메서드
[스트림의](../../../ado/reference/ado-api/stream-object-ado.md) 이진 콘텐츠를 파일에 저장 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름도*  
 **스트림의** 내용이 저장 될 파일의 정규화 된 이름을 포함 하는 **문자열** 값입니다. 모든 유효한 로컬 위치나 UNC 값을 통해 액세스할 수 있는 위치에 저장할 수 있습니다.  
  
 *S*  
 새 파일이 아직 없는 경우 **SaveToFile**에 의해 생성 되어야 하는지 여부를 지정 하는 [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) 값입니다. 기본값은 **adSaveCreateNotExists**입니다. 이러한 옵션을 사용 하 여 지정 된 파일이 없는 경우 오류가 발생 하도록 지정할 수 있습니다. **SaveToFile** 가 기존 파일의 현재 내용을 덮어쓰도록 지정할 수도 있습니다.  
  
> [!NOTE]
>  **AdSaveCreateOverwrite** 가 설정 된 경우 기존 파일을 덮어쓰면 **SaveToFile** 는 새 [EOS](../../../ado/reference/ado-api/eos-property.md)다음에 오는 원래 기존 파일에서 모든 바이트를 자릅니다.  
  
## <a name="remarks"></a>설명  
 **SaveToFile** 는 **Stream** 개체의 내용을 로컬 파일에 복사 하는 데 사용할 수 있습니다. **Stream** 개체의 내용이 나 속성은 변경 되지 않습니다. **SaveToFile**를 호출 하기 전에 **Stream** 개체를 열어야 합니다.  
  
 이 메서드는 **Stream** 개체와 해당 원본 간의 연결을 변경 하지 않습니다. **Stream** 개체는 열린 원본 URL 또는 **레코드** 와 계속 연결 됩니다.  
  
 **SaveToFile** 작업 후에는 스트림의 현재 위치 ([위치](../../../ado/reference/ado-api/position-property-ado.md))가 스트림의 시작 부분 (0)으로 설정 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [Open 메서드 (ADO 스트림)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
