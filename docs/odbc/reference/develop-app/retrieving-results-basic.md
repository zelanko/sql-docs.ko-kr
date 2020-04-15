---
title: 결과 검색 (기본) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f7d01bf92fcee07940e449a2fb4bbac4f0fe6ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304334"
---
# <a name="retrieving-results-basic"></a>결과 검색(기본)
*결과 집합은* 특정 조건과 일치하는 데이터 원본의 행 집합입니다. 쿼리에서 발생 하 고 테이블 형식으로 응용 프로그램에서 사용할 수 있는 개념 테이블입니다. **SELECT** 문, 카탈로그 함수 및 일부 프로시저는 결과 집합을 만듭니다. 다음 예제에서 첫 번째 SQL 문은 Orders 테이블의 모든 행과 모든 열을 포함하는 결과 집합을 만들고 두 번째 SQL 문은 상태가 열려 있는 Orders 테이블의 행에 대해 OrderID, SalesPerson 및 상태 열을 포함하는 결과 집합을 만듭니다.  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 결과 집합은 비어 있을 수 있으며, 이는 전혀 설정된 결과와 다릅니다. 예를 들어 다음 SQL 문은 빈 결과 집합을 만듭니다.  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 빈 결과 집합은 행이 없다는 점을 제외하면 다른 결과 집합과 다르지 않습니다. 예를 들어 응용 프로그램은 결과 집합에 대한 메타데이터를 검색하고, 행을 가져오려고 시도할 수 있으며, 결과 집합에 대한 커서를 닫아야 합니다.  
  
 데이터 원본에서 행을 검색하고 응용 프로그램에 반환하는 *프로세스를 fetching이라고*합니다. 이 섹션에서는 해당 프로세스의 기본 부분에 대해 설명합니다. 블록 및 스크롤 가능한 커서와 같은 고급 항목에 대한 자세한 내용은 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 및 [스크롤 가능한 커서를](../../../odbc/reference/develop-app/scrollable-cursors.md)참조하십시오. 행 업데이트, 삭제 및 삽입에 대한 자세한 내용은 [데이터 개요 업데이트를](../../../odbc/reference/develop-app/updating-data-overview.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 집합이 생성되었나요?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [결과 집합 메타데이터](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [열 바인딩](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [데이터 페치](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)
