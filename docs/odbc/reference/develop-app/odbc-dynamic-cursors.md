---
title: 동적 커서를 ODBC | Microsoft Docs
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
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 706bf3a92122e025977d092c06668fc646f2b6e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912878"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 동적 커서
동적 커서는 해당: 동적입니다. 멤버 자격, 순서 및 커서가 열린 후에 결과 집합의 값에 대 한 변경 내용을 감지할 수 있습니다. 예를 들어 두 개의 행을 인출 하는 동적 커서 및 다른 응용 프로그램에서 다음 행 중 하나를 업데이트 하 고 다른 삭제 합니다. 동적 커서는 행을 다시 인출 하려고 합니다, 삭제 된 행을 찾지 못합니다 이지만 업데이트 된 행에 대 한 새 값을 반환 합니다.  
  
 모든 업데이트를 검색 하는 동적 커서를 삭제 하 고 둘 다 삽입가 자신과 다른 사람이 수행한 합니다. (이 될 수는 격리 수준 SQL_ATTR_TXN_ISOLATION 연결 특성에서 설정한 대로 트랜잭션의 있습니다.) SQL_ATTR_ROW_STATUS_PTR 문 특성에 지정 된 행 상태 배열이 이러한 변경 내용을 반영 되어 있으며 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED, 및 SQL_ROW_ADDED 포함 될 수 있습니다. 동적 커서는 행 집합 외부에 있는 삭제 된 행을 반환 하지 않는 하 고 따라서 결과 집합에서 삭제 된 행 또는 행 상태 배열이의 해당 요소 있는지를 더 이상 인식 하기 때문에 SQL_ROW_DELETED를 반환할 수 없습니다. SQL_ROW_ADDED를 호출 하 여 행이 업데이트 하는 경우에 반환 됩니다 **SQLSetPos**, 다른 커서에 의해 업데이트 되는 경우에 없습니다.  
  
 데이터베이스에서 동적 커서를 구현 하는 한 가지 방법으로 멤버 자격을 정의 하는 선택적 인덱스를 만들고 결과의 순서 지정 하 여 설정 됩니다. 다른 사용자가 변경할 때 인덱스가 업데이트를 하기 때문에 이와 같은 인덱스에 따라 커서가 모든 변경 내용에 민감합니다. 이 인덱스에 의해 정의 된 결과 집합 내에서 추가 선택 된 인덱스에 따라 처리에 의해 불가능 합니다.  
  
 결과 집합의 고유 키로 정렬할 수을 요구 하 여 동적 커서를 시뮬레이션할 수 있습니다. 이러한 제한이 있는 인출을 실행 하 여 내용이 **선택** 문이 될 때마다 행을 인출 하는 커서입니다. 예를 들어이 문에서 결과 집합 정의 되어 있다고 가정 합니다.  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 이 결과 집합의 다음 행 집합을 인출 하는 시뮬레이션 된 커서 다음에서 매개 변수를 설정 **선택** 문을 현재 행 집합의 마지막 행의 값에 다음 실행:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 이 문은 첫 번째 행의 원래 결과 집합의 다음 행 집합은 두 번째 결과 집합을 만듭니다-이 경우 Customers 테이블의 행 집합입니다. 커서는 응용 프로그램에이 행 집합을 반환합니다.  
  
 보면 흥미롭습니다 이런이 방식으로 구현 되는 동적 커서 많은 결과 집합을 생성 하는 실제로 원래 결과 집합에 변경 내용을 검색할 수 있습니다. 이러한 보조 결과 집합이 있는지 식별 되지 응용 프로그램 단순히 커서가 원래 결과 집합에 변경 내용을 검색할 수 있는 처럼 나타납니다.
