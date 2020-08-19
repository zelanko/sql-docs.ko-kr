---
description: Stat 메서드
title: Stat 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: rothja
ms.author: jroth
ms.openlocfilehash: 5375335fe0964107aed54de71d7e700b0588f209
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441995"
---
# <a name="stat-method"></a>Stat 메서드
[스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에 대 한 정보를 검색 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Return Value  
 작업 상태를 나타내는 **Long** 값입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *StatStg*  
 스트림에 대 한 정보로 채워질 STATSTG 구조체입니다. ADO Stream 개체에서 사용 하는 **Stat** 메서드의 구현은 구조의 모든 필드를 채우지 않습니다.  
  
 *StatFlag*  
 이 메서드가 STATSTG 구조체의 일부 멤버를 반환 하지 않도록 지정 하 여 메모리 할당 작업을 저장 하도록 지정 합니다. 값은 STATFLAG 열거형에서 가져옵니다. STATFLAG 열거형에는 두 개의 값이 있습니다.  
  
|상수|값|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>설명  
 ADO Stream 개체에 대해 구현 된 Stat 메서드 버전은 STATSTG 구조의 다음 필드를 채웁니다.  
  
 *pwcsName*  
 스트림의 이름을 포함 하는 문자열입니다 (사용 가능한 경우, STATFLAG_NONAME StatFlag 값이 지정 되지 않은 경우).  
  
 *cbSize*  
 스트림 또는 바이트 배열의 크기를 바이트 단위로 지정합니다.  
  
 *mtime*  
 이 스토리지, 스트림 또는 바이트 배열에 대한 최종 수정 시간을 나타냅니다.  
  
 *ctime*  
 이 스토리지, 스트림 또는 바이트 배열을 만든 시간을 나타냅니다.  
  
 *atime*  
 이 스토리지, 스트림 또는 바이트 배열에 대한 최종 액세스 시간을 나타냅니다.  
  
 StatFlag 매개 변수에 STATFLAG_NONAME 지정 된 경우에는 스트림 이름이 반환 되지 않습니다.  
  
 StatFlag 매개 변수에 STATFLAG_NONAME 지정 되지 않은 경우 현재 스트림에 사용할 수 있는 이름이 없으면이 값이 E_NOTIMPL 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
