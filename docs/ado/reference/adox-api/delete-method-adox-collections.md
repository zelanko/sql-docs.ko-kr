---
title: Delete 메서드 (ADOX 컬렉션) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90f9aa6a788296ff5fef05e96b7f46b56729ded9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298476"
---
# <a name="delete-method-adox-collections"></a>Delete 메서드(ADOX 컬렉션)
컬렉션에서 개체를 제거합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 A **Variant** 이름 또는 삭제할 개체의 서 수 위치 (인덱스)를 지정 하는 합니다.  
  
## <a name="remarks"></a>Remarks  
 오류가 발생 하는 경우는 *이름을* 컬렉션에 존재 하지 않습니다.  
  
 에 대 한 [테이블](../../../ado/reference/adox-api/tables-collection-adox.md) 하 고 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 컬렉션 공급자를 지원 하지 않는 경우 테이블 또는 사용자를 삭제 각각 오류가 발생 합니다. 에 대 한 [프로시저](../../../ado/reference/adox-api/procedures-collection-adox.md) 하 고 [뷰](../../../ado/reference/adox-api/views-collection-adox.md) 컬렉션 **삭제** 공급자 명령 유지를 지원 하지 않는 경우 실패 합니다.  
  
## <a name="applies-to"></a>적용 대상  
  
||||  
|-|-|-|  
|[Columns 컬렉션(ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Groups 컬렉션(ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Indexes 컬렉션(ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Tables 컬렉션(ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>관련 항목  
 [Procedures Delete 메서드 예제 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Views Delete 메서드 예제(VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
