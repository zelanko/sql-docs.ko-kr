---
title: LoadFromFile 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ff7c5a2a2817fbe93d626ca7883107103edc58cd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66694719"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 메서드(ADO)
에 기존 파일의 내용을 로드를 [Stream](../../../ado/reference/ado-api/stream-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>매개 변수  
 *FileName*  
 A **문자열** 에 로드할 파일의 이름을 포함 하는 값을 **Stream**합니다. *FileName* 모든 유효한 경로 UNC 형식에서 이름을 포함할 수 있습니다. 지정 된 파일이 없으면 런타임 오류가 발생 합니다.  
  
## <a name="remarks"></a>Remarks  
 로컬 파일의 내용을 로드 하려면이 메서드를 사용할 수는 **Stream** 개체입니다. 이 서버에 로컬 파일의 콘텐츠를 업로드할 수 있습니다.  
  
 합니다 **Stream** 개체를 호출 하기 전에 열려 있어야 이미 **LoadFromFile**합니다. 이 메서드는 바인딩을 변경 하지는 **Stream** 개체 URL에서 지정 된 개체에 여전히 바인딩되어 됩니다 또는 **레코드** 있는 **Stream** 원래 열립니다.  
  
 **LoadFromFile** 의 현재 내용을 덮어씁니다 합니다 **Stream** 파일에서 읽은 데이터를 사용 하 여 개체입니다. 모든 기존 바이트는 **Stream** 파일의 내용을 덮어씁니다. 다음 이전에 기존 하 고 나머지 바이트는 [EOS](../../../ado/reference/ado-api/eos-property.md) 에서 만든 **LoadFromFile**, 잘립니다.  
  
 호출한 후 **LoadFromFile**, 현재 위치가 시작 부분에 설정 되는 **Stream** ([위치](../../../ado/reference/ado-api/position-property-ado.md) 0).  
  
 2 바이트 인코딩에 스트림의 시작 부분에 추가할 수 있으므로 스트림의 크기 로드 된 파일의 크기를 정확 하 게 일치할 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
