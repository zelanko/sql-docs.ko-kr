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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917031"
---
# <a name="savetofile-method"></a>SaveToFile 메서드
이진 내용을 저장 한 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 파일로.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>매개 변수  
 *FileName*  
 A **문자열** 파일의 정규화 된 이름을 포함 하는 값의 내용을 합니다 **Stream** 저장 됩니다. 모든 유효한 로컬 위치에 저장할 수 있습니다 또는 UNC 값을 통해 액세스할 수 있는 위치입니다.  
  
 *SaveOptions*  
 A [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) 하 여 새 파일을 만들어야 하는지 여부를 지정 하는 값 **SaveToFile**아직 존재 하지 않는 경우. 기본값은 **adSaveCreateNotExists**합니다. 이러한 옵션을 사용 하 여 지정 된 파일이 없는 경우 오류가 발생을 지정할 수 있습니다. 도 지정할 수 있습니다 **SaveToFile** 기존 파일의 현재 내용을 덮어씁니다.  
  
> [!NOTE]
>  기존 파일을 덮어쓰면 (때 **adSaveCreateOverwrite** 설정), **SaveToFile** 새 따르는 원래 기존 파일의 모든 바이트를 자릅니다 [EOS](../../../ado/reference/ado-api/eos-property.md)합니다.  
  
## <a name="remarks"></a>설명  
 **SaveToFile** 의 내용을 복사 하는 데는 **Stream** 로컬 파일에는 개체입니다. 내용이 나 속성의 변경 사항이 없는 합니다 **Stream** 개체입니다. 합니다 **Stream** 개체는 호출 하기 전에 열려 있어야 합니다. **SaveToFile**합니다.  
  
 이 메서드는 연결을 변경 하지는 **Stream** 기본 원본 개체입니다. **Stream** 개체는 원래 URL과 사용 하 여 연결 됩니다 또는 **레코드** 열 때 해당 원본 했습니다.  
  
 후에 **SaveToFile** 작업, 현재 위치 ([위치](../../../ado/reference/ado-api/position-property-ado.md)) 스트림 (0) 스트림의 시작 부분에 설정 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [Open 메서드 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
