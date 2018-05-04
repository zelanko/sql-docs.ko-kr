---
title: 개체 (ADOX) 보기 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a55d77b7bb7f79ee5871445d5169a4dfd2de5f5d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="view-object-adox"></a>뷰 개체 (ADOX)
가상 테이블 또는 레코드의 필터링 된 집합을 나타냅니다. ADO와 함께 사용 하는 경우 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체는 **보기** 개체를 추가, 삭제 또는 뷰 수정에 사용할 수 있습니다.  
  
## <a name="remarks"></a>주의  
 뷰는 다른 데이터베이스 테이블 또는 뷰에서 생성 하는 가상 테이블. **보기** 개체를 알거나 공급자의 "CREATE VIEW" 구문을 사용할 필요 없이 보기를 만들 수 있습니다.  
  
 속성으로는 **보기** 개체를 할 수 있습니다.  
  
-   사용 하 여 뷰를 식별 된 [이름](../../../ado/reference/adox-api/name-property-adox.md) 속성입니다.  
  
-   ADO 지정 **명령** 추가, 삭제 또는 사용 하 여 뷰를 수정 하는 데 사용할 수 있는 개체는 [명령](../../../ado/reference/adox-api/command-property-adox.md) 속성입니다.  
  
-   반환 된 날짜 정보는 [DateCreated](../../../ado/reference/adox-api/datecreated-property-adox.md) 및 [DateModified](../../../ado/reference/adox-api/datemodified-property-adox.md) 속성.  
  
 이 섹션에는 다음 항목 포함 되어 있습니다.  
  
-   [View 개체 속성, 메서드 및 이벤트](../../../ado/reference/adox-api/view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>관련 항목:  
 [뷰 및 필드 컬렉션 예제 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [뷰 추가 (VB) 메서드 예제](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [뷰 컬렉션, CommandText 속성 예제 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [뷰 삭제 (VB) 메서드 예제](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views 컬렉션(ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
