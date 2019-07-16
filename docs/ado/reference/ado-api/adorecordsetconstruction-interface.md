---
title: ADORecordsetConstruction 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e1d14255acd4cc7f18abea1c494353ef970903c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920791"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 인터페이스
합니다 **ADORecordsetConstruction** 인터페이스는 ADO를 만드는 데 사용 됩니다 **레코드 집합** OLE DB 개체 **행 집합** 개체 c에서 /C++ 응용 프로그램입니다.  
  
 이 인터페이스는 다음 속성을 지원합니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[장](../../../ado/reference/ado-api/chapter-property-ado.md)|읽기/쓰기입니다.<br />OLE DB를 가져오거나 **장** 개체에서 /이 ADO **레코드 집합** 개체입니다.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|읽기/쓰기입니다.<br />OLE DB를 가져오거나 **RowPosition** 개체에서 /이 ADO **레코드 집합** 개체입니다.|  
|[행 집합](../../../ado/reference/ado-api/rowset-property-ado.md)|읽기/쓰기입니다.<br />OLE DB를 가져오거나 **행 집합** 개체에서 /이 ADO **레코드 집합** 개체입니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>설명  
 OLE DB를 제공 **행 집합** 개체 (`pRowset`), ADO 생성 **레코드 집합** 개체 (`adoRs`) 다음 세 가지 기본 작업에 금액:  
  
1.  ADO를 만듭니다 **레코드 집합** 개체:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  쿼리는 **IADORecordsetConstruction** 에 대 한 인터페이스를 **Recordset** 개체:  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  호출 된 `IADORecordsetConstruction::put_Rowset` OLE DB를 설정 하려면 속성 메서드 `Rowset` ADO 개체 `Recordset` 개체:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 결과 `adoRs` 개체에는 이제 ADO 나타냅니다 **레코드 집합** OLE DB에서 생성 된 개체 **행 집합** 개체입니다.  
  
 ADO를 생성할 수도 있습니다 **Recordset** OLE DB 개체 **장** 또는 **RowPosition** 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>관련 항목  
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 속성(ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
