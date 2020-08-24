---
description: Indexes 컬렉션(ADOX)
title: Indexes 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: rothja
ms.author: jroth
ms.openlocfilehash: 0075ca8340d869f803a10d296672e03326c5bad6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770272"
---
# <a name="indexes-collection-adox"></a>Indexes 컬렉션(ADOX)
테이블의 모든 [인덱스](./index-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **인덱스** 컬렉션에 대 한 [APPEND](./append-method-adox-indexes.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 인덱스를 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 인덱스에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 인덱스 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 인덱스를 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Indexes 컬렉션 속성, 메서드 및 이벤트](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Indexes Append 메서드 예제 (VB)](./indexes-append-method-example-vb.md)   
 [인덱스 개체(ADOX)](./index-object-adox.md)