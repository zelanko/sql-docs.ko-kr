---
title: 낙관적 동시성 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282492"
---
# <a name="optimistic-concurrency"></a>낙관적 동시성
*낙관적 동시성은* 트랜잭션 간의 충돌이 거의 발생하지 않는다는 낙관적 인 가정에서 이름을 파생합니다. 충돌은 다른 트랜잭션이 현재 트랜잭션에서 읽은 시간과 업데이트 또는 삭제된 시간 사이의 데이터 행을 업데이트하거나 삭제할 때 발생했다고 합니다. 응용 프로그램 개발자가 이러한 충돌이 일반적이라고 믿는 *비관적 동시성* 또는 잠금과는 반대입니다.  
  
 낙관적 동시성에서는 행을 업데이트하거나 삭제할 때까지 행이 잠금 해제된 상태로 남아 있습니다. 이 때 행을 다시 읽고 마지막으로 읽은 이후 변경되었는지 확인합니다. 행이 변경된 경우 업데이트 또는 삭제가 실패하고 다시 시도해야 합니다.  
  
 행이 변경되었는지 여부를 확인하려면 새 버전이 캐시된 행 버전에 대해 검사됩니다. 이 검사는 SQL Server의 타임스탬프 열 또는 행의 각 열 값과 같은 행 버전을 기반으로 할 수 있습니다. 대부분의 DBMS는 행 버전을 지원하지 않습니다.  
  
 낙관적 동시성은 데이터 원본 또는 응용 프로그램에서 구현할 수 있습니다. 두 경우 모두 응용 프로그램은 커밋된 읽기와 같은 낮은 트랜잭션 격리 수준을 사용해야 합니다. 더 높은 수준을 사용하면 낙관적 동시성을 사용하여 얻은 증가된 동시성을 무효화합니다.  
  
 데이터 원본에서 낙관적 동시성을 구현하는 경우 응용 프로그램은 SQL_ATTR_CONCURRENCY 명령문 특성을 SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES 설정합니다. 행을 업데이트하거나 삭제하기 위해 포지셔닝된 업데이트를 실행하거나 문을 삭제하거나 비관적 동시성으로 **SQLSetPos를** 호출합니다. 드라이버 또는 데이터 원본은 충돌로 인해 업데이트 또는 삭제가 실패할 경우 SQLSTATE 01001(커서 작업 충돌)을 반환합니다.  
  
 응용 프로그램 자체가 낙관적 동시성을 구현하는 경우 SQL_ATTR_CONCURRENCY 문 특성을 행을 읽을 SQL_CONCUR_READ_ONLY 설정합니다. 행 버전을 비교하고 행 버전 열을 모르는 경우 이 열의 이름을 결정하는 SQL_ROWVER 옵션으로 **SQLSpecialColumns를** 호출합니다.  
  
 응용 프로그램은 SQL_CONCUR_LOCK 동시성을 늘리고(행에 대한 쓰기 액세스 권한을 얻으려면) 응용 프로그램이 열이 읽은 경우 행이 가진 버전이나 값을 지정하는 **WHERE** 절로 **UPDATE** 또는 **DELETE** 문을 실행하여 행을 업데이트하거나 삭제합니다. 그 이후로 행이 변경되면 명령문이 실패합니다. **WHERE** 절이 행을 고유하게 식별하지 않는 경우 문은 다른 행을 업데이트하거나 삭제할 수도 있습니다. 행 버전은 항상 행을 고유하게 식별하지만 행 값은 기본 키가 포함된 경우에만 행을 고유하게 식별합니다.
