---
description: 다시 셰이핑
title: 모양 변경 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reshaping previously shaped Recordset [ADO]
- data shaping [ADO], reshaping
ms.assetid: b1c965b7-3dad-4de6-9e0e-502ca8785be3
author: rothja
ms.author: jroth
ms.openlocfilehash: 04c43b9fcca56959aec242f344da6ec81a825030
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979774"
---
# <a name="reshaping"></a>다시 셰이핑
셰이프 명령의 절에서 만든 **레코드 집합** 에는 *별칭* 이름 (일반적으로 AS 키워드 사용)이 할당 될 수 있습니다. 모양이 지정 된 **레코드 집합** 의 별칭은 완전히 다른 명령에서 참조할 수 있습니다. 즉, 새 shape 명령에서 이전에 만든 **레코드 집합** 을 다시 사용 하거나 *변경할*수 있습니다. 이 기능을 지원 하기 위해 ADO는 [이름을 변경](../../../ado/reference/ado-api/reshape-name-property-dynamic-ado.md)하는 속성을 제공 합니다.  
  
 모양 변경에는 두 가지 주요 기능이 있습니다. 첫 번째는 기존 **레코드 집합** 을 새 부모 **레코드 집합과**연결 하는 것입니다.  
  
## <a name="example"></a>예제  
  
```  
rs1.Open "SHAPE {select * from Customers} " & _  
         "APPEND ({select * from Orders} AS chapOrders " & _  
         "RELATE CustomerID to CustomerID)", cn  
  
rs2.Open "SHAPE {select * from Employees} " & _  
         "APPEND (chapOrders RELATE EmployeeID to EmployeeID)", cn  
```  
  
 두 번째 함수는 "SHAPE" 구문을 사용 하 여 기존 자식 **레코드 집합** 개체에 대 한 장으로 연결 되지 않은 액세스를 사용 하도록 설정 하는 것입니다 \<recordset reshape name> .  
  
> [!NOTE]
>  기존 **레코드 집합**에 열을 추가 하거나, 중간 COMPUTE 절에서 매개 변수가 있는 **레코드** 집합 또는 **레코드 집합** 개체의 모양을 변경 하거나, **레코드 집합** 의 모든 **레코드 집합** 하위 항목에 대해 집계 작업을 수행할 수 없습니다. **레코드 집합** 의 모양이 바뀔 때 새 shape 명령은 둘 다 동일한 [연결](../../../ado/reference/ado-api/connection-object-ado.md)을 사용 해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)
