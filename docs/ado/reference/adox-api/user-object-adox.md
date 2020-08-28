---
description: 사용자 개체(ADOX)
title: User 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: rothja
ms.author: jroth
ms.openlocfilehash: 6e83bd40c226f1d5b5948c6475b259c799907866
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983053"
---
# <a name="user-object-adox"></a>사용자 개체(ADOX)
보안 데이터베이스 내에서 액세스 권한이 있는 사용자 계정을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](./catalog-object-adox.md) 의 [사용자](./users-collection-adox.md) 컬렉션은 모든 카탈로그의 사용자를 나타냅니다. [그룹](./group-object-adox.md) 에 대 한 **사용자** 컬렉션은 특정 그룹의 사용자만 나타냅니다.  
  
 **사용자** 개체의 속성, 컬렉션 및 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](./name-property-adox.md) 속성을 사용 하 여 사용자를 식별 합니다.  
  
-   [ChangePassword](./changepassword-method-adox.md) 메서드를 사용 하 여 사용자에 대 한 암호를 변경 합니다.  
  
-   사용자에 게 [getpermissions](./getpermissions-method-adox.md) 및 [SetPermissions](./setpermissions-method-adox.md) 메서드를 사용 하 여 읽기, 쓰기 또는 삭제 권한이 있는지 여부를 확인 합니다.  
  
-   [그룹](./groups-collection-adox.md) 컬렉션을 사용 하 여 사용자가 속한 그룹에 액세스 합니다.  
  
-   [Properties](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 속성에 액세스 합니다.  
  
-   사용자에 대 한 [ParentCatalog](./parentcatalog-property-adox.md) 를 확인 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [사용자 개체 속성, 메서드 및 이벤트](./user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [GetPermissions 및 SetPermissions 메서드 예제 (VB)](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [Groups 컬렉션 (ADOX)](./groups-collection-adox.md)   
 [Users 컬렉션(ADOX)](./users-collection-adox.md)