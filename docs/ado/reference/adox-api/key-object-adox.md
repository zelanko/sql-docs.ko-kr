---
title: "키 개체 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7d05a52614694bc9464c609ab4f4ed0965f3b81e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="key-object-adox"></a>키 개체 (ADOX)
데이터베이스 테이블에서 기본, 외래, 또는 고유 키 필드를 나타냅니다.  
  
## <a name="remarks"></a>주의  
 다음 코드에서는 새 **키**:  
  
```  
Dim obj As New Key  
```  
  
 속성과 컬렉션을 사용 하 여 한 **키** 개체를 할 수 있습니다.  
  
-   사용 하 여 키를 식별 된 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   기본, 외래, 또는 고유 키 적용 되는지 확인은 [형식](../../../ado/reference/adox-api/type-property-key-adox.md) 속성입니다.  
  
-   데이터베이스 열에 사용 하 여 키의 액세스는 [열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
-   포함 된 관련된 테이블의 이름을 지정는 [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) 속성입니다.  
  
-   삭제 하거나 사용 하 여 기본 키의 업데이트에 수행 하는 작업을 결정는 [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) 및 [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) 속성입니다.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Key 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [키 추가 방법, 키 형식, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)

