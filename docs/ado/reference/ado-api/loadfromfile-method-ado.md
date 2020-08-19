---
description: LoadFromFile 메서드(ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f07bd7bc6b04dac8c5b352cc6281ce4eb851d3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443355"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile 메서드(ADO)
기존 파일의 내용을 [스트림으로](../../../ado/reference/ado-api/stream-object-ado.md)로드 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>매개 변수  
 *FileName*  
 **스트림으로**로드할 파일의 이름을 포함 하는 **문자열** 값입니다. *파일 이름* 에는 UNC 형식의 유효한 경로와 이름이 포함 될 수 있습니다. 지정 된 파일이 없으면 런타임 오류가 발생 합니다.  
  
## <a name="remarks"></a>설명  
 이 메서드는 로컬 파일의 내용을 **스트림** 개체로 로드 하는 데 사용할 수 있습니다. 서버에 로컬 파일의 내용을 업로드 하는 데 사용할 수 있습니다.  
  
 **LoadFromFile**를 호출 하기 전에 **Stream** 개체가 이미 열려 있어야 합니다. 이 메서드는 **Stream** 개체의 바인딩을 변경 하지 않습니다. **스트림이** 원래 열린 URL 또는 **레코드로** 지정 된 개체에 계속 바인딩됩니다.  
  
 **LoadFromFile** 는 **Stream** 개체의 현재 콘텐츠를 파일에서 읽은 데이터로 덮어씁니다. **스트림의** 모든 기존 바이트는 파일의 내용에 의해 덮어쓰여집니다. **LoadFromFile**에 의해 생성 된 [EOS](../../../ado/reference/ado-api/eos-property.md) 뒤의 기존 및 나머지 바이트는 잘립니다.  
  
 **LoadFromFile**를 호출한 후 현재 위치는 **스트림의** 시작 부분으로 설정 됩니다 ([position](../../../ado/reference/ado-api/position-property-ado.md) 은 0).  
  
 인코딩에 대해 2 바이트를 스트림의 시작 부분에 추가할 수 있으므로 스트림의 크기는 로드 된 파일의 크기와 정확 하 게 일치 하지 않을 수 있습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
