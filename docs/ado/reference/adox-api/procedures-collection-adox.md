---
title: 프로시저 컬렉션 (ADOX) | Microsoft Docs
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
- Procedures
- Catalog::Procedures
helpviewer_keywords:
- Procedures collection [ADOX]
ms.assetid: dc7a38e1-93b9-4034-9af2-ff419e8fb2a3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2690c2911fbd4824937c7153ba681cd5d77b703c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286662"
---
# <a name="procedures-collection-adox"></a>프로시저 컬렉션 (ADOX)
모든 포함 [프로시저](../../../ado/reference/adox-api/procedure-object-adox.md) 카탈로그의 개체가 있습니다.  
  
## <a name="remarks"></a>Remarks  
 [Append](../../../ado/reference/adox-api/append-method-adox-procedures.md) 에 대 한 메서드는 **프로시저** 컬렉션이 ADOX에 대해 고유 합니다. 다음 작업을 수행할 수 있습니다.  
  
-   새 프로시저를 사용 하 여 컬렉션에 추가 **Append** 메서드.  
  
 나머지 속성 및 메서드는 표준 ADO 컬렉션으로. 다음 작업을 수행할 수 있습니다.  
  
-   사용 하 여 컬렉션의 프로시저에 액세스는 [항목](../../../ado/reference/ado-api/item-property-ado.md) 속성입니다.  
  
-   사용 하 여 컬렉션에 포함 된 프로시저의 수를 반환 된 [Count](../../../ado/reference/ado-api/count-property-ado.md) 속성입니다.  
  
-   프로시저를 사용 하 여 컬렉션에서 제거 된 [삭제](../../../ado/reference/adox-api/delete-method-adox-collections.md) 메서드.  
  
-   현재 데이터베이스 스키마와 반영 하기 위해 컬렉션의 개체를 업데이트 하는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Indexes 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [명령 및 CommandText 속성 예제 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Parameters 컬렉션, 명령 속성 예제 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [메서드 예제 (VB)를 추가 하는 절차](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [프로시저 삭제 (VB) 메서드 예제](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [프로시저는 메서드 예제를 (VB)를 새로 고칩니다.](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [프로시저 컬렉션 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/procedures-collection-properties-methods-and-events.md)   
 [카탈로그 개체 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Procedure 개체(ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)
