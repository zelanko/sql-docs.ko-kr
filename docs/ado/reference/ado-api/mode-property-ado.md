---
title: "Mode 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ee4463749e231b6ecd48a1fa24af1a72b3766ef
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="mode-property-ado"></a>Mode 속성 (ADO)
데이터 수정에 대 한 사용할 수 있는 권한을 나타냅니다는 [연결](../../../ado/reference/ado-api/connection-object-ado.md), [레코드](../../../ado/reference/ado-api/record-object-ado.md), 또는 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체입니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) 값입니다. 에 대 한 기본값을 **연결** 은 **adModeUnknown**합니다. 에 대 한 기본값을 **레코드** 개체가 **adModeRead**합니다. 에 대 한 기본값은 **스트림** 원본에 연결 된 (원본으로 또는 기본적으로 URL을 사용 하 여 열린 **스트림** 의 **레코드**)은 ** adModeRead**합니다. 에 대 한 기본값은 **스트림** 에서 원본에 연결 되지 않은 소스 (메모리에서 시작)는 **adModeUnknown**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **모드** 속성을 설정 하거나 현재 연결에서 공급자가 사용 중인 액세스 권한을 반환 합니다. 설정할 수 있습니다는 **모드** 속성 경우에만 **연결** 개체가 닫혀 있습니다.  
  
 에 대 한는 **스트림** 개체를 여는 데 사용 하는 소스에서 상속 된 액세스 모드를 지정 하지 않은 경우는 **스트림** 개체입니다. 예를 들어 경우는 **스트림** 에서 열린는 **레코드** 같은 모드에서 열릴 기본적으로 개체는 **레코드**합니다.  
  
 개체가 있는 동안 닫혀 있고 읽기 전용 개체가 열려 있는 동안이 속성은 읽기/쓰기입니다.  
  
> [!NOTE]
>  **원격 데이터 서비스 사용** 클라이언트 쪽에서 사용할 때 **연결** 개체는 **모드** 속성 설정할 수 있습니다 **adModeUnknown**합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[레코드 개체(ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[스트림 개체(ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [IsolationLevel 및 모드 속성 예제 (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 및 모드 속성 예제 (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   

