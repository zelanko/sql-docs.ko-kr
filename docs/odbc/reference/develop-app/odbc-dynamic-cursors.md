---
title: ODBC 동적 커서 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 628de07f90de47efb0546dff84c03f56efb0674c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086304"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 동적 커서
동적 커서는 동적 커서입니다. 커서를 연 후 결과 집합의 멤버 자격, 순서 및 값에 대 한 변경 내용을 검색할 수 있습니다. 예를 들어 동적 커서가 두 행을 페치하고 다른 애플리케이션이 해당 행 중 하나를 업데이트하고 다른 행을 삭제한다고 가정합니다. 그런 다음 동적 커서는 이러한 행을 다시 페치 시도 하지만 삭제 된 행을 찾지는 않지만 업데이트 된 행의 새 값을 반환 합니다.  
  
 동적 커서는 모든 업데이트, 삭제 및 삽입을 모두 검색 하 고 다른 사용자가 수행한 모든 업데이트, 삭제 및 삽입을 검색 합니다. 이는 SQL_ATTR_TXN_ISOLATION 연결 특성에 의해 설정 된 트랜잭션의 격리 수준이 적용 됩니다. SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 지정 된 행 상태 배열은 이러한 변경 내용을 반영 하 고 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED 및 SQL_ROW_ADDED 포함할 수 있습니다. 동적 커서가 행 집합 외부에서 삭제 된 행을 반환 하지 않기 때문에 SQL_ROW_DELETED를 반환할 수 없습니다. 따라서 결과 집합 또는 행 상태 배열의 해당 요소에 삭제 된 행이 존재 하는 것을 더 이상 인식 하지 못합니다. SQL_ROW_ADDED는 다른 커서에 의해 업데이트 될 때가 아니라 **SQLSetPos**를 호출 하 여 행을 업데이트 하는 경우에만 반환 됩니다.  
  
 데이터베이스에서 동적 커서를 구현 하는 한 가지 방법은 결과 집합의 멤버 자격과 순서를 정의 하는 선택적 인덱스를 만드는 것입니다. 인덱스는 다른 사용자가 변경할 때 업데이트 되므로 이러한 인덱스를 기반으로 하는 커서는 모든 변경 내용을 인식 합니다. 인덱스를 따라 처리 하면이 인덱스에 의해 정의 된 결과 집합 내에서 추가로 선택할 수 있습니다.  
  
 동적 커서는 고유 키를 기준으로 결과 집합을 정렬 하도록 하 여 시뮬레이션할 수 있습니다. 이러한 제한을 사용 하면 커서에서 행을 인출할 때마다 **SELECT** 문을 실행 하 여 반입이 수행 됩니다. 예를 들어 다음 문으로 결과 집합이 정의 되어 있다고 가정 합니다.  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 이 결과 집합에서 다음 행 집합을 인출 하기 위해 시뮬레이트된 커서는 다음 **SELECT** 문의 매개 변수를 현재 행 집합의 마지막 행에 있는 값으로 설정 하 고 실행 합니다.  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 이 문은 두 번째 결과 집합을 만듭니다. 첫 번째 행 집합은 원래 결과 집합의 다음 행 집합입니다 .이 경우에는 Customers 테이블의 행 집합입니다. 커서는 응용 프로그램에이 행 집합을 반환 합니다.  
  
 이러한 방식으로 구현 된 동적 커서는 원래 결과 집합에 대 한 변경 내용을 검색할 수 있는 많은 결과 집합을 생성 한다는 점에 주목 해야 합니다. 응용 프로그램은 이러한 보조 결과 집합의 존재를 학습 하지 않습니다. 커서에서 원래 결과 집합에 대 한 변경 내용을 검색할 수 있는 것 처럼 표시 됩니다.
