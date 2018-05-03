---
title: ADORecordsetConstruction 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4692187f3d47f2fde3ce0c5521066fa8b68735d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 인터페이스
**ADORecordsetConstruction** 인터페이스 사용 하는 ADO 생성 **레코드 집합** OLE DB에서 개체 **행 집합** C/c + + 응용 프로그램의 개체입니다.  
  
 이 인터페이스는 다음 속성을 지원합니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[장](../../../ado/reference/ado-api/chapter-property-ado.md)|읽기/쓰기입니다.<br />가져오기/설정 OLE DB **장** 개체에서 /이 ADO에 **레코드 집합** 개체입니다.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|읽기/쓰기입니다.<br />가져오기/설정 OLE DB **RowPosition** 개체에서 /이 ADO에 **레코드 집합** 개체입니다.|  
|[행 집합](../../../ado/reference/ado-api/rowset-property-ado.md)|읽기/쓰기입니다.<br />가져오기/설정 OLE DB **행 집합** 개체에서 /이 ADO에 **레코드 집합** 개체입니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>주의  
 OLE DB를 제공 **행 집합** 개체 (`pRowset`), ADO의 생성 **레코드 집합** 개체 (`adoRs`) 다음 세 가지 기본 작업입니다.  
  
1.  ADO 만들기 **레코드 집합** 개체:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  쿼리는 **IADORecordsetConstruction** 에 대 한 인터페이스는 **레코드 집합** 개체:  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  호출 된 `IADORecordsetConstruction::put_Rowset` 속성은 OLE DB를 설정 하는 방법은 `Rowset` ADO 개체 `Recordset` 개체:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 결과 `adoRs` 개체는 이제 ADO 나타냅니다 **레코드 집합** OLE DB에서 생성 된 개체 **행 집합** 개체입니다.  
  
 ADO를 생성할 수도 있습니다 **레코드 집합** OLE DB에서 개체 **장** 또는 **RowPosition** 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>관련 항목:  
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 속성(ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
