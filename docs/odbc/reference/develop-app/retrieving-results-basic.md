---
title: 결과 검색 (기본) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020474"
---
# <a name="retrieving-results-basic"></a>결과 검색(기본)
*결과 집합* 은 특정 조건과 일치 하는 데이터 원본에 대 한 행 집합입니다. 이 테이블은 쿼리에서 생성 되 고 테이블 형식으로 응용 프로그램에 사용할 수 있는 개념적 테이블입니다. **SELECT** 문, 카탈로그 함수 및 일부 프로시저에서 결과 집합을 만듭니다. 다음 예에서는 첫 번째 SQL 문이 Orders 테이블의 모든 행과 모든 열을 포함 하는 결과 집합을 생성 하 고, 두 번째 SQL 문은 Orders 테이블의 행에 대해 OrderID, 판매원 및 상태 열을 포함 하는 결과 집합을 만듭니다. 상태가 열린 상태:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 결과 집합은 비어 있을 수 있습니다 .이는 결과 집합과 전혀 다르지 않습니다. 예를 들어 다음 SQL 문은 빈 결과 집합을 만듭니다.  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 빈 결과 집합은 행을 포함 하지 않는다는 점을 제외 하 고는 다른 결과 집합과는 다릅니다. 예를 들어 응용 프로그램은 결과 집합에 대 한 메타 데이터를 검색 하 고, 행 페치를 시도할 수 있으며, 결과 집합 위에 커서를 닫아야 합니다.  
  
 데이터 원본에서 행을 검색 하 고 응용 프로그램에 반환 하는 프로세스를 *인출*이라고 합니다. 이 섹션에서는 해당 프로세스의 기본 부분에 대해 설명 합니다. 블록 및 스크롤 가능 커서와 같은 고급 항목에 대 한 자세한 내용은 [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 및 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)를 참조 하세요. 행을 업데이트, 삭제 및 삽입 하는 방법에 대 한 자세한 내용은 [데이터 업데이트 개요](../../../odbc/reference/develop-app/updating-data-overview.md)를 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 집합이 생성되었나요?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [결과 집합 메타데이터](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [열 바인딩](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [데이터 페치](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)
