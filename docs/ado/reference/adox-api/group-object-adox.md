---
title: 그룹 개체가 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36c26ab9fd3fc92f0636adaff725ef37b181a081
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286032"
---
# <a name="group-object-adox"></a>그룹 개체 (ADOX)
보안된 데이터베이스 내에서 액세스 권한이 있는 그룹 계정을 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 [그룹](../../../ado/reference/adox-api/groups-collection-adox.md) 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 카탈로그의 모든 그룹 계정을 나타냅니다. **그룹** 에 대 한 컬렉션은 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 유일한 사용자가 속한 그룹을 나타냅니다.  
  
 속성, 컬렉션, 및의 메서드는 **그룹** 개체를 할 수 있습니다.  
  
-   그룹을 식별 된 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   확인 여부는 그룹에 읽기, 쓰기 또는 삭제 권한이 있는 [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) 및 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) 메서드.  
  
-   사용 하 여 그룹에 등록 된 사용자 계정에 액세스는 [사용자](../../../ado/reference/adox-api/users-collection-adox.md) 컬렉션입니다.  
  
-   사용 하 여 공급자별 속성에 액세스는 [속성](../../../ado/reference/ado-api/properties-collection-ado.md) 컬렉션입니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Group 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [그룹 컬렉션 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 컬렉션(ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
