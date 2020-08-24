---
description: 그룹 개체(ADOX)
title: Group 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0442ca3bd785269fed49dc86d982971a8feec4ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770422"
---
# <a name="group-object-adox"></a>그룹 개체(ADOX)
보안 데이터베이스 내에서 액세스 권한이 있는 그룹 계정을 나타냅니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](./catalog-object-adox.md) 의 [Groups](./groups-collection-adox.md) 컬렉션은 모든 카탈로그의 그룹 계정을 나타냅니다. [사용자](./user-object-adox.md) 에 대 한 **그룹** 컬렉션은 사용자가 속한 그룹만 나타냅니다.  
  
 **Group** 개체의 속성, 컬렉션 및 메서드를 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](./name-property-adox.md) 속성을 사용 하 여 그룹을 식별 합니다.  
  
-   그룹에 [getpermissions](./getpermissions-method-adox.md) 및 [SetPermissions](./setpermissions-method-adox.md) 메서드를 사용 하 여 읽기, 쓰기 또는 삭제 권한이 있는지 여부를 확인 합니다.  
  
-   [사용자](./users-collection-adox.md) 컬렉션을 사용 하 여 그룹의 멤버 자격이 있는 사용자 계정에 액세스 합니다.  
  
-   [Properties](../ado-api/properties-collection-ado.md) 컬렉션을 사용 하 여 공급자별 속성에 액세스 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [그룹 개체 속성, 메서드 및 이벤트](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Groups 컬렉션 (ADOX)](./groups-collection-adox.md)   
 [Users 컬렉션(ADOX)](./users-collection-adox.md)