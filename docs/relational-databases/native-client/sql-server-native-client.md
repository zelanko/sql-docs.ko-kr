---
title: SQL Server Native Client | Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 1df5ea03a73a3c4836c1b011dab0a101d80a749b
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39535443"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client 
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

SNAC, 또는 SQL Server Native Client ODBC 및 OLE DB 드라이버 SQL Server에 대 한 참조를 같은 의미로 사용 된 용어입니다.

**참고:** 새로운 개발에 대 한이 드라이버를 사용 하는 것은 권장 되지 않습니다. 새 OLE DB 공급자가 호출 된 [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) 앞으로 최신 서버 기능을 사용 하 여 업데이트 됩니다.


**자세한 내용은 및 SNAC 또는 ODBC 드라이버를 다운로드 하려면 방문 [SNAC 수명 주기를 설명](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)합니다.**

SQL Server 용 ODBC 드라이버에 자세한 내용은 참조 [Windows의 SQL Server 용 Microsoft ODBC Driver](https://msdn.microsoft.com/library/jj730314(v=sql.110).aspx)합니다.  도 참조 하세요 [새로운 Microsoft ODBC Driver for SQL Server 소개](https://blogs.msdn.microsoft.com/sqlnativeclient/2013/01/23/introducing-the-new-microsoft-odbc-drivers-for-sql-server/), 및 [ODBC Driver 13.1 for SQL Server 출시](https://blogs.technet.microsoft.com/dataplatforminsider/2016/08/03/odbc-driver-13-1-for-sql-server-released/)합니다.  

 에 대 한 정보를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 기능와 함께 릴리스된 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], 마지막 사용 가능한 버전의 SQL Server native Client:

-   [LocalDB에 대한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [메타데이터 검색](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0의 UTF-16 지원](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [확장 이벤트 로그의 진단 정보 액세스](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

ODBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 Windows 7 SDK에 대 한 표준 ODBC에 추가 된 세 가지 기능을 지원 합니다.  

-   연결 관련 작업에 대한 비동기 실행. 자세한 내용은 [비동기 실행](http://go.microsoft.com/fwlink/?LinkID=191493)합니다.  

-   C 데이터 형식 확장성. 자세한 내용은 [odbc에서 C 데이터 형식](http://go.microsoft.com/fwlink/?LinkID=191495)합니다.  

     이 기능을 지원 하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client SQLGetDescField 반환할 수 있습니다 **SQL_C_SS_TIME2** (에 대 한 **시간** 형식) 또는 **SQL_C_SS_TIMESTAMPOFFSET** ( **datetimeoffset**) 대신 **SQL_C_BINARY**응용 프로그램에서 ODBC 3.8을 사용 하는 경우. 자세한 내용은 [ODBC 날짜 및 시간 기능 향상을 위한 데이터 형식 지원](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)합니다.  

-   호출 **SQLGetData** 작은 버퍼로 여러 번 큰 매개 변수 값을 검색 합니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](http://go.microsoft.com/fwlink/?LinkID=191494)합니다.  

 다음 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서의 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client 동작 변경에 대해 설명합니다.  

-   호출할 때 **icommandwithparameters:: Setparameterinfo**, 전달 되는 값을 *pwszName* 매개 변수는 유효한 식별자 여야 합니다. 자세한 내용은 [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)합니다.  

-   **SQLDescribeParam** 은 ODBC 사양 표준에 맞는 값을 일관성 있게 반환 합니다. 자세한 내용은 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)합니다.  

-   [문자 변환을 처리 시 ODBC 드라이버 동작 변경](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>참고자료  
[SQL Server Native Client 설치](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client 기능](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
