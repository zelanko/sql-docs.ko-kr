---
title: "낙관적 동시성 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- optimistic concurrency [ODBC]
ms.assetid: 9d71e09e-bc68-4c1f-9229-ed2a7be7d324
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3ae017de17892595dac94a0dd4bbb843d6d5f658
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="optimistic-concurrency"></a>낙관적 동시성
*낙관적 동시성* 이라는 낙관적 가정에서 이름을 파생 트랜잭션 간의 충돌 됩니다는 거의 발생 하지 않으면 충돌이 발생 한 다른 트랜잭션의 업데이트 또는 읽기 시간 사이 데이터의 행을 삭제 하는 경우를 라고 합니다. 시간과 현재 트랜잭션에 의해 업데이트 또는 삭제 됩니다. 반대 되 *비관적 동시성* 잠금, 또는에 응용 프로그램 개발자가 이러한 충돌은 일반적입니다.  
  
 낙관적 동시성의 행은 제외는 시점이를 업데이트 하거나 삭제할 때까지 잠금을 해제 합니다. 이 시점에서 행을 다시 읽고 이며 검사 하는 경우 변경 된 마지막으로 읽은 후 확인 됩니다. 행 변경 된 업데이트 또는 삭제 실패 하 고 다시 시도해 야 하는 경우 합니다.  
  
 행 변경 되었는지 여부를 확인 하려면 해당 새 버전은 행의 캐시 된 버전에 대해 확인 됩니다. 이 검사 기반 SQL Server 또는 행의 각 열 값의 타임 스탬프 열과 같은 행 버전입니다. 여러 Dbms 행 버전을 지원 하지 않습니다.  
  
 낙관적 동시성은 데이터 원본이 나 응용 프로그램으로 구현할 수 있습니다. 두 경우 모두 응용 프로그램 Read Committed; 같은 낮은 트랜잭션 격리 수준을 사용 해야 상위 수준을 사용 하 여 낙관적 동시성을 사용 하 여 얻은 동시성 향상된을 부정 합니다.  
  
 낙관적 동시성은 데이터 원본에 의해 구현 되는 경우 응용 프로그램 SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES 문 특성 SQL_ATTR_CONCURRENCY를 설정 합니다. 위치 지정된 update 또는 delete 문이나 호출 실행을 업데이트 하거나 행을 삭제 하려면 **SQLSetPos** 비관적 동시성; 된 것 처럼 드라이버 또는 데이터 원본의 경우 SQLSTATE 01001 (커서 작업 충돌)을 반환 하는 update 또는 delete 충돌로 인해 실패합니다.  
  
 응용 프로그램 자체에서 낙관적 동시성을 구현 하는 경우 문 특성 SQL_ATTR_CONCURRENCY를 SQL_CONCUR_READ_ONLY 행을 읽을 수 설정 합니다. 행 버전을 비교 합니다 및 행 버전 열을 알 수 없습니다, 호출 **SQLSpecialColumns** 이 열의 이름을 확인 하려면 SQL_ROWVER 옵션을 사용 합니다.  
  
 응용 프로그램을 업데이트 하거나 SQL_CONCUR_LOCK (행에 대 한 쓰기 권한을) 및 실행 하는 동시성을 증가 시켜 행을 삭제 하는 **업데이트** 또는 **삭제** 문을 **위치 ** 응용 프로그램에서 읽을 때 행 값 또는 버전을 지정 하는 절을 포함 했습니다. 그 이후에 변경 행이 문이 실패 합니다. 경우는 **여기서** 절 행을 고유 하 게 식별 하지 않습니다도 문이 업데이트나 다른 행을 삭제할 수 있습니다; 행 버전은 항상 고유 하 게 행을 식별 하지만 기본 키를 포함 하는 경우에 행 값 행을 고유 하 게 식별 합니다.

