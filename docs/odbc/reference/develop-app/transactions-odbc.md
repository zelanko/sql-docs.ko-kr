---
title: 트랜잭션 ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fa56e9d1827b5a4335afb94fc8e69085e662009d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="transactions-odbc"></a>ODBC 트랜잭션
A *트랜잭션* 는 작업의 단위를 단일 원자성 작업으로 이루어집니다; 작업이 성공 하거나 전체 실패 즉, 합니다. 예를 들어 은행 계좌에서 간에 자금을 이체 하는 것이 좋습니다. 이 두 단계: 첫 번째 계정에서 금액을 취소 하 고 두 번째에서 입출금 계좌 합니다. 성공 하는 단계를 모두; 반드시 성공 하려면 1 단계 및 실패에 대 한 허용 되지 않습니다. 트랜잭션을 지 원하는 데이터베이스는이 보장할 수 있습니다.  
  
 트랜잭션을 있는 것으로 완료할 수 있습니다 *커밋된* 되 또는 *롤백*합니다. 트랜잭션이 커밋되기, 트랜잭션 내용이 영구적으로 반영 한다는 점에서 변경 합니다. 트랜잭션이 롤백되면 때 영향을 받는 행을 트랜잭션이 시작 전에의 상태로 반환 됩니다. 계정 전송 예제를 확장 하려면 응용 프로그램에 두 번째 계정 환불 다른 SQL 문 및 첫 번째 계좌에서 금액을 하나의 SQL 문을 실행 합니다. 두 문은 성공 하는 경우 응용 프로그램을 다음 트랜잭션을 커밋합니다. 하지만 어떤 이유로 든 실패 하면 두 문을 응용 프로그램의 트랜잭션을 롤백합니다. 두 경우 모두 응용 프로그램은 트랜잭션이 끝날 때 일관 된 상태를 보장합니다.  
  
 단일 트랜잭션으로 다른 시간에 발생 하는 여러 데이터베이스 작업에 포함 될 수 있습니다. 다른 트랜잭션의 중간 결과에 액세스할 수 있으면 트랜잭션이 서로 충돌할 수 있습니다. 예를 들어 한 트랜잭션에서 행을 삽입, 가정 두 번째 트랜잭션이 해당 행과 첫 번째 트랜잭션이 롤백되면 읽습니다. 이제 두 번째 트랜잭션이 존재 하지 않는 행에 대 한 데이터가 있습니다.  
  
 이 문제를 해결 하기 위해 다양 한 체계 트랜잭션이 서로 격리할 수 있습니다. *트랜잭션 격리* 일반적으로 구현 됩니다 잠금 행에서 동일한 행을 사용 하 여 동시에 둘 이상의 트랜잭션의 배제 하는 합니다. 일부 데이터베이스에서 행 잠금을 다른 행 잠글 수도 있습니다.  
  
 증가 된 트랜잭션와 격리 단점이 감소 *동시성,* 또는 동시에 동일한 데이터를 사용 하는 두 개의 트랜잭션 기능입니다. 자세한 내용은 참조 [트랜잭션 격리 수준을](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC의 트랜잭션](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [동시성 제어](../../../odbc/reference/develop-app/concurrency-control.md)
