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
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964959"
---
# <a name="users-collection-adox"></a>Users 컬렉션(ADOX)
[카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 또는 [그룹](../../../ado/reference/adox-api/group-object-adox.md)의 모든 저장 된 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 의 **사용자** 컬렉션은 모든 카탈로그의 사용자를 나타냅니다. [그룹](../../../ado/reference/adox-api/group-object-adox.md) 에 대 한 **사용자** 컬렉션은 특정 그룹의 멤버 자격이 있는 사용자만 나타냅니다.  
  
 **사용자** 컬렉션에 대 한 [APPEND](../../../ado/reference/adox-api/append-method-adox-users.md) 메서드는 ADOX에 대해 고유 합니다. 다음과 같은 작업을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 사용자를 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음과 같은 작업을 수행할 수 있습니다.  
  
-   [Item](../../../ado/reference/ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 사용자에 액세스 합니다.  
  
-   [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 사용자 수를 반환 합니다.  
  
-   [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 사용자를 제거 합니다.  
  
-   [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스의 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
> [!NOTE]
>  **Group** 개체의 **사용자 컬렉션에** **사용자** 개체를 추가 하기 전에 추가 될 [이름과](../../../ado/reference/adox-api/name-property-adox.md) 같은 **사용자** 개체가 **카탈로그**의 **사용자** 컬렉션에 이미 존재 해야 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Users 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
