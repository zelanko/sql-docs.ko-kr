---
title: 동시성 제어 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e54298e9c25777f10b92f322f1b1e6a3d94c243
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191754"
---
# <a name="concurrency-control"></a>동시성 제어
*동시성* 는 동시에 동일한 데이터를 사용 하는 두 개의 트랜잭션이의 기능 및 향상 된 트랜잭션 격리 일반적으로 추가 되어 동시성이 줄어들된 합니다. 잠금 행에서 트랜잭션 격리는 일반적으로 구현 하는 트랜잭션을 더 적게 잠긴된 행으로 적어도 일시적으로 차단 되지 않고 수행할 행이 더 잠겨, 때문입니다. 동시성이 줄어들된는 일반적으로 데이터베이스 무결성을 유지 하는 데 필요한 더 높은 트랜잭션 격리 수준에 대 한 절충안으로 허용 되지만, 커서를 사용 하는 높은 읽기/쓰기 작업을 사용 하 여 대화형 응용 프로그램에서 문제가 될 수 있습니다.  
  
 예를 들어, 응용 프로그램에는 SQL 문을 실행 **선택 \* 에서 주문**합니다. 호출한 **SQLFetchScroll** 결과 내 설정 및 업데이트를 사용 하면 삭제 또는 주문을 삽입 합니다. 사용자 업데이트, 삭제, 주문을 삽입 한 후 응용 프로그램에는 트랜잭션을 커밋합니다.  
  
 격리 수준이 Repeatable Read 이면 트랜잭션이 잠길 수 있습니다--구현 방법을 따라에서 반환한 각 행 **SQLFetchScroll**합니다. 격리 수준이 Serializable 인 경우 트랜잭션이 전체 주문 테이블을 잠글 수 있습니다. 두 경우 모두 트랜잭션이 커밋되거나 롤백되는 경우에 해당 잠금을 해제 합니다. 따라서 사용자 주문과 업데이트, 삭제 시간이 읽기 시간이 많이 소비 또는 삽입, 트랜잭션 수는 많은 수의 행을 다른 사용자에 게 사용할 수 있도록 고정 됩니다.  
  
 커서가 읽기 전용 및 응용 프로그램 사용자가 기존 주문만 읽기를 허용 하는 경우에 문제입니다. 응용 프로그램의 트랜잭션을 커밋합니다.이 경우 및 호출할 때 잠금 해제 **SQLCloseCursor** (자동 커밋 모드)에서 또는 **SQLEndTran** (수동 커밋 모드에서).  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [동시성 유형](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)
