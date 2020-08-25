---
description: Groups 컬렉션(ADOX)
title: Groups 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: rothja
ms.author: jroth
ms.openlocfilehash: 5edecbbfebeea82d28f97bc31d15e04bf28c576a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770332"
---
# <a name="groups-collection-adox"></a>Groups 컬렉션(ADOX)
카탈로그나 사용자의 모든 저장 된 [그룹](./group-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 [카탈로그](./catalog-object-adox.md) 의 **Groups** 컬렉션은 모든 카탈로그 그룹 계정을 나타냅니다. [사용자](./user-object-adox.md) 에 대 한 **그룹** 컬렉션은 사용자가 속한 그룹만 나타냅니다.  
  
 **그룹** 컬렉션에 대 한 [APPEND](./append-method-adox-groups.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 보안 그룹을 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 그룹에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 그룹의 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 그룹을 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
> [!NOTE]
>  **그룹** 개체를 **사용자** 개체의 **groups** 컬렉션에 추가 하기 전에 추가 될 그룹과 동일한 [이름의](./name-property-adox.md) **그룹** 개체가 **카탈로그**의 **groups** 컬렉션에 이미 존재 해야 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Groups 컬렉션 속성, 메서드 및 이벤트](./groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [그룹 개체(ADOX)](./group-object-adox.md)