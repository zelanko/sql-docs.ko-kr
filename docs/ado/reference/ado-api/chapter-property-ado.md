---
title: Chapter 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 601573a34082f386bfee238308a8f97c41743e4b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239771"
---
# <a name="chapter-property-ado"></a>Chapter 속성(ADO)
OLE DB를 가져오거나 설정 합니다. **장** 간에에서 개체를 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) 개체입니다. 사용 하는 경우 **put_Chapter** 설정 하는 **장** 개체를 행의 하위 집합 ADO로 바뀝니다 [레코드 집합 개체](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 이 설정의 현재 장 합니다 **행 집합**개체입니다. 이 속성은 읽기/쓰기가 가능합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>매개 변수  
 *plChapter*  
 장 핸들에 대 한 포인터입니다.  
  
 *LChapter*  
 장 핸들입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK와 E_FAIL을 비롯 한 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
