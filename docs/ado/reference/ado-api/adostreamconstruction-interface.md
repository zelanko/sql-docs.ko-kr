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
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920782"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction 인터페이스
**ADOStreamConstruction** 인터페이스는 C/c + + 응용 프로그램의 OLE DB **ISTREAM** 개체에서 ADO **스트림** 개체를 생성 하는 데 사용 됩니다.  
  
## <a name="properties"></a>속성  
  
|||  
|-|-|  
|[Stream 속성](../../../ado/reference/ado-api/stream-property.md)|읽기/쓰기. OLE DB **Stream** 개체를 가져오거나 설정 합니다.|  
  
## <a name="methods"></a>메서드  
 없음  
  
## <a name="events"></a>이벤트  
 없음  
  
## <a name="remarks"></a>설명  
 OLE DB **IStream** 개체 (`pStream`)를 지정 하는 경우 다음 세 가지 기본 작업에`adoStr`대 한 ADO **스트림** 개체 ()의 생성은 다음과 같습니다.  
  
1.  ADO **Stream** 개체를 만듭니다.  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  **Stream** 개체에서 **IADOStreamConstruction** 인터페이스를 쿼리 합니다.  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 속성 메서드를 호출 하 여 ADO **스트림** 개체에 대 한 OLE DB IStream 개체를 설정 합니다. **** `IADOStreamConstruction::get_Stream`  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 이제 결과 `adoStr` 개체는 OLE DB **IStream** 개체에서 생성 된 ADO **스트림** 개체를 나타냅니다.  
  
## <a name="requirements"></a>요구 사항  
 **버전:** ADO 2.0 이상 버전  
  
 **라이브러리:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>참고 항목  
 [ADO API 참조](../../../ado/reference/ado-api/ado-api-reference.md)
