---
title: "RowPosition 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords: RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 65bd34a35b48b980cd3d9b6c29dc5e297b732fa3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="rowposition-property-ado"></a>RowPosition 속성 (ADO)
OLE DB를 가져오거나 설정 합니다. **RowPosition** 에/에서 개체는 **ADORecordsetConstruction** 개체입니다. 사용 하는 경우 **put_RowPosition** 설정 하는 **RowPosition** 결과 개체 **레코드 집합** 개체에서 사용 하 여 **RowPosition** 개체를 현재 행을 결정 합니다.  
  
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
 이 속성 메서드는 S_OK와 E_FAIL을 포함 하는 표준 HRESULT 값을 반환 합니다.  
  
## <a name="remarks"></a>주의  
 하는 경우,이 속성이 설정 되어는 **행 집합** 개체에 **RowPosition** 개체 간에 차이가 있는 **행 집합** 개체에 **레코드 집합**전자 재정의 후자 개체입니다. 현재는 동일한 동작이 적용 됩니다. **장** 의 **RowPosition** 도 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
