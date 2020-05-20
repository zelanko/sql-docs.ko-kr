---
title: Stream 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
author: rothja
ms.author: jroth
ms.openlocfilehash: cdcd6d9fb734f50c110a3e59e9d24874ea71b974
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759601"
---
# <a name="stream-property"></a>Stream 속성
**ADOStreamConstruction** 개체의/에서 OLE DB **Stream** 개체를 가져오거나 설정 합니다.  
  
 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppStream*  
 OLE DB **Stream** 개체에 대 한 포인터입니다.  
  
 *pStream*  
 OLE DB **Stream** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 표준 HRESULT 값을 반환 합니다. 여기에는 S_OK 및 E_FAIL 포함 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADOStreamConstruction 인터페이스](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
