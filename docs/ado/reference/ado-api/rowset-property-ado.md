---
title: Rowset 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 922f6690679d86bdb6cdafb721e3a5ed6bb674ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67917118"
---
# <a name="rowset-property-ado"></a>Rowset 속성(ADO)
**ADORecordsetConstruction** 개체에서/에 대 한 OLE DB **행 집합** 개체를 가져오거나 설정 합니다. Put_Rowset 사용 하는 경우 행 집합은 ADO **레코드 집합** 개체로 전환 됩니다.  
  
 읽기/쓰기입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>매개 변수  
 *ppRowset*  
 OLE DB **행 집합** 개체에 대 한 포인터입니다.  
  
 *PRowset*  
 OLE DB **행 집합** 개체입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK 및 E_FAIL를 포함 하 여 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordsetConstruction 인터페이스](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
