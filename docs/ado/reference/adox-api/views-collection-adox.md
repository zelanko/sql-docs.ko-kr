---
description: Views 컬렉션(ADOX)
title: Views 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
author: rothja
ms.author: jroth
ms.openlocfilehash: 26d61c1d2835d9dcabba82beb2a120330f8f2ead
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982874"
---
# <a name="views-collection-adox"></a>Views 컬렉션(ADOX)
카탈로그의 모든 [뷰](./view-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **Views** 컬렉션에 대 한 [APPEND](./append-method-adox-views.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 뷰를 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 뷰에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 뷰 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 뷰를 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Views 컬렉션 속성, 메서드 및 이벤트](./views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Views 및 Fields 컬렉션 예제 (VB)](./views-and-fields-collections-example-vb.md)   
 [Views Append 메서드 예제 (VB)](./views-append-method-example-vb.md)   
 [Views 컬렉션, CommandText 속성 예제 (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete 메서드 예제 (VB)](./views-delete-method-example-vb.md)   
 [Views Refresh 메서드 예제 (VB)](./views-refresh-method-example-vb.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [보기 개체(ADOX)](./view-object-adox.md)