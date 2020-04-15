---
title: 커서 및 준비된 명세서에 대한 거래의 영향 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef3cb4095410b8ccb03b0a138f65b8df2cfb1a4b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300473"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>커서 및 준비된 명령문에 트랜잭션이 미치는 영향
트랜잭션커밋 또는 롤백은 커서 및 액세스 계획에 다음과 같은 영향을 미칩니다.  
  
-   모든 커서가 닫히고 해당 연결에서 준비된 명령문에 대한 액세스 계획이 삭제됩니다.  
  
-   모든 커서가 닫혀 있고 해당 연결에 대해 준비된 명령문에 대한 액세스 계획은 그대로 유지됩니다.  
  
-   모든 커서는 열려 있고 해당 연결에 대해 준비된 명령문에 대한 액세스 계획은 그대로 유지됩니다.  
  
 예를 들어 데이터 원본이 이 목록에서 가장 제한적인 첫 번째 동작을 나타낸다고 가정합니다. 이제 응용 프로그램이 다음을 수행한다고 가정합니다.  
  
1.  커밋 모드를 수동 커밋으로 설정합니다.  
  
2.  명령문 1에 판매 주문의 결과 집합을 만듭니다.  
  
3.  사용자가 해당 주문을 강조 할 때 명령문 2에 판매 순서에 줄의 결과 집합을 만듭니다.  
  
4.  **SQLExecute를** 호출하여 사용자가 줄을 업데이트할 때 문 3에 준비된 위치 가 있는 업데이트 문을 실행합니다.  
  
5.  **SQLEndTran을** 호출하여 위치 가 있는 업데이트 문을 커밋합니다.  
  
 데이터 원본의 동작으로 인해 5단계에서 **SQLEndTran을** 호출하면 문 1과 2의 커서를 닫고 모든 명령문에 대한 액세스 계획을 삭제합니다. 응용 프로그램은 명령문 1과 2를 다시 실행하여 결과 집합을 다시 만들고 문 3에 대한 문을 다시 준비해야 합니다.  
  
 자동 커밋 **모드에서는 SQLEndTran** 이외 함수가 트랜잭션을 커밋합니다.  
  
-   **SQLExecute** 또는 **SQLExecDirect** 앞의 예에서 **4단계에서 SQLExecute** 호출은 트랜잭션을 커밋합니다. 이렇게 하면 데이터 원본이 문 1과 2의 커서를 닫고 해당 연결의 모든 명령문에 대한 액세스 계획을 삭제합니다.  
  
-   **SQLBulkOperations** 또는 **SQLSetPos** 위의 예에서 응용 프로그램이 문 3에 위치 된 업데이트 문을 실행 하는 대신 문 2에 SQL_UPDATE 옵션으로 **SQLSetPos를** 호출 하는 경우를 가정 합니다. 이렇게 하면 트랜잭션이 커밋되고 데이터 원본이 문 1과 2의 커서를 닫고 해당 연결의 모든 액세스 계획을 삭제합니다.  
  
-   **SQL닫닫는 커서** 앞의 예제에서 사용자가 다른 판매 순서를 강조 강조 할 때 응용 프로그램이 새 판매 주문에 대한 줄의 결과를 만들기 전에 문 2에서 **SQLCloseCursor를** 호출한다고 가정합니다. **SQLCloseCursor에** 대한 호출은 결과 줄 집합을 만든 **SELECT** 문을 커밋하고 데이터 원본이 문 1에서 커서를 닫은 다음 해당 연결의 모든 액세스 계획을 삭제합니다.  
  
 사용자가 결과 집합을 스크롤하고 행을 업데이트하거나 삭제하는 응용 프로그램, 특히 화면 기반 응용 프로그램은 이 동작에 대해 코딩할 때 주의해야 합니다.  
  
 트랜잭션이 커밋되거나 롤백될 때 데이터 원본이 어떻게 행동하는지 확인하기 위해 응용 프로그램은 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 사용하여 **SQLGetInfo를** 호출합니다.
