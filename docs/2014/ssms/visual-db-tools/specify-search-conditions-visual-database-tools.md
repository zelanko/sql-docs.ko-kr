---
title: 검색 조건 지정(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- choosing search criteria
- search conditions [SQL Server], specifying
- search criteria [SQL Server], specifying conditions
ms.assetid: 18e2c759-68ec-4efe-b208-2f73418cd9bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 75b29477c7ead402f06c9df2505a84636b906978
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63163950"
---
# <a name="specify-search-conditions-visual-database-tools"></a>검색 조건 지정(Visual Database Tools)
  검색 조건을 지정하여 쿼리에 표시할 데이터 행을 지정할 수 있습니다. 예를 들어 `employee` 테이블을 쿼리 중인 경우 특정 지역에 근무하는 직원만 찾도록 지정할 수 있습니다.  
  
 식을 사용하여 검색 조건을 지정합니다. 가장 일반적으로 사용하는 식은 연산자와 검색 값으로 구성됩니다. 예를 들어 특정 영업 지역에 근무하는 직원을 찾으려면 `region` 열에 다음 검색 조건을 지정하면 됩니다.  
  
```  
='UK'  
```  
  
> [!NOTE]  
>  여러 테이블을 사용하여 작업 중인 경우 쿼리 및 뷰 디자이너는 각 검색 조건을 검사하여 사용자가 만든 비교를 조인할지 여부를 결정합니다. 조인하도록 결정하면 쿼리 및 뷰 디자이너가 검색 조건을 조인으로 자동 변환합니다. 자세한 내용은 [테이블 자동 조인&#40;Visual Database Tools&#41;](visual-database-tools.md)을 참조하세요.  
  
### <a name="to-specify-search-conditions"></a>검색 조건을 지정하려면  
  
1.  검색 조건 내에 사용할 열이나 식을 조건 창에 아직 추가하지 않았다면 추가합니다.  
  
     선택 쿼리를 만드는 중이며 쿼리 결과에 검색 열이나 식을 표시하지 않으려면 각 검색 열이나 식에 대해 **출력** 열의 선택을 취소하여 출력 열에서 제거합니다.  
  
2.  검색할 데이터 열이나 식을 포함하는 행을 찾은 다음 **필터** 열에 검색 조건을 입력합니다.  
  
    > [!NOTE]  
    >  연산자를 입력하지 않으면 쿼리 및 뷰 디자이너에서 자동으로 등가 연산자 "="를 삽입합니다.  
  
 쿼리 및 뷰 디자이너는 WHERE 절을 추가하거나 수정하여 [SQL 창](sql-pane-visual-database-tools.md) 에서 SQL 문을 업데이트합니다.  
  
## <a name="see-also"></a>관련 항목  
 [검색 값 입력 규칙 &#40;Visual Database Tools&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [검색 조건 지정&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
