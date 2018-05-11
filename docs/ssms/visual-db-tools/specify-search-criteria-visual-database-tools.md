---
title: 검색 조건 지정(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- queries [Visual Database Tools]
- criteria for search conditions
- search conditions [SQL Server], search criteria
- View Designer, Criteria pane
- row return limitations [SQL Server]
- Criteria pane
- restricting rows returned
- search criteria [SQL Server]
- Visual Database Tools [SQL Server], queries
- limiting rows returned
ms.assetid: 25fb4e31-6dbf-4cf6-8e47-0dd0998c836c
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7975547333f76fdf86c0c3633e6b0794be8a98a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="specify-search-criteria-visual-database-tools"></a>검색 조건 지정(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
검색 기준을 사용하여 쿼리가 반환하는 행의 수를 제한할 수 있습니다.  
  
검색 기준을 만드는 특정 단계에 대한 자세한 내용은 다음 표에 나열된 항목을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
[검색 값 입력 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
텍스트, 숫자, 날짜 또는 논리 값을 입력하는 방법에 대해 설명합니다.  
  
[조건 창의 검색 조건 결합 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
AND 및 OR 연산자를 사용하는 데 필요한 기본 개념을 설명합니다.  
  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-conditions-visual-database-tools.md)  
필요한 데이터만 얻기 위해 검색 조건을 선택하는 데 필요한 기본 개념을 설명합니다.  
  
[한 열에 여러 검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)  
동일한 데이터 열에 대해 여러 검색 조건을 만드는 방법에 대해 설명합니다.  
  
[여러 열에 여러 검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
여러 개의 데이터 열을 하나의 쿼리에 대한 검색 조건의 일부로 포함하는 방법에 대해 설명합니다.  
  
[쿼리에 TOP 절 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-the-top-clause-in-queries-visual-database-tools.md)  
지정된 개수나 비율의 행만 반환하도록 만드는 방법에 대해 설명합니다.  
  
[동일한 쿼리에서 HAVING 및 WHERE 절 사용&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)  
쿼리에서 이러한 절을 모두 사용하는 방법과 그 이유에 대해 설명합니다.  
  
[값이 일치하지 않는 행 선택&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/select-rows-that-do-not-match-a-value-visual-database-tools.md)  
쿼리 문에 입력한 값과 지정된 열의 값이 일치하지 않는 행을 모두 반환하는 방법에 대해 설명합니다.  
  
[행 포함 또는 제외&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/include-or-exclude-rows-visual-database-tools.md)  
쿼리에 사용되는 절과 연산자에 대한 기본 개념을 설명합니다.  
  
[중복 행 제외&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md)  
선택 쿼리에서 중복 행을 필터링하여 제거하는 방법에 대해 설명합니다.  
  
[AND에 우선 순위가 있는 조건 조합&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
쿼리 결과를 필터링하기 위해 AND 연산자를 사용하는 방법과 그 이유에 대해 설명합니다.  
  
[OR에 우선 순위가 있는 조건 조합&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
쿼리 결과를 필터링하기 위해 OR 연산자를 사용하는 방법과 그 이유에 대해 설명합니다.  
  
[하위 쿼리 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-subqueries-visual-database-tools.md)  
하위 쿼리 또는 중첩된 쿼리를 만드는 방법에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 섹션  
[쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
가장 일반적인 쿼리 태스크를 수행하는 단계와 관련된 항목의 링크를 제공합니다.  
  
[쿼리 형식&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
지원되는 쿼리 형식에 대해 설명하는 항목의 링크를 제공합니다.  
  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
쿼리 결과를 정렬하고 그룹화하는 단계와 관련된 항목의 링크를 제공합니다.  
  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
NULL 및 숫자 이외의 열을 비롯한 결과를 요약하는 단계와 관련된 항목의 링크를 제공합니다.  
  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
쿼리 및 뷰 디자이너를 사용하여 쿼리와 뷰에서 수행할 수 있는 작업에 대해 설명하는 항목과 섹션의 링크를 제공합니다.  
  
