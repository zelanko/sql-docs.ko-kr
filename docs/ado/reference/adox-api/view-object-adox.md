---
title: 개체 (ADOX) 보기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6bc26e8d59c29bd7b1b0fbdd0a3a4fdb39f8fee1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964842"
---
# <a name="view-object-adox"></a>보기 개체(ADOX)
가상 테이블을 레코드의 필터링 된 집합을 나타냅니다. ADO와 함께 사용 하는 경우 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체를 **보기** 개체 추가, 삭제 또는 뷰 수정에 사용할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 뷰는 다른 데이터베이스 테이블 또는 뷰에서 생성 하는 가상 테이블. 합니다 **보기** 개체를 사용 하면 알고 있거나 공급자의 "CREATE VIEW" 구문을 사용 하지 않고 뷰를 만들 수 있습니다.  
  
 속성을 사용 하 여는 **보기** 개체를 할 수 있습니다.  
  
-   뷰를 식별 합니다 [이름을](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   ADO 지정 **명령** 추가, 삭제 또는 사용 하 여 뷰를 수정 하는 개체를 [명령](../../../ado/reference/adox-api/command-property-adox.md) 속성입니다.  
  
-   사용 하 여 날짜 정보를 반환 합니다 [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) 하 고 [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) 속성입니다.  
  
 이 섹션에서는 다음 항목을 포함합니다.  
  
-   [View 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목  
 [뷰 및 Fields 컬렉션 예제 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 메서드 예제 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 컬렉션, CommandText 속성 예제 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 메서드 예제 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
