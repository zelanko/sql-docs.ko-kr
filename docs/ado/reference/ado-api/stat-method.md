---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 127aab5e00247ce5550f25e2a281e190472b0186
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740343"
---
# <a name="stat-method"></a>Stat 메서드
에 대 한 정보를 검색 한 [Stream](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>반환 값  
 A **긴** 작업의 상태를 나타내는 값입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *StatStg*  
 스트림에 대 한 정보를 사용 하 여 입력 수는 STATSTG 구조체입니다. 구현의 합니다 **Stat** ADO Stream 개체에서 사용 하는 메서드를 모든 구조체의 필드에서 충족할 수 없습니다.  
  
 *StatFlag*  
 이 메서드가 반환 하지 않음을 멤버의 일부 메모리 할당 작업을 저장 하므로 STATSTG 구조에 지정 합니다. 값은 STATFLAG 열거형에서 가져옵니다. STATFLAG 열거형에는 두 값  
  
|상수|값|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Remarks  
 Stat 메서드 ADO Stream 개체에 대 한 구현 버전 STATSTG 구조체의 다음 필드를 채웁니다.  
  
 *pwcsName*  
 사용 가능한 경우 스트림 및 STATFLAG_NONAME StatFlag 값의 이름을 포함 하는 문자열을 지정 하지 않았습니다.  
  
 *cbSize*  
 스트림 또는 바이트 배열의 바이트의 크기를 지정합니다.  
  
 *mtime*  
 이 저장소, 스트림 또는 바이트 배열에 대 한 마지막 수정 시간을 나타냅니다.  
  
 *ctime*  
 이 저장소, 스트림 또는 바이트 배열에 대 한 생성 시간을 나타냅니다.  
  
 *atime*  
 이 스토리지, 스트림 또는 바이트 배열에 대한 최종 액세스 시간을 나타냅니다.  
  
 STATFLAG_NONAME StatFlag 매개 변수에 지정 된 경우에 스트림의 이름을 반환 되지 않습니다.  
  
 STATFLAG_NONAME StatFlag 매개 변수에 지정 되지 않았고 현재 스트림에 대 한 사용 가능한 이름은, E_NOTIMPL이 값이 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
