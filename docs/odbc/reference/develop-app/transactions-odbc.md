---
title: 거래 ODBC | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a40c34b2abeb346c7a718994ba2484bfc728e2b1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297958"
---
# <a name="transactions-odbc"></a>트랜잭션 ODBC
*트랜잭션은* 단일 원자성 작업으로 수행되는 작업 단위입니다. 즉, 작업이 전체적으로 성공하거나 실패합니다. 예를 들어 한 은행 계좌에서 다른 은행 계좌로 송금하는 것이 좋습니다. 이것은 두 단계를 포함 : 첫 번째 계정에서 돈을 인출하고 두 번째에 입금. 두 단계가 모두 성공하는 것이 중요합니다. 한 단계가 성공하고 다른 단계가 실패하는 것은 허용되지 않습니다. 트랜잭션을 지원하는 데이터베이스는 이를 보장할 수 있습니다.  
  
 트랜잭션을 *커밋하거나* *롤백하여*완료할 수 있습니다. 트랜잭션이 커밋되면 해당 트랜잭션의 변경 내용이 영구적으로 수행됩니다. 트랜잭션이 롤백되면 영향을 받는 행은 트랜잭션이 시작되기 전에 있던 상태로 반환됩니다. 계정 이전 예제를 확장하기 위해 응용 프로그램은 첫 번째 계정을 인출하기 위해 하나의 SQL 문을 실행하고 다른 SQL 문을 실행하여 두 번째 계정에 크레딧을 할당합니다. 두 문이 모두 성공하면 응용 프로그램은 트랜잭션을 커밋합니다. 그러나 어떤 이유로든 두 명령문이 실패하면 응용 프로그램은 트랜잭션을 롤백합니다. 두 경우 모두 응용 프로그램은 트랜잭션이 끝날 때 일관된 상태를 보장합니다.  
  
 단일 트랜잭션에는 서로 다른 시간에 발생하는 여러 데이터베이스 작업이 포함될 수 있습니다. 다른 트랜잭션이 중간 결과에 완전히 액세스할 수 있는 경우 트랜잭션이 서로 간섭할 수 있습니다. 예를 들어 한 트랜잭션이 행을 삽입하고 두 번째 트랜잭션이 해당 행을 읽고 첫 번째 트랜잭션이 롤백한다고 가정합니다. 이제 두 번째 트랜잭션에는 존재하지 않는 행에 대한 데이터가 있습니다.  
  
 이 문제를 해결하기 위해 트랜잭션을 서로 격리하는 다양한 체계가 있습니다. *트랜잭션 격리는* 일반적으로 행을 잠그면 동시에 동일한 행을 사용하는 것이 두 개 이상의 트랜잭션을 배제하여 구현됩니다. 일부 데이터베이스에서는 행을 잠그면 다른 행이 잠글 수도 있습니다.  
  
 트랜잭션 격리가 증가하면 *동시성이* 감소하거나 두 트랜잭션이 동시에 동일한 데이터를 사용할 수 있습니다. 자세한 내용은 [트랜잭션 격리 수준 설정을](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC의 트랜잭션](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [동시성 제어](../../../odbc/reference/develop-app/concurrency-control.md)
