---
title: 키 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7365b3ac33f215840a112089523f23e88697a433
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626731"
---
# <a name="key-object-adox"></a>키 개체(ADOX)
데이터베이스 테이블에서 기본, 외래, 또는 고유 키 필드를 나타냅니다.  
  
## <a name="remarks"></a>Remarks  
 다음 코드를 만듭니다 **키**:  
  
```  
Dim obj As New Key  
```  
  
 속성 및 컬렉션을 **키** 개체를 할 수 있습니다.  
  
-   사용 하 여 키를 식별 합니다 [이름을](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   기본, 외래, 또는 고유 키 인지 확인 합니다 [형식](../../../ado/reference/adox-api/type-property-key-adox.md) 속성입니다.  
  
-   사용 하 여 키의 데이터베이스 열에 액세스 합니다 [열](../../../ado/reference/adox-api/columns-collection-adox.md) 컬렉션입니다.  
  
-   관련된 테이블의 이름을 지정 합니다 [RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md) 속성입니다.  
  
-   삭제 또는 기본 키가 업데이트에서 수행 하는 동작을 확인 합니다 [DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md) 하 고 [UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md) 속성입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [Key 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [Keys Append 메서드, 키 유형, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Columns 컬렉션 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys 컬렉션(ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
