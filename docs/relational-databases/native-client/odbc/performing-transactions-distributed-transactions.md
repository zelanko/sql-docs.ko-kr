---
title: 분산 트랜잭션 만들기 | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f21ea9b7146b2907a09688f5189d6d9ae4f3f26a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303707"
---
# <a name="create-a-distributed-transaction"></a>분산 트랜잭션 만들기

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


다른 방법으로 다른 Microsoft SQL 시스템에 대 한 분산 트랜잭션을 만들 수 있습니다.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 드라이버가 SQL Server 온-프레미스에 대 한 MSDTC를 호출 합니다.

MSDTC (Microsoft DTC(Distributed Transaction Coordinator))를 사용 하면 응용 프로그램에서 둘 이상의 인스턴스에서 트랜잭션을 확장 하거나 _배포할_ 수 있습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 분산 트랜잭션은 두 인스턴스가 별도의 컴퓨터에서 호스팅되는 경우에도 작동 합니다.

MSDTC는 Microsoft SQL Server 온-프레미스에 대해 설치 되지만 Microsoft Azure SQL Database 클라우드 서비스에는 사용할 수 없습니다.

MSDTC는 c + + 프로그램에서 분산 트랜잭션을 관리할 때 ODBC (Open Database Connectivity) 용 SQL Server Native Client 드라이버에 의해 호출 됩니다. Native Client ODBC 드라이버에는 Open DTP (Distributed Transaction Processing) XA 표준과 호환 되는 트랜잭션 관리자가 있습니다. 이 준수는 MSDTC에 필요 합니다. 일반적으로 모든 트랜잭션 관리 명령은이 Native Client ODBC 드라이버를 통해 전송 됩니다. 순서는 다음과 같습니다.

1. C + + Native Client ODBC 응용 프로그램은 자동 커밋 모드가 해제 된 상태에서 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)를 호출 하 여 트랜잭션을 시작 합니다.

2. 응용 프로그램은 A 컴퓨터의 SQL Server X에서 일부 데이터를 업데이트 합니다.

3. 응용 프로그램은 컴퓨터 B의 SQL Server Y에서 일부 데이터를 업데이트 합니다.
    - SQL Server Y에 대 한 업데이트가 실패 하는 경우 두 SQL Server 인스턴스의 커밋되지 않은 모든 업데이트가 롤백됩니다.

4. 마지막으로 응용 프로그램은 SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용 하 여 [Sqlendtran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md)을 호출 하 여 트랜잭션을 종료 합니다.

_(1)_ ODBC 없이 MSDTC를 호출할 수 있습니다. 이 경우 MSDTC는 트랜잭션 관리자가 되며 응용 프로그램은 더 이상 **Sqlendtran**을 사용 하지 않습니다.

### <a name="only-one-distributed-transaction"></a>하나의 분산 트랜잭션만

C + + Native Client ODBC 응용 프로그램이 분산 트랜잭션에 참여 한다고 가정 합니다. 그런 다음 응용 프로그램은 두 번째 분산 트랜잭션에 참여 합니다. 이 경우 Native Client ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 드라이버는 원래 분산 트랜잭션을 떠나 새 분산 트랜잭션에 참여 시킵니다.

자세한 내용은 [DTC 프로그래머 참조](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))를 참조 하세요.

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>클라우드의 SQL Database에 대 한 c # 대안

MSDTC는 Azure SQL Database 또는 Azure SQL Data Warehouse에 대해 지원 되지 않습니다.

그러나 c # 프로그램에서 .NET 클래스 [system.object](/dotnet/api/system.transactions.transactionscope)를 사용 하도록 하 여 SQL Database에 대 한 분산 트랜잭션을 만들 수 있습니다.

### <a name="other-programming-languages"></a>기타 프로그래밍 언어

다음과 같은 다른 프로그래밍 언어는 SQL Database 서비스를 사용 하 여 분산 트랜잭션에 대 한 지원을 제공 하지 않을 수 있습니다.

- ODBC 드라이버를 사용 하는 네이티브 c + +
- Transact-sql을 사용 하는 연결 된 서버
- JDBC 드라이버

## <a name="see-also"></a>참고 항목

[트랜잭션 수행(ODBC)](performing-transactions-in-odbc.md)
