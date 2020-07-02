---
title: 정보
description: SQL Server Native Client (SNAC)의 기능에 대해 알아봅니다. SQL Server Native Client는 SQL Server에 대 한 ODBC 및 OLE DB 드라이버를 나타냅니다.
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 829b6dccd12edaa707a2aad2d0861c75e99c408e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787589"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

SNAC 또는 SQL Server Native Client는 SQL Server에 대 한 ODBC 및 OLE DB 드라이버를 참조 하는 데 사용 되는 용어입니다.

> [!IMPORTANT] 
> SQL Server Native Client (SQLNCLI)는 더 이상 사용 되지 않으며 새로운 개발 작업에 사용 하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.

> [!NOTE]
> SNAC 또는 ODBC 드라이버를 다운로드 하 고 다운로드 하는 방법에 대 한 자세한 내용은 [SNAC 수명 주기 설명 블로그 게시물](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)을 참조 하세요.
> SQL Server에 대 한 ODBC 드라이버에 대 한 자세한 내용은 [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)을 참조 하십시오.  

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]최신 버전의 SQL Server Native client와 함께 출시 된 Native client 기능에 대 한 정보 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 를 제공 합니다.

-   [LocalDB에 대한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0의 UTF-16 지원](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [확장 이벤트 로그의 진단 정보 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

Native Client의 ODBC는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 7 SDK의 표준 odbc에 추가 된 세 가지 기능을 지원 합니다.  

-   연결 관련 작업에 대한 비동기 실행. 자세한 내용은 [비동기 실행](https://go.microsoft.com/fwlink/?LinkID=191493)을 참조 하세요.  

-   C 데이터 형식 확장성. 자세한 내용은 [ODBC의 C 데이터 형식](https://go.microsoft.com/fwlink/?LinkID=191495)을 참조 하세요.  

     Native Client에서이 기능을 지원 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLGetDescField는 응용 프로그램에서 ODBC 3.8를 사용 하는 경우 **SQL_C_BINARY**대신 **SQL_C_SS_TIME2** ( **시간** 형식) 또는 **SQL_C_SS_TIMESTAMPOFFSET** ( **datetimeoffset**)를 반환할 수 있습니다. 자세한 내용은 [ODBC 날짜 및 시간 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)을 참조 하세요.  

-   작은 버퍼로 **SQLGetData** 를 여러 번 호출 하 여 많은 매개 변수 값을 검색 합니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](https://go.microsoft.com/fwlink/?LinkID=191494)을 참조 하세요.  

 다음 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 동작 변경에 대해 설명합니다.  

-   **ICommandWithParameters:: SetParameterInfo**를 호출 하는 경우 *pwszName* 매개 변수에 전달 된 값은 올바른 식별자 여야 합니다. 자세한 내용은 [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)를 참조 하세요.  

-   **SQLDescribeParam** 는 ODBC 사양에 맞는 값을 일관 되 게 반환 합니다. 자세한 내용은 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)를 참조 하세요.  

-   [문자 변환을 처리 시 ODBC 드라이버 동작 변경](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>참고 항목  
[SQL Server Native Client 설치](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 기능](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
