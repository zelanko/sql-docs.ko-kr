---
title: "LoadFromFile 메서드 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Stream::raw_LoadFromFile
helpviewer_keywords: LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c50565a087c9323a7f4dbafb9c604a42a19e1179
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 메서드 (ADO)
에 기존 파일의 내용을 로드는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>매개 변수  
 *FileName*  
 A **문자열** 에 로드 될 파일의 이름을 포함 하는 값은 **스트림**합니다. *FileName* 모든 유효한 경로 UNC 형식에서 이름을 포함할 수 있습니다. 지정된 된 파일이 없는 경우 런타임 오류가 발생 합니다.  
  
## <a name="remarks"></a>주의  
 이 메서드는 로컬 파일의 내용을 로드 데 사용할 수는 **스트림** 개체입니다. 서버에 로컬 파일의 콘텐츠를 업로드 데 될 수 있습니다.  
  
 **스트림** 개체를 호출 하기 전에 열려 있어야 이미 **LoadFromFile**합니다. 이 메서드는의 바인딩을 변경 되지 않습니다는 **스트림** 개체는 여전히 URL에서 지정한 개체에 바인딩할 수 또는 **레코드** 입니다는 **스트림** 원래 열.  
  
 **LoadFromFile** 의 현재 내용을 덮어씁니다는 **스트림** 개체 파일에서 읽은 데이터를 사용 합니다. 기존 바이트는 **스트림** 파일의 내용을 덮어씁니다. 다음 이전에 기존 및 나머지 바이트는 [EOS](../../../ado/reference/ado-api/eos-property.md) 에서 만든 **LoadFromFile**, 잘립니다.  
  
 호출한 후 **LoadFromFile**, 현재 위치를 맨 앞으로 설정 되는 **스트림** ([위치](../../../ado/reference/ado-api/position-property-ado.md) 은 0).  
  
 인코딩에 대 한 스트림의 시작 부분에 2 바이트를 추가할 수 있습니다, 때문에 스트림의 크기를 다 로드 된 파일의 크기입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
