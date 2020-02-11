---
title: 커서 및 준비 된 문의 트랜잭션 효과 | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046884"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>커서 및 준비된 명령문에 트랜잭션이 미치는 영향
트랜잭션을 커밋하거나 롤백하려면 커서 및 액세스 계획에 다음과 같은 영향을 미칠 것입니다.  
  
-   모든 커서가 닫히고 해당 연결의 준비 된 문에 대 한 액세스 계획이 삭제 됩니다.  
  
-   모든 커서가 닫히고 해당 연결에 대 한 준비 된 문의 액세스 계획이 그대로 유지 됩니다.  
  
-   모든 커서는 열린 상태를 유지 하 고 해당 연결에 대 한 준비 된 문의 액세스 계획은 그대로 유지 됩니다.  
  
 예를 들어 데이터 원본에서이 목록의 첫 번째 동작을 표시 한다고 가정 합니다. 이러한 동작은 가장 제한적입니다. 이제 응용 프로그램에서 다음을 수행 한다고 가정 합니다.  
  
1.  커밋 모드를 수동 커밋으로 설정 합니다.  
  
2.  문 1에서 판매 주문의 결과 집합을 만듭니다.  
  
3.  사용자가 해당 주문을 강조 표시할 때 문 2의 판매 주문에 있는 줄의 결과 집합을 만듭니다.  
  
4.  는 **Sqlexecute** 를 호출 하 여 사용자가 줄을 업데이트할 때 문 3에서 준비 된 위치 지정 update 문을 실행 합니다.  
  
5.  는 **Sqlendtran** 을 호출 하 여 위치 지정 update 문을 커밋합니다.  
  
 데이터 원본의 동작으로 인해 5 단계에서 **Sqlendtran** 을 호출 하면 문 1과 2에 대 한 커서를 닫고 모든 문에 대 한 액세스 계획을 삭제 합니다. 응용 프로그램은 결과 집합을 다시 만들고 문 3에서 문을 다시 준비 하기 위해 문 1과 2를 다시 생성 해야 합니다.  
  
 자동 커밋 모드에서 **Sqlendtran** commit 트랜잭션 이외의 함수:  
  
-   **Sqlexecute** 또는 **sqlexecdirect** 위의 예제에서 4 단계에서 **sqlexecute** 를 호출 하면 트랜잭션이 커밋됩니다. 이렇게 하면 데이터 원본에서 문 1과 2의 커서를 닫고 해당 연결의 모든 문에 대 한 액세스 계획을 삭제 합니다.  
  
-   **SQLBulkOperations** 또는 **SQLSetPos** 위의 예제에서 4 단계에서 응용 프로그램은 문 3에서 위치 지정 UPDATE 문을 실행 하는 대신 문의 2에 있는 SQL_UPDATE 옵션을 사용 하 여 **SQLSetPos** 를 호출 한다고 가정 합니다. 이렇게 하면 트랜잭션이 커밋되고 데이터 원본이 문의 1과 2에 대 한 커서를 닫고 해당 연결에 대 한 모든 액세스 계획을 삭제 합니다.  
  
-   **SQLCloseCursor** 앞의 예제에서 사용자가 다른 판매 주문을 강조 표시 하면 응용 프로그램은 새 판매 주문에 대 한 줄의 결과를 만들기 전에 문 2에서 **SQLCloseCursor** 를 호출 한다고 가정 합니다. **SQLCloseCursor** 에 대 한 호출은 행의 결과 집합을 만든 **SELECT** 문을 커밋하고 데이터 소스가 문 1에서 커서를 닫은 다음 해당 연결에 대 한 모든 액세스 계획을 삭제 합니다.  
  
 응용 프로그램, 특히 사용자가 결과 집합 주위를 스크롤하고 행을 업데이트 하거나 삭제 하는 화면 기반 응용 프로그램은이 동작을 코딩 하는 데 주의 해야 합니다.  
  
 트랜잭션이 커밋되거나 롤백될 때 데이터 소스가 어떻게 동작 하는지 확인 하기 위해 응용 프로그램은 SQL_CURSOR_COMMIT_BEHAVIOR 및 SQL_CURSOR_ROLLBACK_BEHAVIOR 옵션으로 **SQLGetInfo** 를 호출 합니다.
