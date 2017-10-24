---
title: "중간 셰이프 COMPUTE 절 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- COMPUTE clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: a576bf81-8f3c-4ba1-817b-87e89a8da684
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8f96448c095c9b2e818e413bcd131d11fa464782
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="intervening-shape-compute-clauses"></a>중간 셰이프 COMPUTE 절
다음 예제와 같이 매개 변수가 있는 shape 명령에서 부모 및 자식 간 하나 이상의 COMPUTE 절을 포함 하는 것이 올바릅니다.  
  
```  
SHAPE {select au_lname, state from authors} APPEND   
   ((SHAPE   
      (SHAPE   
         {select * from authors where state = ?} rs   
      COMPUTE rs, ANY(rs.state) state, ANY(rs.au_lname) au_lname   
      BY au_id) rs2   
   COMPUTE rs2, ANY(rs2.state) BY au_lname)   
RELATE state TO PARAMETER 0)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)

