---
title: 스트림 속성이 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85df7a816f04d6247cb0524e354546322dbf3066
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="stream-property"></a>스트림 속성
OLE DB를 가져오거나 설정 합니다. **스트림** 에/에서 개체는 **ADOStreamConstruction** 개체입니다.  
  
 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppStream*  
 OLE DB에 대 한 포인터 **스트림** 개체입니다.  
  
 *pStream*  
 OLE DB **스트림** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 표준 HRESULT 값을 반환합니다. S_OK와 E_FAIL이 포함 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADOStreamConstruction 인터페이스](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
