---
title: 트랜잭션 격리 수준 설정 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e59db823f8b84edfb5c92f2d142c8238449e3323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107585"
---
# <a name="setting-the-transaction-isolation-level"></a>트랜잭션 격리 수준 설정
트랜잭션 격리 수준을 설정 하려면 응용 프로그램 SQL_ATTR_TXN_ISOLATION 연결 특성을 사용 합니다. 데이터 원본에 요청 된 격리 수준을 지원 하지 않습니다, 경우 드라이버 또는 데이터 원본 더 높은 수준을 설정할 수 있습니다. 지 원하는 어떤 트랜잭션 격리 수준으로 데이터 소스를 확인 하려면 및 기본 격리 수준이 인 응용 프로그램 호출 **SQLGetInfo** 에서 SQL_TXN_ISOLATION_OPTION 및 SQL_DEFAULT_TXN_ISOLATION 옵션을 사용 하 여 각각.  
  
 더 높은 수준의 트랜잭션 격리는 데이터베이스 데이터의 무결성에 대 한 대부분의 보호를 제공합니다. 직렬화 가능 트랜잭션은 다른 트랜잭션에 의해 영향을 받지 않습니다 보장 되며 따라서 데이터베이스 무결성을 유지 하도록 보장 됩니다.  
  
 그러나 더 높은 수준의 트랜잭션 격리 응용 프로그램 잠금을 해제할 데이터에서 대기 하는 가능성 증가 성능이 저하 될 수 있습니다. 응용 프로그램에는 다음과 같은 경우에는 성능 향상을 위해 격리 낮은 수준을 지정할 수 있습니다.:  
  
-   경우 것을 보장할 수 없는 다른 트랜잭션에서 있는지 응용 프로그램의 트랜잭션을 충돌할 수 있습니다. 이 이런 명 소규모 회사에 유지 한 컴퓨터에서 직원 데이터를 포함 하는 dBASE 파일을 관리 하는 경우와 같은 제한 된 상황 에서만에서 발생 하 고 이러한 파일을 공유 하지 않습니다.  
  
-   속도 정확도 및 오류 보다 더 중요 한 경우 작은 일 수 있습니다. 예를 들어 회사 작은 판매 수 있도록 하 고 대규모 매출을 드물게 발생 합니다. 열려 있는 모든 판매액의 합계 값을 추정 하는 트랜잭션이 Read Uncommitted 격리 수준 안전 하 게 사용할 수 있습니다. 트랜잭션이 열리거나 닫힐 되며 이후에 순서 대로 포함 하지만이 일반적으로 서로 위배 롤백되고 한다는 이러한 주문을 발견 될 때마다 차단 되지 않은 트랜잭션이 훨씬 속도가 더 빠를 수는 합니다.  
  
 자세한 내용은 [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)합니다.
