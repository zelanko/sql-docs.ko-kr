---
title: 트랜잭션 ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], about transactions
- transactions [ODBC]
ms.assetid: b4ca861a-c164-4e87-8672-d5de15e3823c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6ce5decd2744c0ce9d753e355321a40d00fd620
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840661"
---
# <a name="transactions-odbc"></a>트랜잭션 ODBC
A *트랜잭션* 작업 단위는;은 단일 원자성 작업으로 수행 하는 작업의 성공 또는 전체가 실패, 합니다. 예를 들어 은행 계좌에서 간에 자금을 이체 하는 것이 좋습니다. 이 두 단계로 이루어집니다: 첫 번째 계정에서 돈을 출금 및 두 번째에서 작업입니다. 두 단계가 모두 성공; 반드시 1 단계 성공 및 실패에 대 한 허용 되지 않습니다. 트랜잭션을 지 원하는 데이터베이스는이 보장할 수 있습니다.  
  
 트랜잭션이 있는 것으로 완료할 수 있습니다 *커밋된* 되거나 *롤백*합니다. 트랜잭션이 커밋되면, 트랜잭션 내용이 영구적으로 반영 하는 지정 하 여 변경 합니다. 트랜잭션이 롤백되면 영향을 받는 행 전의에서 트랜잭션이 시작 된 상태로 반환 됩니다. 계정 전송 예제를 확장 하려면 응용 프로그램 하나 SQL 문을 첫 번째 계좌에서 금액 및 두 번째 계정 크레딧 다른 SQL 문을 실행 합니다. 두 문은 모두 성공 하면 응용 프로그램을 한 다음 트랜잭션을 커밋합니다. 하지만 어떤 이유로 든 실패 하면 두 문을 응용 프로그램의 트랜잭션을 롤백합니다. 두 경우 모두 응용 프로그램 트랜잭션이 끝날 때 일관 된 상태를 보장합니다.  
  
 단일 트랜잭션으로 다른 시간에 발생 하는 여러 데이터베이스 작업에 포함 될 수 있습니다. 다른 트랜잭션의 중간 결과에 액세스할 수 있으면 트랜잭션이 서로 방해 합니다. 예를 들어, 행을 삽입 하는 하나의 트랜잭션으로, 가정 두 번째 트랜잭션이 해당 행과 첫 번째 트랜잭션이 롤백되면 읽습니다. 이제 두 번째 트랜잭션이 존재 하지 않는 행에 대 한 데이터에 있습니다.  
  
 이 문제를 해결 하기 위해 다양 한 스키마에서 다른 하나는 트랜잭션 격리 있습니다. *트랜잭션 격리* 일반적으로 구현 됩니다 잠금 행에서 동일한 행을 사용 하 여 동시에 둘 이상의 트랜잭션이 갖습니다. 일부 데이터베이스에서는 행 잠금는 다른 행 잠글 수도 있습니다.  
  
 트랜잭션 격리는 감소 *동시성* 또는 동시에 동일한 데이터를 사용 하는 두 개의 트랜잭션이의 기능입니다. 자세한 내용은 [설정 Transaction Isolation Level](../../../odbc/reference/develop-app/setting-the-transaction-isolation-level.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC의 트랜잭션](../../../odbc/reference/develop-app/transactions-in-odbc-odbc.md)  
  
-   [트랜잭션 격리](../../../odbc/reference/develop-app/transaction-isolation.md)  
  
-   [동시성 제어](../../../odbc/reference/develop-app/concurrency-control.md)
