---
title: 속성 (ADO)를 행 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 041356f05daaaef50e6e81d995209ab5379fc901
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192826"
---
# <a name="row-property-ado"></a>Row 속성(ADO)
OLE DB를 가져오거나 설정 합니다. **행** 에서 개체를 [ADORecordConstruction 인터페이스](../../../ado/reference/ado-api/adorecordconstruction-interface.md) 개체입니다. 사용 하는 경우 **put_Row** 설정 하는 **행** 개체를 행 ADO로 바뀝니다 **레코드** 개체입니다.  
  
## <a name="readwritesyntax"></a>Read/write.Syntax  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppRow*  
 OLE DB에 대 한 포인터 **행** 개체입니다.  
  
 *PRow*  
 OLE DB **행** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK와 E_FAIL을 비롯 한 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordConstruction 인터페이스](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
