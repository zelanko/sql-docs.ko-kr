---
title: 결과 (기본) 검색 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b09820c0716d6d7a8261ede3b5a4173dc73f384d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913008"
---
# <a name="retrieving-results-basic"></a>결과 (기본) 검색
A *결과 집합* 는 특정 조건에 일치 하는 데이터 원본에 있는 행의 집합입니다. 해당 하는 쿼리 생성 되며를 테이블 형식으로 응용 프로그램에 사용할 수 있는 개념적 테이블입니다. **선택** 문, 카탈로그 함수 및 일부 절차 결과 집합을 만듭니다. 다음 예제에서는 첫 번째 SQL 문을 모든 행 및 Orders 테이블의 모든 열을 포함 한 결과 집합을 만든 두 번째 SQL 문은 Orders 테이블의 행에 대 한 OrderID, 영업 사원, 및 상태 열을 포함 한 결과 집합을 만듭니다. 상태는 OPEN입니다.  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 결과 집합을 전혀 없음와에서 다른 결과 집합, 비어 있을 수 있습니다. 예를 들어 다음 SQL 문은 빈 결과 집합을 만듭니다.  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 빈 결과 집합이 다른 결과 집합을 행이 없는 있다는 점을 제외 하 고 다르지 않습니다. 예를 들어 응용 프로그램이 결과 집합에 대 한 메타 데이터를 검색할 수, 행을 인출 하려고 할 수 있습니다 및 결과 집합에서 커서를 닫아야 합니다.  
  
 데이터 원본에서 행을 검색 하 고 응용 프로그램에 반환 하기는 프로세스 라고 *인출*합니다. 이 섹션에서는 해당 프로세스의 기본 부분에 설명 합니다. 스크롤 가능 커서 블록 등의 추가적인 고급 항목에 대 한 정보를 참조 하십시오. [블록 커서](../../../odbc/reference/develop-app/block-cursors.md) 및 [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)합니다. 업데이트에 대 한 정보, 삭제 및 삽입 행 참조 [업데이트 데이터 개요](../../../odbc/reference/develop-app/updating-data-overview.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [결과 집합이 생성되었습니까?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [결과 집합 메타데이터](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [열 바인딩](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [데이터 페치](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [커서 닫기](../../../odbc/reference/develop-app/closing-the-cursor.md)
