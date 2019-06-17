---
title: ParentRow 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 180ab01d28cb5c6f7715480459eeb12ab6ea81be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703287"
---
# <a name="parentrow-property-ado"></a>ParentRow 속성(ADO)
OLE DB의 컨테이너를 설정 **행** 에서 개체를 **ADORecordConstruction** 개체를 부모 행의 ADO에 켜져 있도록 **레코드** 개체입니다.  
  
 쓰기 전용입니다.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>매개 변수  
 *pParent*  
 행의 컨테이너입니다.  
  
## <a name="return-values"></a>반환 값  
 이 속성 메서드는 S_OK와 E_FAIL을 비롯 한 표준 HRESULT 값을 반환 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [ADORecordConstruction 인터페이스](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
