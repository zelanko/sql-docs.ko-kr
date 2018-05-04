---
title: 사용자 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 703f62b3a14511bc34aa7f01306ae557db9d07e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="user-object-adox"></a>사용자 개체 (ADOX)
보안된 데이터베이스 내에서 액세스 권한이 있는 사용자 계정을 나타냅니다.  
  
## <a name="remarks"></a>주의  
 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 카탈로그의 모든 사용자를 나타냅니다. **사용자** 에 대 한 컬렉션은 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 특정 그룹의 사용자만 나타냅니다.  
  
 속성, 컬렉션, 및의 메서드는 **사용자** 개체를 할 수 있습니다.  
  
-   사용 하 여 사용자를 식별 된 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   사용자에 대 한 암호를 변경 하는 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 메서드.  
  
-   사용자가 읽을 있는지 확인 쓰기 또는 삭제 된 권한은 [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) 및 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) 메서드.  
  
-   사용자와 속해 있는 그룹 액세스는 [그룹](../../../ado/reference/adox-api/groups-collection-adox.md) 컬렉션입니다.  
  
-   사용 하 여 공급자별 속성에 액세스는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
-   확인 된 [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 사용자에 대 한 합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [User 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [그룹 컬렉션 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
