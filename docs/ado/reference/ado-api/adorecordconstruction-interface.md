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
ms.openlocfilehash: c56ba0b9d7ebebbf4a9e4baf669bbdc6eb84355e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920805"
---
# <a name="adorecordconstruction-interface"></a>ADORecordConstruction 인터페이스
**ADORecordConstruction**인터페이스는 C/c + + 응용 프로그램의 OLE DB **ROW** 개체에서 ADO **Record** 개체를 생성 하는 데 사용 됩니다.  
  
 이 인터페이스는 다음 속성을 지원 합니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|쓰기 전용입니다.<br />이 ADO **레코드** 개체에 대 한 OLE DB **Row** 개체의 컨테이너를 설정 합니다.|  
|[행당](../../../ado/reference/ado-api/row-property-ado.md)|읽기/쓰기.<br />이 ADO **레코드** 개체에서/에 대 한 OLE DB **행** 개체를 가져오거나 설정 합니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>설명  
 OLE DB **행** 개체 (`pRow`)가 지정 된 경우 ADO **Record** 개체 (`adoR`)의 생성은 다음 세 가지 기본 작업에 해당 합니다.  
  
1.  ADO **Record** 개체를 만듭니다.  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  **Record** 개체에서 **IADORecordConstruction** 인터페이스를 쿼리 합니다.  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  **IADORecordConstruction::p ut_Row** property 메서드를 호출 하 여 ADO **Record** 개체의 OLE DB **행** 개체를 설정 합니다.  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 이제 결과 **adoR** 개체가 OLE DB **Row** 개체에서 생성 된 ADO **Record** 개체를 나타냅니다.  
  
 ADO **Record** 개체는 OLE DB **Row** 개체의 컨테이너에서 생성 될 수도 있습니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
