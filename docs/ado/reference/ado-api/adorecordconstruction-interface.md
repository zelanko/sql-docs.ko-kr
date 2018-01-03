---
title: "ADORecordConstruction 인터페이스 | Microsoft Docs"
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
f1_keywords: ADORecordConstruction
helpviewer_keywords: ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1cedc7639b0b5c1559fe137be96c822287a3ff82
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 인터페이스
**ADORecordConstruction**인터페이스 사용 하는 ADO 생성 **레코드** OLE DB에서 개체 **행** C/c + + 응용 프로그램의 개체입니다.  
  
 이 인터페이스는 다음 속성을 지원합니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|쓰기 전용입니다.<br />OLE DB의 컨테이너를 설정 **행** 이 ADO 개체 **레코드** 개체입니다.|  
|[행](../../../ado/reference/ado-api/row-property-ado.md)|읽기/쓰기입니다.<br />가져오기/설정 OLE DB **행** 개체에서 /이 ADO에 **레코드** 개체입니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>주의  
 OLE DB를 제공 **행** 개체 (`pRow`), ADO의 생성 **레코드** 개체 (`adoR`), 다음 세 가지 기본 작업입니다.  
  
1.  ADO 만들기 **레코드** 개체:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  쿼리는 **IADORecordConstruction** 에 대 한 인터페이스는 **레코드** 개체:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  호출 된 **IADORecordConstruction::put_Row** 속성은 OLE DB를 설정 하는 방법은 **행** ADO 개체 **레코드** 개체:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 결과 **adoR** 개체는 이제 ADO 나타냅니다 **레코드** OLE DB에서 생성 된 개체 **행** 개체입니다.  
  
 ADO **레코드** OLE DB의 컨테이너에서 개체를 만들 수도 있습니다 **행** 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
