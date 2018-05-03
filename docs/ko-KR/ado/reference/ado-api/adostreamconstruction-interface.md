---
title: ADOStreamConstruction 인터페이스 | Microsoft Docs
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
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 693ccde4f48d5c358f65b83654d137745f97acff
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 인터페이스
**ADOStreamConstruction** 인터페이스 사용 하는 ADO 생성 **스트림** OLE DB에서 개체 **IStream** C/c + + 응용 프로그램의 개체입니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[Stream 속성](../../../ado/reference/ado-api/stream-property.md)|읽기/쓰기입니다. 가져오기/설정 OLE DB **스트림** 개체입니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>주의  
 OLE DB를 제공 **IStream** 개체 (`pStream`), ADO의 생성 **스트림** 개체 (`adoStr`) 다음 세 가지 기본 작업입니다.  
  
1.  ADO 만들기 **스트림** 개체:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  쿼리는 **IADOStreamConstruction** 에 대 한 인터페이스는 **스트림** 개체:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 호출 된 `IADOStreamConstruction::get_Stream` 속성은 OLE DB를 설정 하는 방법은 **IStream** ADO 개체 **스트림** 개체:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 결과 `adoStr` 개체는 이제 ADO 나타냅니다 **스트림** OLE DB에서 생성 된 개체 **IStream** 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 또는 최신 버전  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>관련 항목:  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)
