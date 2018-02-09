---
title: "사용자 컬렉션 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e063db5cd8fa810a1729b0591883b9dda0f9bc2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="users-collection-adox"></a>사용자 컬렉션 (ADOX)
모든 포함 저장 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 의 개체는 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 또는 [그룹](../../../ado/reference/adox-api/group-object-adox.md)합니다.  
  
## <a name="remarks"></a>주의  
 **사용자** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 카탈로그의 모든 사용자를 나타냅니다. **사용자** 에 대 한 컬렉션은 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 특정 그룹에는 구성원 자격이 있는 사용자만 나타냅니다.  
  
 [Append](../../../ado/reference/adox-api/append-method-adox-users.md) 에 대 한 메서드는 **사용자** 컬렉션이 ADOX에 대해 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 새 사용자 컬렉션에 추가 된 **Append** 메서드.  
  
 나머지 속성 및 메서드는 표준 ADO 컬렉션으로. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 사용자 액세스는 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 사용자 수를 반환 된 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에서 사용자를 제거는 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스의 스키마를 반영 하기 위해 컬렉션의 개체를 업데이트 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
> [!NOTE]
>  추가 하기 전에 **사용자** 개체는 **사용자** 의 컬렉션은 **그룹** 개체는 **사용자** 개체와 같은 [이름 ](../../../ado/reference/adox-api/name-property-adox.md) 추가할 하나에 이미 있어야 하는 대로 **사용자** 의 컬렉션은 **카탈로그**합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Users 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User 개체(ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
