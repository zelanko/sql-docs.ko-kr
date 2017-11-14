---
title: "모양 변경 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d5264de973e4ed36cc24eb5c535576bdfa0a7228
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="reshaping"></a>모양 변경
A **레코드 집합** 만든 도형의 절에 의해 명령을 할당할 수 있습니다는 *별칭* 이름 (일반적으로 AS 키워드가). 모양의의 별칭 **레코드 집합** 완전히 다른 명령에서 참조할 수 있습니다. 즉, 다시 사용할 수 있습니다, 또는 *변형*, 이전에 모양의 **레코드 집합** 새 shape 명령에서 합니다. 이 기능을 지원 하려면 ADO에는 속성을 제공 [이름 변형](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)합니다.  
  
 모양 변경에 두 가지 주요 기능이 있습니다. 기존 연결 하는 첫 번째는 **레코드 집합** 새 부모와 **레코드 집합**합니다.  
  
## <a name="example"></a>예제  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 두 번째 기능은 기존 자식에 장으로 나뉜 비 액세스할 수 있도록 하는 것 **레코드 집합** 구문을 사용 하 여 개체 "셰이프 \<레코드 집합 변형 이름 >"입니다.  
  
> [!NOTE]
>  기존 열을 추가할 수 없습니다 **레코드 집합**, 매개 변수가 있는 변형 **레코드 집합** 또는 **레코드 집합** 모든 중간 COMPUTE 절에 개체 또는 수행 작업을 집계 **레코드 집합** 에서 하위는 **레코드 집합** 모양을 변경할 되 고 있습니다. **레코드 집합** 모양을 변경할 되 고 새 셰이프 명령을 둘 다 사용 해야 동일한 [연결](../../../ado/reference/ado-api/connection-object-ado.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)

