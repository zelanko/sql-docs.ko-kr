---
title: ADOStreamConstruction 인터페이스 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf21be88854837ab2dff1a8bc8bc73f44a6e20c9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63248825"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 인터페이스
합니다 **ADOStreamConstruction** 인터페이스는 ADO를 만드는 데 사용 됩니다 **Stream** OLE DB 개체 **IStream** 개체 c에서 /C++ 응용 프로그램입니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[Stream 속성](../../../ado/reference/ado-api/stream-property.md)|읽기/쓰기입니다. OLE DB를 가져오거나 **Stream** 개체입니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>Remarks  
 OLE DB를 제공 **IStream** 개체 (`pStream`), ADO 생성 **Stream** 개체 (`adoStr`) 다음 세 가지 기본 작업에 금액:  
  
1.  ADO를 만듭니다 **Stream** 개체:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  쿼리는 **IADOStreamConstruction** 에 대 한 인터페이스를 **Stream** 개체:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 호출 된 `IADOStreamConstruction::get_Stream` OLE DB를 설정 하려면 속성 메서드 **IStream** ADO 개체 **Stream** 개체:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 결과 `adoStr` 개체에는 이제 ADO 나타냅니다 **Stream** OLE DB에서 생성 된 개체 **IStream** 개체입니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상 버전  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>관련 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)
