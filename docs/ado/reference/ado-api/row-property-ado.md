---
description: Row 속성(ADO)
title: Row 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b2862e3f082d42c444b052fcf4a5b493bd192bfe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989394"
---
# <a name="row-property-ado"></a>Row 속성(ADO)
[ADORecordConstruction Interface](./adorecordconstruction-interface.md) 개체의 또는에서 OLE DB **행** 개체를 가져오거나 설정 합니다. **Put_Row** 를 사용 하 여 **행** 개체를 설정 하는 경우에는 행이 ADO **Record** 개체로 설정 됩니다.  
  
## <a name="readwritesyntax"></a>읽기/쓰기. 구문과  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppRow*  
 OLE DB **행** 개체에 대 한 포인터입니다.  
  
 *PRow*  
 OLE DB **행** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK 및 E_FAIL를 포함 하 여 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordConstruction 인터페이스](./adorecordconstruction-interface.md)