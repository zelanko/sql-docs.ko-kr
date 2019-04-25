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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa80ff3359e3bbbed9e28044cce7514006c40f10
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446215"
---
# <a name="optimistic-concurrency"></a>낙관적 동시성
*낙관적 동시성* 이라는 낙관적 가정에서 이름을 파생는 트랜잭션 간 충돌이 거의 발생; 충돌을 다른 트랜잭션이 업데이트 하거나 읽기 시간 사이 데이터의 행을 삭제 하는 경우 발생 라고 합니다. 현재 트랜잭션 시간을 업데이트 또는 삭제 됩니다. 반대입니다 *비관적 동시성* 잠금 또는 응용 프로그램 개발자가 이러한 충돌은 일반화는에 있습니다.  
  
 낙관적 동시성을 행 그대로 시점이 업데이트 또는 삭제 될 때까지 잠금을 해제 합니다. 이 시점에서 행을 다시 읽고 이며를 검사 하는 경우 변경 된 마지막으로 읽은 후 확인 됩니다. 행 변경 된 업데이트 또는 삭제 실패 하 고 다시 시도해 야 합니다.  
  
 행 변경 되었는지 여부를 확인 하려면 해당 새 버전은 행의 캐시 된 버전에 대해 확인 됩니다. 이 검사는 행 버전에서 SQL Server 또는 행의 각 열 값을 타임 스탬프 열과 같이 기반 할 수 있습니다. 여러 Dbms 행 버전을 지원 하지 않습니다.  
  
 데이터 원본이 나 응용 프로그램에서 낙관적 동시성을 구현할 수 있습니다. 두 경우 모두 응용 프로그램을 사용할지 낮은 트랜잭션 격리 수준을 Read Committed; 등 더 높은 수준을 사용 하 여 낙관적 동시성을 사용 하 여 얻은 동시성 향상된을 부정 합니다.  
  
 데이터 원본에서 낙관적 동시성 구현 된 경우 응용 프로그램 SQL_CONCUR_ROWVER 또는 SQL_CONCUR_VALUES 문 특성 SQL_ATTR_CONCURRENCY를 설정 합니다. 위치 지정된 update 또는 delete 문을 호출 실행을 업데이트 하거나 행을 삭제 하려면 **SQLSetPos** 비관적 동시성;를 사용 하 여 것 처럼에서 드라이버 또는 데이터 원본 경우 SQLSTATE 01001 (커서 작업이 충돌)을 반환 하는 합니다 update 또는 delete 충돌로 인해 실패합니다.  
  
 응용 프로그램 자체에서 낙관적 동시성을 구현 하는 경우 행을 읽는 SQL_CONCUR_READ_ONLY에 문 특성 SQL_ATTR_CONCURRENCY를 설정 합니다. 에서는 행 버전을 비교 하 고 행 버전 열을 알 수 없습니다, 하는 경우 호출 **SQLSpecialColumns** 이 열의 이름을 확인 하는 SQL_ROWVER 옵션을 사용 하 여 합니다.  
  
 응용 프로그램 업데이트 또는 SQL_CONCUR_LOCK (행에 대 한 쓰기 액세스 권한을) 하 고 실행 하는 동시성을 증가 시켜 행을 삭제 하는 **업데이트** 또는 **삭제** 사용 하 여 문을 **위치**  응용 프로그램에서 읽을 때 행 값 또는 버전을 지정 하는 절 했습니다. 그 후 변경 행이 문이 실패 합니다. 경우는 **여기서** 절 행을 고유 하 게 식별 하지 않습니다, 문이 될 수 있습니다도 업데이트 하거나 다른 행을 삭제할 행 버전은 항상 고유 하 게 행을 식별 하지만 기본 키를 포함 하는 경우에 행 값 행을 고유 하 게 식별 합니다.
