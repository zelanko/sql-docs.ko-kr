---
title: Flush 메서드 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 931d8a2546c9a4d5c41d6b2348a7db5d9ad312ef
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278772"
---
# <a name="flush-method-ado"></a>Flush 메서드 (ADO)
내용을 강제로 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 원본 개체는 ADO 버퍼에에서 남아 있는 **스트림** 연결 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Remarks  
 이 메서드는 스트림 버퍼의 내용을 내부 개체를 보내는 데 사용할 수 있습니다: 예를 들어 노드 또는 파일의 원본이 URL이 나타내는 **스트림** 개체입니다. 모든 있는 변경 되는지 확인 하려는 경우이 메서드를 호출 해야의 내용에 대 한는 **스트림** 썼는지 합니다. 그러나 ADO 이므로 없이 호출할 필요가 **플러시**와 ADO 지속적으로 백그라운드에서 가능한 한 버퍼를 플러시합니다. 변경 내용에는 **스트림** 은 자동으로 변경 될 때까지 캐시 되지 **플러시** 호출 됩니다.  
  
 닫기는 **스트림** 와 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드 플러시합니다의 콘텐츠는 **스트림** 자동으로; 있는 명시적으로 호출할 필요가 없습니다 **플러시**직전 **닫기**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
