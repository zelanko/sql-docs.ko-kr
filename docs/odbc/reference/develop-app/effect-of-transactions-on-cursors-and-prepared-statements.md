---
title: 커서 및 준비 된 문은 트랜잭션의 효과 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 83b693922d08f7298d0c5282fe2c7d1c20149d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046884"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>커서 및 준비된 명령문에 트랜잭션이 미치는 영향
커밋 또는 롤백 트랜잭션이 효과가 다음 커서에 대 한 액세스 계획:  
  
-   모든 커서, 닫혀 있고 해당 연결에서 준비 된 문에 대 한 액세스 계획 삭제 됩니다.  
  
-   모든 커서, 닫혀 있고 해당 연결에서 준비 된 문에 대 한 액세스 계획 그대로 유지 됩니다.  
  
-   모든 커서에 열려 있고 해당 연결에서 준비 된 문에 대 한 액세스 계획 그대로 유지 됩니다.  
  
 예를 들어, 데이터 원본에는 이러한 동작 중에서 가장 제한적이 목록의 첫 번째 동작이 나타납니다. 이제 응용 프로그램에서 다음을 수행 한다고 가정 합니다.  
  
1.  수동 커밋에 커밋 모드를 설정합니다.  
  
2.  문에서 1 판매 주문의 결과 집합을 만듭니다.  
  
3.  이 순서를 강조 표시할 때 문에서 2, 판매 주문에 줄은 결과 집합을 만듭니다.  
  
4.  호출 **SQLExecute** 사용자 줄을 업데이트 하는 경우 문에서 3, 준비 된 현재 위치 업데이트 문을 실행 합니다.  
  
5.  호출 **SQLEndTran** 위치 지정된 update 문이 커밋.  
  
 데이터 소스의 동작에 대 한 호출으로 인해 **SQLEndTran** 단계에서 5 하면 모든 문에서 액세스 계획을 삭제 하 고 문 1-2 시 커서 닫기 되도록 합니다. 응용 프로그램 결과 다시 만드는 데 1-2 문 집합을 다시 실행 하려고 하 고 3 문에서 문 reprepare 해야 합니다.  
  
 자동 커밋 모드에서는 함수 이외의 **SQLEndTran** 트랜잭션을 커밋합니다.  
  
-   **SQLExecute** 나 **SQLExecDirect** 앞의 예제에 대 한 호출에서 **SQLExecute** 4 단계에서 트랜잭션을 커밋합니다. 이렇게 하면 문 1 및 2에서 커서를 닫고 해당 연결에서 모든 문에서 액세스 계획을 삭제할 데이터 원본.  
  
-   **SQLBulkOperations** 나 **SQLSetPos** 앞의 예제에서 4 단계에서 응용 프로그램 호출을 가정해 보겠습니다 **SQLSetPos** SQL_UPDATE 옵션이 있는 statement 2 실행 하는 대신에 사용 하 여를 문에서 3 update 문을 배치 합니다. 이 트랜잭션을 커밋합니다 및 문 1 및 2, 시 커서 닫기에 데이터 소스 및 해당 연결에서 모든 액세스 계획을 삭제 합니다.  
  
-   **SQLCloseCursor** 앞의 예제에는 다른 판매 주문의 강조 하는 사용자, 응용 프로그램 호출을 가정 **SQLCloseCursor** 새로운 판매에 대 한 줄의 결과 만들기 전에 문에서 2 순서입니다. 에 대 한 호출 **SQLCloseCursor** 커밋합니다 합니다 **선택** 줄의 결과 집합을 생성 하 고 문 1 시 커서 닫기 데이터 원본을 사용 하면 다음에 모든 액세스 계획을 삭제 하는 문 연결입니다.  
  
 응용 프로그램, 특히 화면 기반 응용 프로그램 사용자의 결과 집합 및 업데이트를 스크롤할 또는 행을 삭제 합니다.이 문제를 해결 하는 코드에 주의 해야 합니다.  
  
 데이터 소스는 트랜잭션이 커밋되거나 롤백될 때 어떻게 동작 하는지 결정할 응용 프로그램 호출 **SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션을 사용 하 여 합니다.
