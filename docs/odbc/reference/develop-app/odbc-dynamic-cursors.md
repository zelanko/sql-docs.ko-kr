---
title: ODBC 동적 커서 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f94b83ef1458cd9f8368d1bea3a39682bd80b1a2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302325"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 동적 커서
동적 커서는 동적입니다. 커서를 연 후 결과 집합의 멤버 자격, 순서 및 값에 대한 변경 내용을 검색할 수 있습니다. 예를 들어 동적 커서가 두 행을 페치하고 다른 애플리케이션이 해당 행 중 하나를 업데이트하고 다른 행을 삭제한다고 가정합니다. 동적 커서가 해당 행을 다시 가져오려고 하면 삭제된 행을 찾지 못하지만 업데이트된 행에 대한 새 값을 반환합니다.  
  
 동적 커서는 모든 업데이트, 삭제 및 삽입을 자체적으로 검색하고 다른 사용자가 만든 커서를 모두 검색합니다. 트랜잭션의 격리 수준에 따라 SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정 됩니다. SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정된 행 상태 배열은 이러한 변경 내용을 반영하며 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED 및 SQL_ROW_ADDED 포함할 수 있습니다. 동적 커서가 행 집합 외부에서 삭제된 행을 반환하지 않으므로 더 이상 결과 집합에 삭제된 행이 있는지 또는 행 상태 배열의 해당 요소가 있는지 인식하지 않으므로 SQL_ROW_DELETED 반환할 수 없습니다. SQL_ROW_ADDED 행이 다른 커서에 의해 업데이트될 때가 아니라 **SQLSetPos**호출에 의해 업데이트될 때만 반환됩니다.  
  
 데이터베이스에서 동적 커서를 구현하는 한 가지 방법은 결과 집합의 멤버 자격 및 순서를 정의하는 선택적 인덱스를 만드는 것입니다. 다른 사용자가 변경할 때 인덱스가 업데이트되므로 이러한 인덱스를 기반으로 하는 커서는 모든 변경 사항에 민감합니다. 이 인덱스에 의해 정의된 결과 집합 내에서 인덱스를 따라 처리하여 추가 선택을 할 수 있습니다.  
  
 동적 커서는 고유한 키로 결과 집합을 정렬하도록 요구하여 시뮬레이션할 수 있습니다. 이러한 제한으로 커서가 행을 가져올 때마다 **SELECT** 문을 실행하여 인출됩니다. 예를 들어 결과 집합이 이 명령문에 의해 정의되어 있다고 가정합니다.  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 이 결과 집합에서 다음 행 집합을 가져오려면 시뮬레이션된 커서는 다음 **SELECT** 문의 매개 변수를 현재 행 집합의 마지막 행의 값으로 설정한 다음을 실행합니다.  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 이 문은 두 번째 결과 집합을 만들고, 첫 번째 행 집합은 원래 결과 집합의 다음 행 집합입니다.이 경우 Customers 테이블의 행 집합입니다. 커서는 이 행 집합을 응용 프로그램에 반환합니다.  
  
 이러한 방식으로 구현된 동적 커서는 실제로 많은 결과 집합을 생성하여 원래 결과 집합의 변경 내용을 검색할 수 있다는 점에 유의해야 합니다. 응용 프로그램은 이러한 보조 결과 세트의 존재를 결코 알지 않습니다. 커서가 원래 결과 집합의 변경 내용을 감지할 수 있는 것처럼 간단하게 나타납니다.
