---
title: SQL 서버 네이티브 클라이언트 | 마이크로 소프트 문서
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
ms.openlocfilehash: 30ef404501c498fca2c722e9eb88bb13997a17b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305041"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC 또는 SQL Server 네이티브 클라이언트는 SQL Server용 ODBC 및 OLE DB 드라이버를 참조하기 위해 상호 교환적으로 사용되는 용어입니다.

> [!IMPORTANT] 
> SQLNCLI(SQLNCLI)는 더 이상 사용되지 않으며 새 개발 작업에는 사용하지 않는 것이 좋습니다. 대신 최신 서버 기능으로 업데이트되는 새로운 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md)(MSOLEDBSQL)를 사용하세요.

> [!NOTE]
> 자세한 내용은 SNAC 또는 ODBC 드라이버를 다운로드하려면 [SNAC 수명 주기 설명 블로그 게시물을](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)참조하십시오.
> SQL Server용 ODBC 드라이버에 대한 자세한 내용은 [SQL Server용 Microsoft ODBC 드라이버를](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)참조하십시오.  

 에서 해제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 된 네이티브 클라이언트 기능에 대 한 정보 입니다. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]

-   [LocalDB에 대한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0의 UTF-16 지원](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [확장 이벤트 로그에서 진단 정보에 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

네이티브 클라이언트의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC는 Windows 7 SDK의 표준 ODBC에 추가된 세 가지 기능을 지원합니다.  

-   연결 관련 작업에 대한 비동기 실행. 자세한 내용은 [비동기 실행](https://go.microsoft.com/fwlink/?LinkID=191493)을 참조하십시오.  

-   C 데이터 형식 확장성. 자세한 내용은 [ODBC의 C 데이터 유형을](https://go.microsoft.com/fwlink/?LinkID=191495)참조하십시오.  

     네이티브 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 클라이언트에서 이 기능을 지원하기 위해 SQLGetDescField는 응용 프로그램에서 ODBC 3.8을 사용하는 경우 **SQL_C_BINARY**대신 **SQL_C_SS_TIME2(시간** 형식) 또는 **time** **SQL_C_SS_TIMESTAMPOFFSET(날짜** **오프셋의**경우)를 반환할 수 있습니다. 자세한 내용은 [ODBC 날짜 및 시간 개선에 대한 데이터 형식 지원을](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)참조하십시오.  

-   큰 매개 변수 값을 검색하려면 작은 버퍼로 **SQLGetData를** 여러 번 호출합니다. 자세한 내용은 [SQLGetData를 사용하여 출력 매개 변수 검색을](https://go.microsoft.com/fwlink/?LinkID=191494)참조하십시오.  

 다음 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 동작 변경에 대해 설명합니다.  

-   **ICommandWithParameters::SetParameterInfo를**호출할 때 *pwszName* 매개 변수에 전달 된 값은 유효한 식별자 여야 합니다. 자세한 내용은 [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)을 참조하십시오.  

-   **SQLDescribeParam은** 값을 준수하는 ODBC 사양을 일관되게 반환합니다. 자세한 내용은 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)을 참조하십시오.  

-   [문자 변환을 처리 시 ODBC 드라이버 동작 변경](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>참조  
[SQL 서버 네이티브 클라이언트 설치](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 기능](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
