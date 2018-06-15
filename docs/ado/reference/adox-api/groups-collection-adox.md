---
title: 컬렉션 (ADOX) 그룹화 | Microsoft Docs
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
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 253cf76adf8f32734b4bd878cb2f623e79489ccb
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35285972"
---
# <a name="groups-collection-adox"></a>그룹 컬렉션 (ADOX)
모든 포함 저장 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 카탈로그 또는 사용자의 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 **그룹** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 모든 카탈로그의 그룹 계정을 나타냅니다. **그룹** 에 대 한 컬렉션은 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 유일한 사용자가 속한 그룹을 나타냅니다.  
  
 [Append](../../../ado/reference/adox-api/append-method-adox-groups.md) 에 대 한 메서드는 **그룹** 컬렉션이 ADOX에 대해 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   새 보안 그룹을 사용 하 여 컬렉션에 추가 **Append** 메서드.  
  
 나머지 속성 및 메서드는 표준 ADO 컬렉션으로. 다음 작업을 수행할 수 있습니다.  
  
-   그룹 사용 하 여 컬렉션에 액세스할 수는 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 그룹 수를 반환 된 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   그룹을 사용 하 여 컬렉션에서 제거 된 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스 스키마와 반영 하기 위해 컬렉션의 개체를 업데이트 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
> [!NOTE]
>  추가 하기 전에 **그룹** 개체는 **그룹** 의 컬렉션은 **사용자** 개체는 **그룹** 개체와 같은 [ 이름](../../../ado/reference/adox-api/name-property-adox.md) 추가할 하나에 이미 있어야 하는 대로 **그룹** 의 컬렉션은 **카탈로그**합니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Groups 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
