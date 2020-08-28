---
description: 키 개체(ADOX)
title: Key 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d8b2f37dd12f7243f2c5fcb8e577dc35e350c6a9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984054"
---
# <a name="key-object-adox"></a>키 개체(ADOX)
데이터베이스 테이블의 기본 키, 외래 키 또는 고유 키 필드를 나타냅니다.  
  
## <a name="remarks"></a>설명  
 다음 코드는 새 **키**를 만듭니다.  
  
```  
Dim obj As New Key  
```  
  
 **키** 개체의 속성 및 컬렉션을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](./name-property-adox.md) 속성을 사용 하 여 키를 식별 합니다.  
  
-   [Type](./type-property-key-adox.md) 속성을 사용 하 여 키가 primary, foreign 또는 unique 인지 여부를 확인 합니다.  
  
-   [열](./columns-collection-adox.md) 컬렉션을 사용 하 여 키의 데이터베이스 열에 액세스 합니다.  
  
-   [RelatedTable](./relatedtable-property-adox.md) 속성을 사용 하 여 관련 테이블의 이름을 지정 합니다.  
  
-   [DeleteRule](./deleterule-property-adox.md) 및 [UpdateRule](./updaterule-property-adox.md) 속성을 사용 하 여 기본 키를 삭제 하거나 업데이트할 때 수행 되는 동작을 결정 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [키 개체 속성, 메서드 및 이벤트](./key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Columns 컬렉션 (ADOX)](./columns-collection-adox.md)   
 [Keys 컬렉션(ADOX)](./keys-collection-adox.md)