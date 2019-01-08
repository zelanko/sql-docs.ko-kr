---
title: 전체 텍스트 검색 쿼리 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- CONTAINS predicate (Transact-SQL)
- queries [full-text search], creating
- full-text queries [SQL Server], creating
ms.assetid: 537fa556-390e-4c88-9b8e-679848d94abc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1f3ab74c6dd095fd92e0f9d20ba622be70a37ef9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52768575"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>전체 텍스트 검색 쿼리 만들기(Visual Database Tools)
  전체 텍스트 검색에는 해당 열에 지정된 텍스트가 있는 행을 찾기 위한 CONTAINS 조건자가 사용됩니다. 전체 텍스트 검색은 전체 텍스트 인덱스가 활성화된 열에 대해서만 수행할 수 있습니다. 전체 텍스트 인덱스가 현재 활성화되어 있지 않은 열에 대해 CONTAINS 절을 사용하려 하면 오류가 발생합니다. 전체 텍스트 인덱스와 CONTAINS 절에 대 한 자세한 내용은 참조 하세요. [Full-text Search](../../relational-databases/search/full-text-search.md) 하 고 [CONTAINS &#40;TRANSACT-SQL&#41;](/sql/t-sql/queries/contains-transact-sql).  
  
### <a name="to-create-a-full-text-search-query"></a>전체 텍스트 검색 쿼리를 만들려면  
  
1.  솔루션 탐색기에서 쿼리를 열거나 새 쿼리를 만듭니다.  
  
2.  전체 텍스트 열을 검색하기 위한 CONTAINS 함수를 쿼리의 WHERE 절에 사용합니다.  
  
## <a name="see-also"></a>관련 항목  
 [지원 되는 쿼리 유형 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [방법 도움말 항목을 쿼리 및 뷰 디자인 &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
