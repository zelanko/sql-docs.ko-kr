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
manager: craigg
ms.openlocfilehash: 8eb98d7c17663894e1bacdc27e431d6a54f45d3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468669"
---
# <a name="retrieving-results-basic"></a>결과 검색(기본)
A *결과 집합* 특정 조건과 일치 하는 데이터 원본에 대 한 행의 집합이 있습니다. 이 쿼리에서 결과 사용할 수 있는 응용 프로그램에 테이블 형식에서 및 개념적 테이블입니다. **선택** 문, 카탈로그 함수 및 일부 프로시저의 결과 집합을 만듭니다. 다음 예에서 첫 번째 SQL 문 결과 행을 모두 Orders 테이블의 모든 열이 포함 된 집합을 만들고 두 번째 SQL 문을 만듭니다 Orders 테이블의 행에 대 한 OrderID, SalesPerson 및 상태 열이 포함 된 resultset 상태는 OPEN입니다.  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 결과 집합을 비어 있을 수는 없습니다 결과 집합을 전혀 다릅니다. 예를 들어, 다음 SQL 문은 빈 결과 집합을 만듭니다.  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 빈 결과 집합을 다른 결과 집합을 제외 하 고 해당 행이 없는 다르지 않습니다. 예를 들어, 응용 프로그램 결과 집합에 대 한 메타 데이터를 검색할 수 있습니다, 행을 인출 하려고 할 수 있습니다 및 결과 집합에 대해 커서를 닫아야 합니다.  
  
 데이터 원본에서 행을 검색 하 고 응용 프로그램에 반환 하는 프로세스 라고 *페치*합니다. 이 섹션에서는 해당 프로세스의 기본적인 부분을 설명 합니다. 블록 및 스크롤 가능 커서와 같은 좀 더 고급 항목에 대 한 정보를 참조 하세요. [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 하 고 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다. 업데이트에 대 한 내용은 삭제 및 삽입 행을 참조 하세요 [업데이트 데이터 개요](../../../odbc/reference/develop-app/updating-data-overview.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 집합이 생성되었습니까?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [결과 집합 메타데이터](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [열 바인딩](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [데이터 페치](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)
