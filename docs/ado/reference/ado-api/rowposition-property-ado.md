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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a333a2be2728f3c0b412246b0a793dae64096ae5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931229"
---
# <a name="rowposition-property-ado"></a>RowPosition 속성(ADO)
OLE DB를 가져오거나 설정 합니다. **RowPosition** 간에에서 개체를 **ADORecordsetConstruction** 개체입니다. 사용 하는 경우 **put_RowPosition** 설정 하는 **RowPosition** 개체를 결과 **레코드 집합** 개체에서 사용 하는 **RowPosition** 개체 현재 행을 결정 합니다.  
  
 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppRowPos*  
 OLE DB에 대 한 포인터 **RowPosition** 개체입니다.  
  
 *PRowPos*  
 OLE DB **RowPosition** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK와 E_FAIL을 비롯 한 표준 HRESULT 값을 반환 합니다.  
  
## <a name="remarks"></a>설명  
 경우이 속성이 설정 된 경우는 **행 집합** 에서 개체를 **RowPosition** 개체와 다릅니다.를 **행 집합** 에서 개체를 **레코드집합**이전 재정의 두 번째 개체입니다. 현재는 동일한 동작이 적용 됩니다 **장** 의 합니다 **RowPosition** 도 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
