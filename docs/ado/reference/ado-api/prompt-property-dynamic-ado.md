---
title: "동적 속성 (ADO)를 확인 합니다. | Microsoft Docs"
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
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 065656ea3023b1526573a48cd6d7d21eee6f6179
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="prompt-property-dynamic-ado"></a>Prompt 속성 동적 (ADO)
OLE DB 공급자에 게 초기화 정보 메시지를 표시 하는지 여부를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하 고 반환 된 [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) 값입니다.  
  
## <a name="remarks"></a>주의  
 **프롬프트** 은에 추가할 수 있는 동적 속성은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) OLE DB 공급자별으로 컬렉션입니다. OLE DB 공급자는 초기화 정보에 대 한 메시지를 표시 하려면 사용자에 게 대화 상자를 일반적으로 표시 됩니다.  
  
 동적 속성은 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 손실 되는 경우는 **연결** 닫혀 있습니다. **프롬프트** 다시 열기 전에 속성을 다시 설정 해야는 **연결** 기본값 이외의 값을 사용 하도록 합니다.  
  
> [!NOTE]
>  공급자는 사용자 됩니다 대화 상자에 응답할 수 없게 하는 시나리오에서 사용자를 메시지를 표시를 지정 하지 마십시오. 예를 들어 사용자 응용 프로그램 사용자의 클라이언트가 아닌 서버 시스템에서 실행 중인 경우 또는 응용 프로그램 로그온 한 사용자와 시스템에서 실행 중인 경우 응답할 수 없게 됩니다. 이러한 경우 응용 프로그램이 응답을 받기 위해 무기한 대기 되며 잠그는 것 같습니다.  
  
## <a name="usage"></a>사용법  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)

