---
title: "프로시저 개체 (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Procedure
helpviewer_keywords: Procedure object [ADOX]
ms.assetid: 927bcf3e-32f5-4a80-98d3-600779f0732e
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: febff0a863fc7bbabec2bed076249366644b84c8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="procedure-object-adox"></a>프로시저 개체 (ADOX)
저장된 프로시저를 나타냅니다. ADO와 함께 사용 하는 경우 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체는 **프로시저** 개체를 추가, 삭제 또는 저장된 프로시저 수정에 사용할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 **프로시저** 개체를 알거나 공급자의 "CREATE PROCEDURE" 구문을 사용 하지 않고도 저장된 프로시저를 만들 수 있습니다.  
  
 속성으로는 **프로시저** 개체를 할 수 있습니다.  
  
-   사용 하 여 프로시저를 식별 된 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   ADO 지정 **명령** 만들거나 사용 하 여 프로시저를 실행 하는 데 사용할 수 있는 개체는 [명령](../../../ado/reference/adox-api/command-property-adox.md) 속성입니다.  
  
-   반환 된 날짜 정보는 [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) 및 [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) 속성.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [Procedure 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/procedure-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [명령 및 CommandText 속성 예제 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Parameters 컬렉션, 명령 속성 예제 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [메서드 예제 (VB)를 추가 하는 절차](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [프로시저 삭제 (VB) 메서드 예제](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Procedures 컬렉션(ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
