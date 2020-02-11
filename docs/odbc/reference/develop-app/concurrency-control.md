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
ms.openlocfilehash: 7c541bf28c1d4c7ec2e2041201bd7c168625bb34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083257"
---
# <a name="concurrency-control"></a>동시성 제어
*동시성* 은 두 트랜잭션이 동시에 동일한 데이터를 사용 하는 기능이 며 트랜잭션 격리가 증가 하면 일반적으로 동시성이 줄어듭니다. 이는 일반적으로 트랜잭션 격리가 행 잠금에 의해 구현 되기 때문 이며, 더 많은 행이 잠겨 있으므로 일시적으로 잠긴 행에 의해 차단 되지 않고 트랜잭션을 더 적게 완료할 수 있습니다. 축소 된 동시성은 일반적으로 데이터베이스 무결성을 유지 하는 데 필요한 높은 트랜잭션 격리 수준에 대 한 절충으로 허용 되지만 커서를 사용 하는 읽기/쓰기 작업이 많은 대화형 응용 프로그램에서 문제가 될 수 있습니다.  
  
 예를 들어 응용 프로그램이 SQL 문 ** \* select FROM Orders**를 실행 한다고 가정 합니다. 이 메서드는 **Sqlfetchscroll** 을 호출 하 여 결과 집합 주위를 스크롤하고 사용자가 주문을 업데이트, 삭제 또는 삽입할 수 있습니다. 사용자가 주문을 업데이트, 삭제 또는 삽입 하면 응용 프로그램이 트랜잭션을 커밋합니다.  
  
 격리 수준을 반복 읽기로 설정 하면 트랜잭션이 구현 된 방법에 따라 **Sqlfetchscroll**에서 반환 된 각 행을 잠급니다. 격리 수준을 직렬화 할 수 있는 경우 트랜잭션은 전체 Orders 테이블을 잠글 수 있습니다. 두 경우 모두 트랜잭션은 커밋되거나 롤백될 때만 잠금을 해제 합니다. 따라서 사용자가 주문을 읽는 데 많은 시간을 소비 하 고 매우 적은 시간을 업데이트, 삭제 또는 삽입 하는 경우에는 트랜잭션에서 많은 수의 행을 쉽게 잠그고 다른 사용자가 사용할 수 없게 만들 수 있습니다.  
  
 커서가 읽기 전용이 고 응용 프로그램에서 사용자에 게 기존 주문만 읽을 수 있는 경우에도이 문제가 발생 합니다. 이 경우 응용 프로그램은 트랜잭션을 커밋하고 **SQLCloseCursor** (자동 커밋 모드) 또는 **sqlendtran** (수동 커밋 모드)을 호출할 때 잠금을 해제 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [동시성 형식](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)
