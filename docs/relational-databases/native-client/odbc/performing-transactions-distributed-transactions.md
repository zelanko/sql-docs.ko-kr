---
title: 분산 트랜잭션 만들기 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303707"
---
# <a name="create-a-distributed-transaction"></a>분산 트랜잭션 만들기

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


분산 트랜잭션은 다른 방법으로 다른 Microsoft SQL 시스템에 대해 만들 수 있습니다.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>ODBC 드라이버는 SQL Server 온-프레미스에 대해 MSDTC를 호출합니다.

MSDTC(Microsoft 분산 트랜잭션 코디네이터)를 사용하면 응용 프로그램이 두 개 이상의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]인스턴스에서 트랜잭션을 확장하거나 _배포할_ 수 있습니다. 분산 트랜잭션은 두 인스턴스가 별도의 컴퓨터에서 호스팅되는 경우에도 작동합니다.

MSDTC는 Microsoft SQL Server 온-프레미스에 설치되지만 Microsoft의 Azure SQL Database 클라우드 서비스에는 사용할 수 없습니다.

MSDTC는 C++ 프로그램이 분산 트랜잭션을 관리할 때 개방형 데이터베이스 연결(ODBC)에 대한 SQL Server 네이티브 클라이언트 드라이버에서 호출합니다. 네이티브 클라이언트 ODBC 드라이버에는 DTP(개방형 그룹 분산 트랜잭션 처리) XA 표준을 준수하는 트랜잭션 관리자가 있습니다. 이 규정 준수는 MSDTC에서 요구합니다. 일반적으로 모든 트랜잭션 관리 명령은 이 네이티브 클라이언트 ODBC 드라이버를 통해 전송됩니다. 순서는 다음과 같습니다.

1. C++ 네이티브 클라이언트 ODBC 응용 프로그램은 자동 커밋 모드가 꺼진 [SQLSetConnectAttr을](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)호출하여 트랜잭션을 시작합니다.

2. 응용 프로그램은 컴퓨터 A의 SQL Server X의 일부 데이터를 업데이트합니다.

3. 응용 프로그램은 컴퓨터 B의 SQL Server Y의 일부 데이터를 업데이트합니다.
    - SQL Server Y에 대한 업데이트가 실패하면 두 SQL Server 인스턴스에서 커밋되지 않은 모든 업데이트가 롤백됩니다.

4. 마지막으로 응용 프로그램은 SQL_COMMIT 또는 SQL_ROLLBACK 옵션을 사용 하 여 [SQLEndTran _(1)를_](../../../relational-databases/native-client-odbc-api/sqlendtran.md)호출 하 여 트랜잭션을 종료 합니다.

_(1)_ MSDTC는 ODBC없이 호출 할 수 있습니다. 이러한 경우 MSDTC는 트랜잭션 관리자가 되며 응용 프로그램은 더 이상 **SQLEndTran**을 사용하지 않습니다.

### <a name="only-one-distributed-transaction"></a>하나의 분산 트랜잭션만

C++ 네이티브 클라이언트 ODBC 응용 프로그램이 분산 트랜잭션에 등록되어 있다고 가정합니다. 다음으로 응용 프로그램은 두 번째 분산 트랜잭션에 참여합니다. 이 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 네이티브 클라이언트 ODBC 드라이버는 원래 분산 트랜잭션을 떠나 새 분산 트랜잭션에 참여합니다.

자세한 내용은 [DTC 프로그래머 의 참조](https://docs.microsoft.com/previous-versions/windows/desktop/ms686108\(v=vs.85\))를 참조하십시오.

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>클라우드의 SQL 데이터베이스에 대한 C# 대안

MSDTC는 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스에 대해 지원되지 않습니다.

그러나 C# 프로그램이 .NET 클래스 [System.Transactions.TransactionScope](/dotnet/api/system.transactions.transactionscope)를 사용하도록 하여 SQL Database에 분산 트랜잭션을 만들 수 있습니다.

### <a name="other-programming-languages"></a>기타 프로그래밍 언어

다음 다른 프로그래밍 언어는 SQL Database 서비스를 사용하여 분산 트랜잭션을 지원하지 않을 수 있습니다.

- ODBC 드라이버를 사용하는 기본 C++
- 거래-SQL을 사용하여 연결된 서버
- JDBC 드라이버

## <a name="see-also"></a>참조

[트랜잭션 수행(ODBC)](performing-transactions-in-odbc.md)
