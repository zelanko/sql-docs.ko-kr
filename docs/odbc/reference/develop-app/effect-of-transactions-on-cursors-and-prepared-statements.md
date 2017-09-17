---
title: "커서 및 준비 된 문을에 트랜잭션의 영향 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2533778f9b0e837ce59850d4f70a3c4545f8be60
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>커서 및 준비 된 문을에 트랜잭션이 미치는 영향
커밋 또는 롤백 트랜잭션이 커서 및 액세스 계획에 다음과 같은 결과가 나타납니다.  
  
-   모든 커서가 닫히고 하 고 해당 연결에서 준비 된 문에 대 한 액세스 계획 삭제 됩니다.  
  
-   모든 커서, 닫혀 있고 해당 연결에서 준비 된 문에 대 한 액세스 계획 그대로 유지 합니다.  
  
-   모든 커서는 계속 열려 하 고 해당 연결에서 준비 된 문에 대 한 액세스 계획 그대로 유지 합니다.  
  
 예를 들어, 데이터 원본에서 이러한 동작 중에서 가장 제한적이 목록의 첫 번째 동작을 보여 줍니다. 이제 응용 프로그램에서 다음을 수행 한다고 가정 합니다.  
  
1.  커밋 모드를 수동 커밋 모드로 설정 합니다.  
  
2.  문에서 1 판매 주문의 결과 집합을 만듭니다.  
  
3.  이 순서를 강조 표시할 때 문에서 2, 판매 주문에서 줄은 결과 집합을 만듭니다.  
  
4.  호출 **SQLExecute** 사용자 줄을 업데이트 한 경우 문에서 3, 준비 된 위치 지정된 update 문을 실행 하려면.  
  
5.  호출 **SQLEndTran** 위치 지정된 update 문을 커밋할 수 있습니다.  
  
 데이터 소스의 동작에 대 한 호출 때문에 **SQLEndTran** 단계에서 5 인해 모든 문에서 액세스 계획을 삭제 하 고 문 1과 2에 대 한 커서를 닫습니다 되도록 합니다. 응용 프로그램 1과 2 결과 다시 만들려고 문 집합을 다시 실행 하려고 하 고 3 문에서 문 reprepare 해야 합니다.  
  
 자동 커밋 모드에서 이외의 함수 **SQLEndTran** 트랜잭션을 커밋합니다.  
  
-   **SQLExecute** 또는 **SQLExecDirect** 앞의 예제에 대 한 호출에서 **SQLExecute** 4 단계에서 트랜잭션을 커밋합니다. 그러면 데이터 소스를 문 1과 2에 커서를 닫고 해당 연결에서 모든 문에서 액세스 계획을 삭제 합니다.  
  
-   **SQLBulkOperations** 또는 **SQLSetPos** 앞의 예제에서 4 단계에서 응용 프로그램 호출 하 라고 가정해 보겠습니다. **SQLSetPos** statement 2 실행 하는 대신 SQL_UPDATE 옵션이 update 문의 문 3에 배치 됩니다. 이 트랜잭션을 커밋합니다 및 문 1과 2에 커서를 닫는 데이터 원본을 사용 하면 고 해당 연결에서 모든 액세스 계획을 무시 합니다.  
  
-   **SQLCloseCursor** 앞의 예제에서 다른 판매 주문의 강조 표시할 때 응용 프로그램 호출 하는 라고 가정해 보겠습니다. **SQLCloseCursor** 에 새 판매에 대 한 줄의 결과 만들기 전에 문을 2 순서입니다. 에 대 한 호출 **SQLCloseCursor** 커밋합니다는 **선택** 줄의 결과 집합을 생성 하 고 데이터 소스를 1, 문에서 커서 닫기 사용 하면 다음 그에 대 한 액세스 계획을 모두 삭제 하는 문 연결입니다.  
  
 응용 프로그램, 특히 화면 기반 응용 프로그램 사용자는 결과 집합 및 업데이트를 스크롤할 또는 행을 삭제 합니다.이 문제를 해결 하는 코드에 주의 해야 합니다.  
  
 데이터 소스는 트랜잭션이 커밋되거나 롤백될 때 동작 하는 방식을 확인 하려면 응용 프로그램이 호출 **SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션입니다.
