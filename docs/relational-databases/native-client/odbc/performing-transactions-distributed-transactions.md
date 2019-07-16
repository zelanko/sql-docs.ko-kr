---
title: 분산된 트랜잭션을 만들 | Microsoft Docs
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fc61ad955be287faad20289245ca4520efcd4bbd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913171"
---
# <a name="create-a-distributed-transaction"></a>분산된 트랜잭션을 만들려면

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->

[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

다른 방법으로 다른 Microsoft SQL 시스템에 대 한 분산된 트랜잭션을 만들 수 있습니다.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>SQL Server 온-프레미스에 대 한 MSDTC를 호출 하는 ODBC 드라이버

MSDTC Microsoft Distributed Transaction Coordinator () 사용 하면 응용 프로그램 확장 또는 _배포할_ 의 두 개 이상의 인스턴스에서 트랜잭션을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다. 분산된 트랜잭션의 두 인스턴스가 서로 다른 컴퓨터에서 호스팅되는 경우에 작동 합니다.

MSDTC는 Microsoft SQL Server 온-프레미스에 설치 되어 있지만 Microsoft의 Azure SQL Database 클라우드 서비스에 사용할 수 없습니다.

MSDTC 라고 SQL Server Native Client 드라이버에서 Open Database Connectivity (ODBC)에 대 한 경우에 C++ 프로그램에서 분산된 트랜잭션을 관리 합니다. Native Client ODBC 드라이버에는 트랜잭션 관리자와는 열린 그룹 분산 트랜잭션 처리 (DTP) XA 표준을 준수 합니다. MSDTC에 의해이 규정 준수 필요 합니다. 일반적으로 모든 트랜잭션 관리 명령은이 Native Client ODBC 드라이버를 통해 전송 됩니다. 시퀀스는 다음과 같습니다.

1. 에 C++ Native Client ODBC 응용 프로그램 호출 하 여 트랜잭션을 시작 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)는 자동 커밋 모드를 해제 합니다.

2. 1\. 컴퓨터에서 SQL Server X에서 일부 데이터를 업데이트 하는 응용 프로그램

3. 컴퓨터 B에서 y SQL 서버의 일부 데이터를 업데이트 하는 응용 프로그램
    - SQL Server Y에 대 한 업데이트에 실패 하면 두 SQL Server 인스턴스에서 커밋되지 않은 모든 업데이트 내용이 롤백됩니다.

4. 마지막으로 호출 하 여 트랜잭션을 종료를 응용 프로그램 [SQLEndTran _(1)_ ](../../../relational-databases/native-client-odbc-api/sqlendtran.md)을 SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용 하 여 합니다.

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

_(1)_  MSDTC ODBC 않고 호출할 수 있습니다. 이러한 경우 MSDTC가 트랜잭션 관리자 및 응용 프로그램이 더 이상 사용 하지 **SQLEndTran**합니다.

### <a name="only-one-distributed-transaction"></a>하나의 분산된 트랜잭션

된다고 가정 하면 C++ Native Client ODBC 응용 프로그램은 분산 트랜잭션에 인 리스트 먼 트 합니다. 그런 다음 응용 프로그램을 두 번째 분산된 트랜잭션에 참여합니다. 이 경우에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 원래 분산된 트랜잭션에 연결을 떠나고 새로운 분산된 트랜잭션에 참여 합니다.

자세한 내용은 [DTC 프로그래머 참조](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>C#클라우드에서 SQL Database에 대 한 대안

MSDTC는 Azure SQL Database 또는 Azure SQL Data Warehouse에 대 한 지원 되지 않습니다.

그러나 분산된 트랜잭션을 만들 수 있습니다 SQL Database에 대 한 함으로써 사용자 C# .NET 클래스를 사용 하 여 프로그램 [System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope)합니다.

### <a name="other-programming-languages"></a>다른 프로그래밍 언어

다음 다른 프로그래밍 언어 SQL Database 서비스를 사용 하 여 분산된 트랜잭션에 대 한 어떤 지원도 제공 하지 않을 수 있습니다.

- 네이티브 C++ ODBC 드라이버를 사용 하는
- TRANSACT-SQL을 사용 하 여 연결 된 서버
- JDBC 드라이버

## <a name="see-also"></a>참조

[트랜잭션 수행(ODBC)](performing-transactions-in-odbc.md)
