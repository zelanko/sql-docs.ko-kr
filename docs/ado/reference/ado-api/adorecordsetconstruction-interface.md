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
author: rothja
ms.author: jroth
ms.openlocfilehash: 770bf86f62f243ea255693c7773e6fae48527cfd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747083"
---
# <a name="adorecordsetconstruction-interface"></a>ADORecordsetConstruction 인터페이스
**ADORecordsetConstruction** 인터페이스는 C/c + + 응용 프로그램의 OLE DB **ROWSET** 개체에서 ADO **레코드 집합** 개체를 생성 하는 데 사용 됩니다.  
  
 이 인터페이스는 다음 속성을 지원 합니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[장](../../../ado/reference/ado-api/chapter-property-ado.md)|읽기/쓰기.<br />이 ADO **레코드 집합** 개체의/에서 OLE DB **챕터** 개체를 가져오거나 설정 합니다.|  
|[행 위치](../../../ado/reference/ado-api/rowposition-property-ado.md)|읽기/쓰기.<br />이 ADO **레코드 집합** 개체의 OLE DB **rowposition** 개체를 가져오거나 설정 합니다.|  
|[행 집합](../../../ado/reference/ado-api/rowset-property-ado.md)|읽기/쓰기.<br />이 ADO **레코드 집합** 개체의 OLE DB **행 집합** 개체를 가져오거나 설정 합니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>설명  
 OLE DB **Rowset** 개체 ( `pRowset` )를 지정 하는 경우 다음 세 가지 기본 작업에 대 한 ADO **레코드 집합** 개체 ()가 생성 됩니다 `adoRs` .  
  
1.  ADO **레코드 집합** 개체를 만듭니다.  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  **레코드 집합** 개체에서 **IADORecordsetConstruction** 인터페이스를 쿼리 합니다.  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  `IADORecordsetConstruction::put_Rowset`속성 메서드를 호출 하 여 `Rowset` ADO 개체의 OLE DB 개체를 설정 합니다 `Recordset` .  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 이제 결과 `adoRs` 개체는 OLE DB **Rowset** 개체에서 생성 된 ADO **레코드 집합** 개체를 나타냅니다.  
  
 OLE DB **챕터** 또는 **rowposition** 개체에서 ADO **레코드 집합** 개체를 생성할 수도 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>참고 항목  
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Rowset 속성(ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
