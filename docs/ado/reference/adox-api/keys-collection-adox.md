---
description: Keys 컬렉션(ADOX)
title: Keys 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 95d1b5b927f03a0592f25cc4cc79c0ffe78cee74
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770062"
---
# <a name="keys-collection-adox"></a>Keys 컬렉션(ADOX)
[테이블](./table-object-adox.md)의 모든 [키](./key-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 [키 컬렉션]() 에 대 한 [APPEND](./append-method-adox-keys.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   [Append](./append-method-adox-keys.md) 메서드를 사용 하 여 컬렉션에 새 키를 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 키에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 키의 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 키를 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스의 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Indexes 컬렉션 속성, 메서드 및 이벤트](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Keys Append 메서드, Key Type, RelatedColumn, RelatedTable 및 UpdateRule 속성 예제 (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Keys 컬렉션 속성, 메서드 및 이벤트](./keys-collection-properties-methods-and-events.md)   
 [키 개체(ADOX)](./key-object-adox.md)