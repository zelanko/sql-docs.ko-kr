---
title: "장 속성 (ADO) | Microsoft Docs"
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
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 766166a48b1d702d9f3550d22bcb40823728c16b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="chapter-property-ado"></a>장 속성 (ADO)
OLE DB를 가져오거나 설정 합니다. **장** 에/에서 개체는 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) 개체입니다. 사용 하는 경우 **put_Chapter** 설정 하는 **장** 개체, 행의 하위 집합 ADO로 변경 됩니다 [Recordset 개체](../../../ado/reference/ado-api/recordset-object-ado.md) 개체입니다. 이 설정의 현재 장은 **행 집합**개체입니다. 이 속성은 읽기/쓰기가 가능합니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>매개 변수  
 *plChapter*  
 장 핸들에 대 한 포인터입니다.  
  
 *LChapter*  
 장의 핸들입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK와 E_FAIL을 포함 하는 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
