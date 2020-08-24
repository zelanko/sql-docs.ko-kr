---
description: Delete 메서드(ADOX 컬렉션)
title: Delete 메서드 (ADOX Collections) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f239978dc9d71af81c74de452fefe16efe95d1bf
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770632"
---
# <a name="delete-method-adox-collections"></a>Delete 메서드(ADOX 컬렉션)
컬렉션에서 개체를 제거 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>매개 변수  
 *이름*  
 삭제할 개체의 이름 또는 서 수 위치 (인덱스)를 지정 하는 **Variant** 입니다.  
  
## <a name="remarks"></a>설명  
 컬렉션에 *이름이* 없는 경우 오류가 발생 합니다.  
  
 [테이블](./tables-collection-adox.md) 및 [사용자](./users-collection-adox.md) 컬렉션의 경우 공급자가 테이블 또는 사용자 삭제를 각각 지원 하지 않는 경우 오류가 발생 합니다. [프로시저](./procedures-collection-adox.md) 및 [뷰](./views-collection-adox.md) 컬렉션의 경우 공급자가 명령 유지를 지원 하지 않으면 **삭제가** 실패 합니다.  
  
## <a name="applies-to"></a>적용 대상  

:::row:::
    :::column:::
        [Columns 컬렉션(ADOX)](./columns-collection-adox.md)  
        [Groups 컬렉션(ADOX)](./groups-collection-adox.md)  
        [Indexes 컬렉션(ADOX)](./indexes-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Keys 컬렉션(ADOX)](./keys-collection-adox.md)  
        [Procedures 컬렉션(ADOX)](./procedures-collection-adox.md)  
        [Tables 컬렉션(ADOX)](./tables-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Users 컬렉션(ADOX)](./users-collection-adox.md)  
        [Views 컬렉션(ADOX)](./views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>참고 항목  
 [프로시저 Delete 메서드 예제 (VB)](./procedures-delete-method-example-vb.md)   
 [Views Delete 메서드 예제(VB)](./views-delete-method-example-vb.md)