---
title: "쿼리 매개 변수 대화 상자(Visual Database Tools) | Microsoft 문서"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:69645
- vdt.dlgbox.definequeryparameters
ms.assetid: 31cdaee2-d7cd-4d64-a45f-924b27e8b1f0
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4071afdf8f0ae520bf60a927cb5e43e10a392b7c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="query-parameters-dialog-box-visual-database-tools"></a>쿼리 매개 변수 대화 상자(Visual Database Tools)
이 대화 상자를 사용하면 쿼리에 정의된 매개 변수에 사용할 값을 입력할 수 있습니다. 이 대화 상자는 런타임에 최종 사용자가 입력해야 할 매개 변수가 포함된 쿼리를 실행할 때 나타납니다.  
  
## <a name="options"></a>옵션  
**이름**  
실행할 쿼리에 대해 정의된 매개 변수를 나열합니다. 쿼리에 명명된 매개 변수가 포함된 경우 목록에 이름이 표시됩니다. 쿼리에 명명되지 않은 매개 변수가 포함된 경우 쿼리의 각 매개 변수에 대해 자동으로 지정된 매개 변수 이름이 나열됩니다.  
  
**Value**  
**이름**아래에 나열된 각 매개 변수에 대한 값을 입력합니다. 가장 최근에 사용한 값이 기본 매개 변수 값으로 표시됩니다.  
  
## <a name="example"></a>예제  
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject_md.md)] 데이터베이스에서 SQL 창의 다음 쿼리를 실행하면 쿼리 매개 변수 대화 상자가 열립니다.  
  
```  
SELECT   FirstName, LastName  
FROM    Person.Person AS Lastname  
WHERE   (LastName = @Param1);  
```  
  
## <a name="see-also"></a>관련 항목:  
[매개 변수를 사용하여 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
