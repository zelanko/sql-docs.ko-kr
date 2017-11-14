---
title: "Stat 메서드 | Microsoft Docs"
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
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c19b5bed54d4bbb27a5aeb235b0e4ab529b9c836
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="stat-method"></a>Stat 메서드
에 대 한 정보를 검색 한 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>반환 값  
 A **긴** 작업의 상태를 나타내는 값입니다.  
  
#### <a name="parameters"></a>매개 변수  
 *StatStg*  
 STATSTG 구조체 스트림에 대 한 정보를 사용 하 여 채울 수입니다. 구현에서 **Stat** ADO 스트림 개체에서 사용 되는 방법을 모든 구조체의 필드를 채우지 합니다.  
  
 *StatFlag*  
 이 메서드가 반환 하지 않도록 지정 일부 멤버 STATSTG 구조에서 메모리 할당 작업을 저장 합니다. 값은 STATFLAG 열거형에서 가져옵니다. STATFLAG 열거형에는 두 개의 값  
  
|상수|값|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1.|  
  
## <a name="remarks"></a>주의  
 STATSTG 구조의 다음 필드 ADO 스트림 개체에 대 한 구현 Stat 메서드 버전을 채웁니다.  
  
 *pwcsName*  
 사용 가능한 경우, 스트림 및 STATFLAG_NONAME StatFlag 값의 이름을 포함 하는 문자열을 지정 하지 않았습니다.  
  
 *cbSize*  
 스트림 또는 바이트 배열의 바이트 크기를 지정합니다.  
  
 *mtime*  
 이 저장소, 스트림 또는 바이트 배열에 대 한 마지막 수정 시간을 나타냅니다.  
  
 *ctime*  
 이 저장소, 스트림 또는 바이트 배열에 대 한 생성 시간을 나타냅니다.  
  
 *은*  
 이 저장소, 스트림 또는 바이트 배열에 대 한 마지막 액세스 시간을 나타냅니다.  
  
 STATFLAG_NONAME StatFlag 매개 변수에 지정 된 경우에 스트림의 이름은 반환 되지 않습니다.  
  
 STATFLAG_NONAME StatFlag 매개 변수에서 지정 되지 않았고 현재 스트림에 대해 사용할 수 있는 이름이, E_NOTIMPL이 값이 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)

