---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3d9ab76d2f2ed1a6f5dbeaf58be7d2f919acd3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932541"
---
# <a name="flush-method-ado"></a>Flush 메서드(ADO)
내용을 강제로 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 는 기본 개체를 ADO 버퍼에에서 남아 있는 **Stream** 연결 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>설명  
 이 메서드는 스트림 버퍼의 내용을 내부 개체를 보내는 데 사용할 수 있습니다: 예를 들어, 노드 또는 파일의 원인이 되는 URL이 나타내는 합니다 **Stream** 개체. 모든 변경 내용을 확인 하려는 경우이 메서드를 호출 해야의 내용에 대 한는 **Stream** 작성 되었습니다. 그러나 ADO를 사용 하 여 일반적으로 필요 없는 호출 **플러시**처럼 ADO 지속적으로 백그라운드에서 최대한 많은 버퍼를 플러시합니다. 변경 내용에는 **Stream** 는 자동으로 변경 될 때까지 캐시 되지 **플러시** 라고 합니다.  
  
 닫기는 **Stream** 사용 하 여 합니다 [닫기](../../../ado/reference/ado-api/close-method-ado.md) 메서드 내용을 플러시합니다를 **Stream** 자동으로 명시적으로 호출 하지 않아도 됩니다 **플러시**직전 **닫기**합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
