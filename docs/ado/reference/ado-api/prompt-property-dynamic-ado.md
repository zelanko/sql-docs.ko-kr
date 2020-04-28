---
title: Prompt 속성-Dynamic (ADO) | Microsoft Docs
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
ms.openlocfilehash: cde7a5ad0324bc7d5cde5e1a794eeb9e2cb3381a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931585"
---
# <a name="prompt-property-dynamic-ado"></a>Prompt 속성-동적(ADO)
OLE DB 공급자가 초기화 정보를 묻는 메시지를 사용자에 게 표시할지 여부를 지정 합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) 값을 설정 하 고 반환 합니다.  
  
## <a name="remarks"></a>설명  
 **Prompt** 는 OLE DB 공급자에 의해 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체의 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션에 추가 될 수 있는 동적 속성입니다. 초기화 정보를 요청 하기 위해 OLE DB 공급자는 일반적으로 사용자에 게 대화 상자를 표시 합니다.  
  
 [연결 개체의](../../../ado/reference/ado-api/connection-object-ado.md) 동적 속성은 **연결** 을 닫을 때 손실 됩니다. 기본값 이외의 값을 사용 하려면 **연결** 을 다시 열기 전에 **Prompt** 속성을 다시 설정 해야 합니다.  
  
> [!NOTE]
>  사용자가 대화 상자에 응답할 수 없는 시나리오에서 공급자가 사용자에 게 메시지를 표시 하도록 지정 하지 마십시오. 예를 들어 응용 프로그램이 사용자의 클라이언트 대신 서버 시스템에서 실행 되 고 있거나 사용자가 로그온 하지 않은 시스템에서 실행 되 고 있는 경우 사용자가 응답할 수 없습니다. 이러한 경우 응용 프로그램은 응답을 무기한 대기 하 고 잠금 상태로 보일 것입니다.  
  
## <a name="usage"></a>사용법  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>적용 대상  
 [연결 개체(ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
