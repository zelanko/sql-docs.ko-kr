---
title: ODBC의 트랜잭션 | Microsoft Docs
description: ODBC는 연결 수준에서 트랜잭션을 관리 하 고 완료 된 모든 작업을 커밋 또는 롤백합니다. 자동 커밋 또는 수동 커밋 모드에서 수행 됩니다.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, transactions
- transactions [ODBC]
- ODBC, transactions
ms.assetid: c5a87fa5-827a-4e6f-a0d9-924bac881eb0
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 071146a14be3dbeff057845f0458de422617430f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483114"
---
# <a name="performing-transactions-in-odbc"></a>ODBC에서 트랜잭션 수행
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  ODBC의 트랜잭션은 연결 수준에서 관리됩니다. 애플리케이션에서는 트랜잭션이 완료되면 해당 연결에서 모든 문 핸들을 통해 완료한 모든 작업을 커밋하거나 롤백합니다. 애플리케이션에서는 트랜잭션을 커밋하거나 롤백할 때 COMMIT 또는 ROLLBACK 문을 전송하는 대신 [SQLEndTran](../../../relational-databases/native-client-odbc-api/sqlendtran.md) 을 호출해야 합니다.  
  
 애플리케이션에서는 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) 을 호출하여 다음과 같은 두 가지 트랜잭션 관리 ODBC 모드 사이를 전환할 수 있습니다.  
  
-   자동 커밋 모드  
  
     성공적으로 완료된 각 문이 자동으로 커밋됩니다. 응용 프로그램을 자동 커밋 모드에서 실행하면 다른 트랜잭션 관리 기능이 필요하지 않습니다.  
  
-   수동 커밋 모드  
  
     **SQLEndTran** 을 호출하여 중지하기 전까지는 실행된 모든 문이 동일한 트랜잭션에 포함됩니다.  
  
 자동 커밋 모드는 ODBC의 기본 트랜잭션 모드입니다. 연결을 설정하면 **SQLSetConnectAttr** 호출을 통해 자동 커밋 모드를 해제하고 수동 커밋 모드로 전환하기 전까지 자동 커밋 모드가 사용됩니다. 애플리케이션에서 자동 커밋을 해제하면 데이터베이스에 보내는 다음 문부터 트랜잭션이 시작되고, 이 트랜잭션은 애플리케이션에서 SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용하여 **SQLEndTran** 을 호출하기 전까지 유효한 상태로 유지됩니다. **SQLEndTran** 을 호출한 이후에 데이터베이스에 보내는 명령부터 다음 트랜잭션이 시작됩니다.  
  
 애플리케이션에서 수동 커밋 모드에서 자동 커밋 모드로 전환하면 드라이버에서는 연결에 현재 열려 있는 모든 트랜잭션을 커밋합니다.  
  
 BEGIN TRANSACTION, COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION 같은 Transact-SQL 트랜잭션 문을 사용하면 드라이버에서 예기치 않은 동작이 발생할 수 있으므로 ODBC 애플리케이션에서는 이러한 문을 사용하지 않는 것이 좋습니다. ODBC 애플리케이션은 자동 커밋 모드로 실행하면서 다른 트랜잭션 관리 함수나 문을 실행하지 않거나, 수동 커밋 모드로 실행하면서 ODBC **SQLEndTran** 함수를 사용하여 트랜잭션을 커밋하거나 롤백해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [ODBC&#41;&#40;트랜잭션 수행 ]()  
  
