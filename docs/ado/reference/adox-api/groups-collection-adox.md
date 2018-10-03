---
title: 컬렉션 (ADOX) 그룹화 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6b8aea077af67c882830220da9ce24b802e25e5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801433"
---
# <a name="groups-collection-adox"></a>Groups 컬렉션(ADOX)
모든 포함 저장 [그룹](../../../ado/reference/adox-api/group-object-adox.md) 카탈로그 또는 사용자의 개체입니다.  
  
## <a name="remarks"></a>Remarks  
 합니다 **그룹** 의 컬렉션을 [카탈로그](../../../ado/reference/adox-api/catalog-object-adox.md) 모든 카탈로그의 그룹 계정을 나타냅니다. 합니다 **그룹** 에 대 한 컬렉션을 [사용자](../../../ado/reference/adox-api/user-object-adox.md) 사용자가 속한 그룹에만 나타냅니다.  
  
 합니다 [추가](../../../ado/reference/adox-api/append-method-adox-groups.md) 에 대 한 메서드는 **그룹** 컬렉션이 ADOX에 대 한 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   새 보안 그룹을 사용 하 여 컬렉션에 추가 합니다 **Append** 메서드.  
  
 나머지 속성 및 메서드는 ADO 컬렉션에 표준입니다. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 그룹에 액세스 합니다 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 그룹 개수를 반환 합니다 [개수](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   그룹을 사용 하 여 컬렉션에서 제거 합니다 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   사용 하 여 현재 데이터베이스 스키마를 반영 하 여 컬렉션의 개체를 업데이트 합니다 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
> [!NOTE]
>  추가 하기 전에 **그룹** 개체를 **그룹** 의 컬렉션을 **사용자** 개체를 **그룹** 개체와 같은 [ 이름](../../../ado/reference/adox-api/name-property-adox.md) 추가할 것에 이미 존재 해야 합니다는 **그룹** 컬렉션을 **카탈로그**합니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Groups 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Catalog 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Group 개체(ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
