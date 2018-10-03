---
title: ADORecordConstruction 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21975fb2442aea97e362cd71b24c087f58addc0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686871"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 인터페이스
합니다 **ADORecordConstruction**인터페이스는 ADO를 만드는 데 사용 됩니다 **레코드** OLE DB 개체 **행** C/c + + 응용 프로그램에서 개체입니다.  
  
 이 인터페이스는 다음 속성을 지원합니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|쓰기 전용입니다.<br />OLE DB의 컨테이너를 설정 **행** 개체의이 ADO **레코드** 개체입니다.|  
|[행](../../../ado/reference/ado-api/row-property-ado.md)|읽기/쓰기입니다.<br />OLE DB를 가져오거나 **행** 개체에서 /이 ADO **레코드** 개체입니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>Remarks  
 OLE DB를 제공 **행** 개체 (`pRow`), ADO 생성 **레코드** 개체 (`adoR`), 다음 세 가지 기본 작업에 금액:  
  
1.  ADO를 만듭니다 **레코드** 개체:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  쿼리는 **IADORecordConstruction** 에 대 한 인터페이스를 **레코드** 개체:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  호출 된 **IADORecordConstruction::put_Row** OLE DB를 설정 하려면 속성 메서드 **행** ADO 개체 **레코드** 개체:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 결과 **adoR** 개체에는 이제 ADO 나타냅니다 **레코드** OLE DB에서 생성 된 개체 **행** 개체입니다.  
  
 ADO **레코드** OLE DB의 컨테이너에서 개체를 생성할 수도 있습니다 **행** 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
