---
title: "SetEOS 메서드 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 40e2cc70b9505ba99a9ac17ebfd54f8d2cf8b401
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="seteos-method"></a>SetEOS 메서드
다음 위치를 스트림의 끝을 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>주의  
 **SetEOS** 의 값이 업데이트는 [EOS](../../../ado/reference/ado-api/eos-property.md) 현재 함으로써 속성 [위치](../../../ado/reference/ado-api/position-property-ado.md) 스트림의 끝입니다. 모든 바이트 또는 현재 위치를 다음 문자는 잘립니다.  
  
 때문에 [쓰기](../../../ado/reference/ado-api/write-method.md), [WriteText](../../../ado/reference/ado-api/writetext-method.md), 및 [CopyTo](../../../ado/reference/ado-api/copyto-method-ado.md) 기존에서 모든 추가 값을 잘라내지 않습니다 **스트림** 개체를 이러한을 잘라낼 수 있습니다 새 스트림 끝 위치를 설정 하 여 문자 또는 바이트 **SetEOS**합니다.  
  
> [!CAUTION]
>  설정한 경우 **EOS** 스트림의 실제 끝 이전 위치로 새 후 모든 데이터는 손실 됩니다 **EOS** 위치입니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)

