---
title: SetEOS 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 027468926d444b25e60ede18bbfb26ff7cedf729
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711402"
---
# <a name="seteos-method"></a>SetEOS 메서드
스트림의 끝에 있는 위치를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>Remarks  
 **SetEOS** 의 값을 업데이트 합니다 [EOS](../../../ado/reference/ado-api/eos-property.md) 속성을 현재 수행 [위치](../../../ado/reference/ado-api/position-property-ado.md) 스트림의 맨 끝입니다. 모든 바이트 또는 현재 위치를 다음 문자는 잘립니다.  
  
 때문에 [작성할](../../../ado/reference/ado-api/write-method.md)를 [WriteText](../../../ado/reference/ado-api/writetext-method.md), 및 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 기존에 다른 값을 잘라내지 않습니다 **Stream** 개체를 이러한 잘라낼 수 있습니다 새 스트림 끝 위치를 설정 하 여 문자 또는 바이트 **SetEOS**합니다.  
  
> [!CAUTION]
>  설정 하는 경우 **EOS** 스트림의 실제 종료 되기 전에 위치로 새 후 모든 데이터는 손실 됩니다 **EOS** 위치 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
