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
manager: craigg
ms.openlocfilehash: 82df10e6b8effeb040b362dcf466eb173dfce4f9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629681"
---
# <a name="odbc-dynamic-cursors"></a>ODBC 동적 커서
동적 커서는: 동적입니다. 멤버 자격, 순서 및 커서가 열린 후에 결과 집합의 값에 대 한 변경 내용을 감지할 수 있습니다. 예를 들어 두 개의 행을 인출 하는 동적 커서 및 다른 응용 프로그램에서 그런 다음 이러한 행 중 하나를 업데이트 하 고 다른를 삭제 합니다. 동적 커서 해당 행을 다시 인출 하려고 시도 삭제 된 행을 찾지 못합니다 있지만 업데이트 된 행에 대 한 새 값이 반환 됩니다.  
  
 모든 업데이트를 검색 하는 동적 커서 삭제 및 삽입, 둘 다가 자신과 다른 사람이 수행한 합니다. (이 경우 격리 될 수 있습니다 SQL_ATTR_TXN_ISOLATION 연결 특성에서 설정한 대로 트랜잭션 수준) SQL_ATTR_ROW_STATUS_PTR 문 특성에 의해 지정 된 행 상태 배열 이러한 변경 내용이 반영 하 고 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED, 및 SQL_ROW_ADDED 포함 될 수 있습니다. 동적 커서 행 집합 외부에 있는 삭제 된 행 반환 되지 않으며 따라서 결과 집합에서 삭제 된 행 또는 행 상태 배열에 해당 하는 요소의 존재 여부를 더 이상 인식 하므로 sql_row_deleted가 반환할 수 없습니다. SQL_ROW_ADDED를 호출 하 여 행이 업데이트 하는 경우에 반환 됩니다 **SQLSetPos**다른 커서에서 업데이트 된 경우에 없습니다.  
  
 데이터베이스에서 동적 커서를 구현 하는 한 가지 방법은 멤버 자격을 정의 하는 선택적 인덱스를 만들고 결과의 순서 지정 하 여 설정 됩니다. 다른 사용자가 변경할 때 인덱스는 업데이트 되므로 이러한 인덱스를 기반으로 커서가 모든 변경 내용에 민감합니다. 이 인덱스에서 정의 된 결과 집합 내에서 추가 선택 된 인덱스에 따라 처리에 의해 불가능 합니다.  
  
 동적 커서는 결과 집합 고유 키를 요구 하 여 시뮬레이션할 수 있습니다. 이러한 제한을 사용 하 여 실행 하 여 인출 됩니다는 **선택** 문을 커서 행을 인출 하는 각 시간입니다. 예를 들어 결과 집합은이 문에 의해 정의 됩니다.  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 이 결과 집합의 다음 행 집합을 페치 하려면 시뮬레이션 된 커서가 다음에서 매개 변수를 설정 **선택** 현재 행 집합의 마지막 행의 값으로 문을 다음 실행 합니다.  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 이 문은 두 번째 결과 집합의 첫 번째 행은 원래 결과 집합의 다음 행 집합을 만듭니다-여기서는 Customers 테이블의 행 집합입니다. 커서는 응용 프로그램에이 행 집합을 반환합니다.  
  
 이 원래 결과 집합에 변경 내용을 검색할 수 있도록이 방식으로 구현 되는 동적 커서에 실제로 여러 결과 집합을 만듭니다 흥미롭습니다. 이러한 보조 결과 집합이 존재 하지 응용 프로그램 학습 단순히 커서를 원래 결과 집합에 변경 내용을 검색 하는 일을 할 것 처럼 표시 됩니다.
