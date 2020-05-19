---
title: RowPosition 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
author: rothja
ms.author: jroth
ms.openlocfilehash: f2621e82fef8d7e9baffa9d6cc8c30c65ea476ea
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756205"
---
# <a name="rowposition-property-ado"></a>RowPosition 속성(ADO)
**ADORecordsetConstruction** 개체에서/에 대 한 OLE DB **rowposition** 개체를 가져오거나 설정 합니다. **Put_RowPosition** 를 사용 하 여 **rowposition** 개체를 설정 하는 경우 결과 **레코드 집합** 개체는 **rowposition** 개체를 사용 하 여 현재 행을 확인 합니다.  
  
 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppRowPos*  
 OLE DB **Rowposition** 개체에 대 한 포인터입니다.  
  
 *PRowPos*  
 OLE DB **Rowposition** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK 및 E_FAIL를 포함 하 여 표준 HRESULT 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 이 속성이 설정 된 경우 **Rowposition** 개체의 **rowset** 개체가 **레코드** 집합 개체의 **rowset** 개체와 다르면 이전에서 후자를 재정의 합니다. **Rowposition** 의 현재 **챕터** 에도 동일한 동작이 적용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
