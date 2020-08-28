---
description: Procedures 컬렉션(ADOX)
title: 프로시저 컬렉션 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures
- Catalog::Procedures
helpviewer_keywords:
- Procedures collection [ADOX]
ms.assetid: dc7a38e1-93b9-4034-9af2-ff419e8fb2a3
author: rothja
ms.author: jroth
ms.openlocfilehash: b3f98420fc85cabd2ccc584817ac6ca9a9203081
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983574"
---
# <a name="procedures-collection-adox"></a>Procedures 컬렉션(ADOX)
카탈로그의 모든 [프로시저](./procedure-object-adox.md) 개체를 포함 합니다.  
  
## <a name="remarks"></a>설명  
 **프로시저** 컬렉션에 대 한 [APPEND](./append-method-adox-procedures.md) 메서드는 ADOX에 대해 고유 합니다. 다음을 수행할 수 있습니다.  
  
-   **Append** 메서드를 사용 하 여 컬렉션에 새 프로시저를 추가 합니다.  
  
 나머지 속성 및 메서드는 ADO 컬렉션의 표준입니다. 다음을 수행할 수 있습니다.  
  
-   [Item](../ado-api/item-property-ado.md) 속성을 사용 하 여 컬렉션의 프로시저에 액세스 합니다.  
  
-   [Count](../ado-api/count-property-ado.md) 속성을 사용 하 여 컬렉션에 포함 된 프로시저 수를 반환 합니다.  
  
-   [Delete](./delete-method-adox-collections.md) 메서드를 사용 하 여 컬렉션에서 프로시저를 제거 합니다.  
  
-   [Refresh](../ado-api/refresh-method-ado.md) 메서드를 사용 하 여 현재 데이터베이스 스키마를 반영 하도록 컬렉션의 개체를 업데이트 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [Indexes 컬렉션 속성, 메서드 및 이벤트](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Command 및 CommandText 속성 예제 (VB)](./command-and-commandtext-properties-example-vb.md)   
 [Parameters 컬렉션, Command 속성 예제 (VB)](./parameters-collection-command-property-example-vb.md)   
 [프로시저 Append 메서드 예제 (VB)](./procedures-append-method-example-vb.md)   
 [프로시저 Delete 메서드 예제 (VB)](./procedures-delete-method-example-vb.md)   
 [프로시저 Refresh 메서드 예제 (VB)](./procedures-refresh-method-example-vb.md)   
 [프로시저 컬렉션 속성, 메서드 및 이벤트](./procedures-collection-properties-methods-and-events.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [프로시저 개체(ADOX)](./procedure-object-adox.md)