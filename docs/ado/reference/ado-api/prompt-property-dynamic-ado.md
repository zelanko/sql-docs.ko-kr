---
title: Prompt 속성-동적 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4f2c778a6e922477cd8b21251a638d430ce15480
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703161"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 속성-동적(ADO)
OLE DB 공급자 초기화 정보에 대 한 사용자 메시지를 표시 하는지 여부를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하 고 반환 된 [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) 값입니다.  
  
## <a name="remarks"></a>Remarks  
 **프롬프트** 에 추가할 수 있습니다는 동적 속성은 합니다 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) OLE DB 공급자를 사용 하 여 컬렉션입니다. OLE DB 공급자는 초기화 정보를 묻는 메시지를 사용자에 게 대화 상자를 일반적으로 표시 됩니다.  
  
 동적 속성을 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 손실 되는 경우를 **연결** 닫혀 있습니다. **프롬프트** 다시 열기 전에 속성 다시 설정 해야 합니다 **연결** 기본값 이외의 값을 사용 하도록 합니다.  
  
> [!NOTE]
>  공급자는 사용자 됩니다 대화 상자에 대처할 수 있도록 하는 시나리오에서 사용자를 메시지를 표시를 지정 하지 마십시오. 예를 들어 사용자 응용 프로그램 사용자의 클라이언트 대신 서버 시스템에서 실행 중인 경우 또는 응용 프로그램 로그온 한 사용자를 사용 하 여 시스템에서 실행 중인 경우에 응답할 수 없습니다. 이러한 경우 응용 프로그램 응답을 무기한 대기 되며를 잠그는 것 같습니다.  
  
## <a name="usage"></a>사용법  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
