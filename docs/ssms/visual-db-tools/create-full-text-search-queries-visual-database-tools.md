---
title: 전체 텍스트 검색 쿼리 만들기(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.openlocfilehash: 20ffbc7d09755d6cc849886723217a4142d47322
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "58306021"
---
# <a name="create-full-text-search-queries-visual-database-tools"></a>전체 텍스트 검색 쿼리 만들기(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
전체 텍스트 검색에는 해당 열에 지정된 텍스트가 있는 행을 찾기 위한 CONTAINS 조건자가 사용됩니다. 전체 텍스트 검색은 전체 텍스트 인덱스가 활성화된 열에 대해서만 수행할 수 있습니다. 전체 텍스트 인덱스가 현재 활성화되어 있지 않은 열에 대해 CONTAINS 절을 사용하려 하면 오류가 발생합니다. 전체 텍스트 인덱스와 CONTAINS 절에 대한 자세한 내용은 [전체 텍스트 검색(SQL Server)](../../relational-databases/search/full-text-search.md) 및 [CONTAINS(Transact-SQL)](https://msdn.microsoft.com/996c72fc-b1ab-4c96-bd12-946be9c18f84)를 참조하세요.  
  
### <a name="to-create-a-full-text-search-query"></a>전체 텍스트 검색 쿼리를 만들려면  
  
1.  솔루션 탐색기에서 쿼리를 열거나 새 쿼리를 만듭니다.  
  
2.  전체 텍스트 열을 검색하기 위한 CONTAINS 함수를 쿼리의 WHERE 절에 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
[지원되는 쿼리 형식&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
