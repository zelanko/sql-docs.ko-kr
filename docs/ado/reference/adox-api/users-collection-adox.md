---
title: 사용자 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bbf05e0b177cc61ed9de757db46f8950aaa7dccd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705631"
---
# <a name="users-collection-adox"></a>Users 컬렉션(ADOX)
모든 포함 저장 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 의 개체를 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 하거나 [그룹](../../../ado/reference/adox-api/group-object-adox.md)합니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **사용자** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 카탈로그의 모든 사용자를 나타냅니다. 합니다 **사용자** 에 대 한 컬렉션을 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 특정 그룹의 멤버 자격이 있는 사용자만을 나타냅니다.  
  
 합니다 [추가](../../../ado/reference/adox-api/append-method-adox-users.md) 에 대 한 메서드는 **사용자** 컬렉션이 ADOX에 대 한 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 새 사용자 컬렉션에 추가 합니다 **Append** 메서드.  
  
 나머지 속성 및 메서드는 ADO 컬렉션에 표준입니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션에서 사용자 액세스는 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 사용자 수를 반환 합니다 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에서 사용자를 제거 합니다 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스의 스키마를 반영 하기 위해 컬렉션의 개체를 업데이트 합니다 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
> [!NOTE]
>  추가 하기 전에 **사용자** 개체를 **사용자** 의 컬렉션을 **그룹** 개체를 **사용자** 개체와 같은 [이름 ](../../../ado/reference/adox-api/name-property-adox.md) 추가할 것에 이미 존재 해야 합니다는 **사용자** 컬렉션을 **카탈로그**합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Users 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
