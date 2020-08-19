---
description: Flush 메서드(ADO)
title: Flush 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: rothja
ms.author: jroth
ms.openlocfilehash: 67689683faa9d1c0f18049d5a55a83319a69fe4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443615"
---
# <a name="flush-method-ado"></a>Flush 메서드(ADO)
ADO 버퍼에 남아 있는 [스트림의](../../../ado/reference/ado-api/stream-object-ado.md) 내용을 **스트림이** 연결 된 기본 개체에 강제로 적용 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>설명  
 이 메서드를 사용 하 여 스트림 버퍼의 내용을 원본 개체에 보낼 수 있습니다. 예를 들어 **스트림** 개체의 원본인 URL이 나타내는 노드나 파일이 있습니다. **스트림의** 내용에 대 한 모든 변경 내용이 작성 되었는지 확인 하려는 경우이 메서드를 호출 해야 합니다. 그러나 ado를 사용 하는 경우에는 ADO가 백그라운드에서 가능한 한 버퍼를 지속적으로 플러시하는 경우 일반적으로 **플러시**를 호출할 필요가 없습니다. **스트림의** 내용에 대 한 변경 내용은 자동으로 생성 되며 **플러시가** 호출 될 때까지 캐시 되지 않습니다.  
  
 [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드를 사용 하 여 **스트림을** 닫으면 **스트림의** 내용이 자동으로 플러시됩니다. **닫기**바로 전에 **플러시** 를 명시적으로 호출할 필요가 없습니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
