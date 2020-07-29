---
title: 값이 일치하지 않는 행 선택
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 56038b9497f60c2a3275c9216d5c2252d65d81f3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86010600"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>값이 일치하지 않는 행 선택(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
값이 일치하지 않는 행을 찾으려면 NOT 연산자를 사용합니다.  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>값이 일치하지 않는 행을 찾으려면  
  
1.  검색 조건 내에 사용할 열이나 식을 [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에 아직 추가하지 않았다면 추가합니다.  
  
2.  검색할 데이터 열이나 식이 포함된 행을 찾은 다음 표 형태 창의 **필터** 열에 NOT 연산자와 검색 값을 차례로 입력합니다.  
  
예를 들어 `products` 테이블에서 제품 코드 열의 값이 "A" 이외의 문자로 시작하는 행을 모두 찾으려면 다음 검색 조건을 입력하면 됩니다.  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>참고 항목  
[검색 값 입력 규칙](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[검색 조건 지정](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
