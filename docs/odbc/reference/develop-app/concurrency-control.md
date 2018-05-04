---
title: 동시성 제어 | Microsoft Docs
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
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fd05a84e70b601180ce67a94cbdc4caabf7e37e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="concurrency-control"></a>동시성 제어
*동시성* 같은 시간에 동일한 데이터를 사용 하는 두 개의 트랜잭션 기능 이며 증가 된 트랜잭션 격리는 대개 제공 동시성이 줄어들된 합니다. 트랜잭션 격리는 잠금 행에서 일반적으로 구현 하 고 잠긴된 행에 의해 적어도 일시적으로 차단 되지 않고 더 적은 트랜잭션을 완료할 수 있습니다 더 많은 행 잠겨 있기 때문입니다. 데이터베이스 무결성을 유지 하는 데 필요한 높은 트랜잭션 격리 수준에 대 한 절충안으로 동시성이 줄어들된은 일반적으로 허용 하는 동안 커서를 사용 하는 높은 읽기/쓰기 작업으로 대화형 응용 프로그램에서 문제가 될 수 있습니다.  
  
 예를 들어, SQL 문을 실행 하는 응용 프로그램 **선택 \* 에서 주문**합니다. 호출 **SQLFetchScroll** 스크롤 하는 결과 집합 및 업데이트를 사용 하면 삭제 또는 삽입 주문 합니다. 사용자를 업데이트, 삭제 또는 삽입 순서, 후 응용 프로그램에는 트랜잭션을 커밋합니다.  
  
 격리 수준이 Repeatable Read 이면 트랜잭션이 수-어떻게 구현 되었는지에 따라-에서 반환한 각 행을 잠그는 **SQLFetchScroll**합니다. 격리 수준이 Serializable 인 트랜잭션이 전체 Orders 테이블을 잠길 수 있습니다. 두 경우 모두 트랜잭션이 커밋되거나 롤백될 때에 해당 잠금을 해제 합니다. 따라서 사용자 주문과 업데이트, 삭제, 시간이 거의 읽기 시간에서 자주 또는 삽입 하는 트랜잭션 수 쉽게 하는 경우에 많은 수의 행을 다른 사용자가 사용할 수 있도록 잠급니다.  
  
 커서는 읽기 전용 및 응용 프로그램을 사용 하면 기존 주문만 읽을 경우에 문제가입니다. 이 경우 응용 프로그램으로 트랜잭션을 커밋합니다 만들고, 잠금을 해제를 호출할 때 **SQLCloseCursor** (자동 커밋 모드)에서 또는 **SQLEndTran** (수동 커밋 모드에서).  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [동시성 유형](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)
