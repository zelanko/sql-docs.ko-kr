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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107585"
---
# <a name="setting-the-transaction-isolation-level"></a>트랜잭션 격리 수준 설정
응용 프로그램은 트랜잭션 격리 수준을 설정 하기 위해 SQL_ATTR_TXN_ISOLATION 연결 특성을 사용 합니다. 데이터 원본에서 요청 된 격리 수준을 지원 하지 않는 경우 드라이버 또는 데이터 원본에서 더 높은 수준을 설정할 수 있습니다. 데이터 원본에서 지 원하는 트랜잭션 격리 수준과 기본 격리 수준을 확인 하기 위해 응용 프로그램은 각각 SQL_TXN_ISOLATION_OPTION 및 SQL_DEFAULT_TXN_ISOLATION 옵션으로 **SQLGetInfo** 를 호출 합니다.  
  
 높은 수준의 트랜잭션 격리는 데이터베이스 데이터의 무결성을 위한 가장 강력한 보호를 제공 합니다. 직렬화 가능 트랜잭션은 다른 트랜잭션의 영향을 받지 않으므로 데이터베이스 무결성을 유지 하기 위해 보장 됩니다.  
  
 그러나 더 높은 수준의 트랜잭션 격리는 응용 프로그램이 해제할 데이터에 대 한 잠금을 대기 해야 하는 가능성을 증가 시킬 수 있기 때문에 성능이 저하 될 수 있습니다. 응용 프로그램은 다음과 같은 경우 성능을 향상 시키기 위해 낮은 격리 수준을 지정할 수 있습니다.  
  
-   응용 프로그램의 트랜잭션을 방해할 수 있는 다른 트랜잭션이 존재 하지 않도록 보장할 수 있습니다. 이 상황은 소규모 회사의 한 사람이 한 컴퓨터의 직원 데이터를 포함 하는 dBASE 파일을 유지 관리 하 고 이러한 파일을 공유 하지 않는 경우와 같이 제한 된 상황 에서만 발생 합니다.  
  
-   속도가 정확도 보다 중요 하 고 오류가 적을 가능성이 높습니다. 예를 들어 회사가 작은 판매액을 많이 사용 하 고 있는 경우에는 대량 판매량이 드물게 발생 한다고 가정 합니다. 모든 오픈 판매의 합계 값을 예측 하는 트랜잭션은 커밋되지 않은 읽기 격리 수준을 안전 하 게 사용할 수 있습니다. 트랜잭션는 열려 있거나 닫혀 있는 주문을 포함 하지만 이후에 롤백되는 경우에는 일반적으로 서로를 취소 하 고 이러한 주문을 발견할 때마다 차단 되지 않으므로 트랜잭션은 훨씬 더 빠릅니다.  
  
 자세한 내용은 [낙관적 동시성](../../../odbc/reference/develop-app/optimistic-concurrency.md)을 참조 하세요.
