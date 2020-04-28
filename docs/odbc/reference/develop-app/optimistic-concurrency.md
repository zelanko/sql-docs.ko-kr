---
title: 낙관적 동시성 | Microsoft Docs
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
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 30eba3ea03b4c798a74a8cb928014b582846607b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282492"
---
# <a name="optimistic-concurrency"></a>낙관적 동시성
*낙관적 동시성* 은 트랜잭션 간의 충돌이 거의 발생 하지 않는다는 낙관적 가정에서 해당 이름을 파생 시킵니다. 현재 트랜잭션에서 읽은 시간과 업데이트 또는 삭제 시간 사이에 다른 트랜잭션이 데이터 행을 업데이트 하거나 삭제 하는 경우 충돌이 발생 한 것으로 간주 됩니다. 이는 응용 프로그램 개발자가 이러한 충돌이 발생 하는 것으로 판단 하는 *비관적 동시성* 또는 잠금과 반대입니다.  
  
 낙관적 동시성에서는 시간이 업데이트 또는 삭제 될 때까지 행의 잠금이 해제 됩니다. 이 시점에서 행은 다시 읽어서 마지막으로 읽은 이후 변경 되었는지 확인 합니다. 행이 변경 되 면 업데이트 또는 삭제가 실패 하 고 다시 시도해 야 합니다.  
  
 행이 변경 되었는지 여부를 확인 하기 위해 해당 행의 캐시 된 버전에 대해 새 버전을 확인 합니다. 이 확인은 행 버전 (예: SQL Server의 timestamp 열 또는 행의 각 열 값)을 기반으로 할 수 있습니다. 많은 Dbms에서 행 버전을 지원 하지 않습니다.  
  
 데이터 원본 또는 응용 프로그램에서 낙관적 동시성을 구현할 수 있습니다. 두 경우 모두 응용 프로그램은 Read Committed와 같은 낮은 트랜잭션 격리 수준을 사용 해야 합니다. 높은 수준을 사용 하면 낙관적 동시성을 사용 하 여 향상 된 동시성이 무효화 됩니다.  
  
 데이터 원본에서 낙관적 동시성을 구현 하는 경우 응용 프로그램은 SQL_ATTR_CONCURRENCY statement 특성을 SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES로 설정 합니다. 행을 업데이트 하거나 삭제 하려면 비관적 동시성을 사용 하는 것과 마찬가지로 위치 지정 update 또는 delete 문을 실행 하거나 **SQLSetPos** 를 호출 합니다. 충돌 때문에 업데이트나 삭제가 실패 하면 드라이버 또는 데이터 원본에서 SQLSTATE 01001 (커서 작업 충돌)를 반환 합니다.  
  
 응용 프로그램 자체에서 낙관적 동시성을 구현 하는 경우 SQL_ATTR_CONCURRENCY statement 특성을 SQL_CONCUR_READ_ONLY 하 여 행을 읽도록 설정 합니다. 행 버전을 비교 하 고 행 버전 열을 알 수 없는 경우에는 SQL_ROWVER 옵션을 사용 하 여 **SQLSpecialColumns** 를 호출 하 여이 열의 이름을 확인 합니다.  
  
 응용 프로그램은 SQL_CONCUR_LOCK (행에 대 한 쓰기 액세스 권한 얻기) 동시성을 증가 하 고, 응용 프로그램에서 행을 읽을 때 행의 버전 또는 값을 지정 하는 **where** 절을 사용 하 여 **UPDATE** 또는 **DELETE** 문을 실행 하 여 행을 업데이트 하거나 삭제 합니다. 이후에 행이 변경 된 경우에는 문이 실패 합니다. **Where** 절에서 행을 고유 하 게 식별 하지 않는 경우에도 문은 다른 행을 업데이트 하거나 삭제할 수 있습니다. 행 버전은 항상 행을 고유 하 게 식별 하지만 행 값은 기본 키가 포함 된 경우에만 행을 고유 하 게 식별 합니다.
