---
title: Microsoft SQL Server에 대 한 드라이버 기록 Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0eb869cf19f128515951421efddc229aa785cdd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451842"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server에 대 한 드라이버 기록

이 페이지에서는 SQL Server에 연결 하기 위한 Microsoft의 기록 데이터 연결 기술에 대해 설명 합니다.

## <a name="odbc"></a>ODBC

SQL Server용 Microsoft ODBC 드라이버의 세 가지 고유한 세대가 있습니다. 첫 번째 "SQL Server" ODBC 드라이버는 [Windows Data Access 구성 요소의](#microsoft-or-windows-data-access-components)일부로 계속 제공 됩니다. 새 개발에는이 드라이버를 사용 하지 않는 것이 좋습니다. SQL Server 2005부터 [SQL Server Native Client](#sql-server-native-client) 는 odbc 인터페이스를 포함 하 고 SQL Server 2005에서 SQL Server 2012를 통해 제공 되는 odbc 드라이버입니다. 새 개발에는이 드라이버를 사용 하지 않는 것이 좋습니다. 2012 SQL Server 후 [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) 은 최신 서버 기능으로 업데이트 된 드라이버입니다.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client은 OLE DB와 ODBC 모두에 사용 되는 독립 실행형 라이브러리입니다. SQL Server Native Client (종종 축약 된 SNAC) SQL Server 2005 ~ 2012에 포함 되었습니다. SQL Server Native Client는 SQL Server 2005 ~ SQL Server 2012에 도입 된 새로운 기능을 활용 해야 하는 응용 프로그램에 사용할 수 있습니다. Microsoft/Windows 데이터 액세스 구성 요소는 SQL Server의 이러한 새 기능에 대해 업데이트 되지 않습니다. SQL Server 2012를 초과 하는 새로운 기능의 SQL Server Native Client는 업데이트 되지 않습니다. 앞으로 새 SQL Server 기능을 활용 하려는 경우 Microsoft ODBC Driver for SQL Server 또는 Microsoft OLE DB Driver for SQL Server으로 전환 합니다.

SQL Server Native Client에 대 한 전체 설명서는 [SQL Server Native Client 설명서](../relational-databases/native-client/sql-server-native-client-programming.md)를 참조 하세요.

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

2012 SQL Server 후에는 SQL Server에 대 한 기본 ODBC 드라이버가 개발 되 고 Microsoft ODBC Driver for SQL Server으로 릴리스 되었습니다. 자세한 내용은 [Microsoft ODBC Driver for SQL Server 설명서](./odbc/microsoft-odbc-driver-for-sql-server.md)를 참조 하세요.

## <a name="ole-db"></a>OLE DB

Microsoft OLE DB Provider for SQL Server의 세 가지 고유한 세대가 있습니다. 첫 번째 “Microsoft OLE DB Provider for SQL Server”(SQLOLEDB)는 [Windows Data Access Components](#microsoft-or-windows-data-access-components)의 일부로 계속 제공됩니다. 이 공급자는 새 기능으로 업데이트 되지 않으며 새로운 개발에이 드라이버를 사용 하지 않는 것이 좋습니다. SQL Server 2005부터 [SQL Server Native Client](#sql-server-native-client) 는 SQLNCLI (OLE DB 공급자 인터페이스)를 포함 하 고 SQL Server 2005를 통해 SQL Server 2017과 함께 제공 되는 OLE DB 공급자입니다. [2011년에 사용되지 않는 드라이버로 발표](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)되었으며, 새로운 개발에 이 드라이버를 사용하지 않는 것이 좋습니다. 2017에서는 OLE DB 데이터 액세스 기술이 [더 이상 사용 되지 않으며 새로운 계획 된 릴리스가](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) 2018에 대해 발표 되었습니다. 새 OLE DB 공급자를 "Microsoft OLE DB Driver for SQL Server" (MSOLEDBSQL) 라고 하며 현재 유지 관리 하 고 지원 합니다.

## <a name="adonet"></a>ADO.NET

ADO.NET는 Microsoft .NET 프레임 워크에서 도입 되었으며 계속 향상 되 고 유지 관리 됩니다. Microsoft .NET Framework의 핵심 구성 요소입니다. 자세한 내용은 [Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-sql-server.md)를 참조 하세요.

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver

2000에서 도입 된 SQL Server 용 Microsoft JDBC Driver는 계속 향상 되 고 유지 관리 됩니다. 2016에서 오픈 소스 였습니다. 드라이버를 다운로드 하는 방법을 비롯 한 최신 정보는 [JDBC 드라이버 개요](./jdbc/overview-of-the-jdbc-driver.md)를 참조 하세요.

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server

2009에서 오픈 소스 프로젝트로 도입 된 Microsoft driver for PHP SQL Server 계속 개선 하 고 유지 관리 합니다. PHP 드라이버를 다운로드 하는 방법을 비롯 한 최신 정보는 [Microsoft Drivers FOR php for SQL Server](./php/microsoft-php-driver-for-sql-server.md)를 참조 하세요.

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>SQL Server 용 Microsoft Driver for node.js

SQL Server 용 Microsoft Driver for node.js 응용 프로그램을 사용 하 여 Microsoft Windows 및 Microsoft Azure에서 node.js 응용 프로그램을 Microsoft SQL Server 하 고 Microsoft Azure SQL Database에 액세스할 수 있습니다. 이 드라이버에 대 한 개발 노력이 더 이상 집중 되지 않습니다. SQL Server 용 node.js 용 Microsoft 드라이버를 사용 하 여 새 응용 프로그램을 만드는 것은 권장 되지 않습니다.

SQL Server 용 node.js 용 Microsoft 드라이버에 대 한 자세한 내용은 [windowsazure.servicebus/node-sqlserver](https://github.com/Azure/node-sqlserver)를 참조 하세요.

### <a name="tedious"></a>Tedious

Microsoft는 현재 JavaScript를 사용 하 여 SQL Server에 연결 하기 위해 node.js에서 오픈 소스 지루한 모듈을 지원 합니다. 자세한 내용은 [SQL Server Node.js Driver](./node-js/node-js-driver-for-sql-server.md)을 참조 하세요.

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 또는 Windows 데이터 액세스 구성 요소

Microsoft/Windows Data Access 구성 요소 (MDAC/WDAC)는 응용 프로그램의 이전 버전과의 호환성을 위해 Windows에서 제공 및 지원 되며 현재 SQL Server 기술 스택의 일부가 아닙니다. MDAC/WDAC의 구성 요소에는 새로운 기능이 추가 되지 않으므로 새 응용 프로그램 개발에 사용 하지 않는 것이 좋습니다.

이 문서의 목적을 위해, MDAC/WDAC 스택을 기술 및 제품을 기반으로 다음 구성 요소로 나눌 수 있습니다.

* **ADO** (ADOMD 및 ADOX 포함)
* **OLE DB** (OLE DB 핵심 서비스, SQL Server OLE DB 공급자, Oracle OLE DB 공급자, ODBC 드라이버용 OLE DB 공급자, 데이터 셰이프 공급자 및 원격 Data Provider 포함)
* **Odbc** (Odbc 드라이버 관리자, SQL odbc 드라이버 및 Oracle odbc 드라이버 포함)

### <a name="mdacwdac-components"></a>MDAC/WDAC 구성 요소

MDAC/WDAC에는 다음 구성 요소가 포함 됩니다.

* **ODBC:** Microsoft ODBC (Open Database Connectivity) 인터페이스는 응용 프로그램에서 다양 한 DBMS (데이터베이스 관리 시스템)의 데이터에 액세스할 수 있도록 하는 C 프로그래밍 언어 인터페이스입니다. 이 API를 사용 하는 응용 프로그램은 관계형 데이터 원본에만 액세스 하도록 제한 됩니다.
* **OLE DB:** OLE DB은 다양 한 데이터 저장소의 데이터에 액세스 하기 위한 COM 인터페이스 집합입니다. 데이터베이스, 파일 시스템, 메시지 저장소, 디렉터리 서비스, 워크플로 및 문서 저장소의 데이터에 액세스 하기 위한 OLE DB 공급자가 있습니다.
* **ADO:** ADO (ADO(ActiveX Data Objects))는 높은 수준의 프로그래밍 모델을 제공 합니다. OLE DB 또는 ODBC를 직접 코딩 하는 것 보다 약간의 성능 이지만 ADO는 학습 하 고 사용 하기 쉽습니다. VBScript (Microsoft Visual Basic Scripting Edition) 또는 Microsoft JScript와 같은 스크립트 언어에서 사용할 수 있습니다.
* **ADOMD:** ADO 다차원 (ADOMD)은 microsoft Analysis Services 공급자 라고도 하는 Microsoft OLAP 공급자와 같은 다차원 데이터 공급자와 함께 사용 됩니다. MDAC 2.0 이후 주요 기능 향상이 적용 되지 않았습니다.
* **ADOX:** DDL 및 Security 용 ADO 확장 (ADOX)을 사용 하면 데이터베이스, 테이블, 인덱스 또는 저장 프로시저의 정의를 만들고 수정할 수 있습니다. 모든 공급자에서 ADOX를 사용할 수 있습니다. Microsoft Jet OLE DB 공급자는 ADOX에 대 한 완전 한 지원을 제공 하 고 Microsoft SQL Server OLE DB 공급자는 제한 된 지원을 제공 합니다.
* **네트워크 라이브러리 Microsoft SQL Server:** SQL Server 네트워크 라이브러리는 SQLOLEDB 및 SQLODBC가 SQL Server 데이터베이스와 통신할 수 있도록 허용 합니다. 다음 SQL Server 네트워크 라이브러리는 MDAC/WDAC 릴리스에서 사용 되지 않습니다. Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet 및 RPC. TCP/IP 및 명명 된 파이프는 계속 지원 되며 64 비트 Windows 운영 체제에서 사용할 수 있습니다.
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL)를 사용 하면 OLE DB 및 ADO (내부적으로 OLEDB를 사용 하는)를 기반으로 하는 응용 프로그램에서 ODBC 드라이버를 통해 데이터 원본에 액세스할 수 있습니다. MSDASQL는 데이터베이스 대신 ODBC에 연결 하는 OLEDB 공급자입니다. 데이터 원본에 대 한 직접 OLE DB 공급자가 없는 경우에는 OLE DB에서 ODBC 드라이버로의 브리지로 연결 됩니다. MSDASQL는 Windows 운영 체제와 함께 제공 되며 windows Server 2008 및 Vista s p 1은 64 비트 버전의 기술을 포함 하는 최초의 Windows 릴리스입니다.

### <a name="deprecated-mdacwdac-components"></a>사용 되지 않는 MDAC/WDAC 구성 요소

이러한 구성 요소는 현재 버전의 MDAC/WDAC에서 계속 지원 되지만 이후 릴리스에서 제거 될 수 있습니다. 새 응용 프로그램을 개발할 때 이러한 구성 요소를 사용 하지 않는 것이 좋습니다. 또한 기존 응용 프로그램을 업그레이드 하거나 수정 하는 경우 이러한 구성 요소에 대 한 종속성을 제거 합니다.

* **SQLOLEDB:** Microsoft SQL Server에 대 한 액세스를 지 원하는 SQLOLEDB (Microsoft OLE DB Provider for SQL Server)는 더 이상 사용 되지 않습니다. 이후 버전의 SQL Server에 대 한 연결이 지원 되지 않을 수 있습니다. SQL Server 7 이전 버전에 연결 하는 기능은 Windows 7 이후 운영 체제에서 제거 될 예정입니다. 새 응용 프로그램은 새로운 SQL Server 기능을 지 원하는 MSOLEDBSQL (Microsoft OLE DB Driver for SQL Server)를 사용 해야 합니다. 기존 응용 프로그램은 더 나은 성능, 안정성 및 지원 가능성을 위해 SQL Server Microsoft OLE DB 드라이버로 마이그레이션해야 합니다. 자세한 내용은 [MDAC의 SQL Server에 대 한 OLE DB 드라이버로 응용 프로그램 업데이트](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)를 참조 하세요.
* **SQLODBC:** Microsoft SQL Server에 대 한 액세스를 지 원하는 Microsoft SQL Server ODBC 드라이버 (SQLODBC)는 더 이상 사용 되지 않습니다. 이후 버전의 SQL Server에 대 한 연결이 지원 되지 않을 수 있습니다. SQL Server 7 이전 버전에 연결 하는 기능은 Windows 7 이후 운영 체제에서 제거 될 예정입니다. 새 응용 프로그램은 새로운 SQL Server 기능을 지 원하는 Windows의 Microsoft ODBC Driver for SQL Server를 사용 해야 합니다. 기존 응용 프로그램은 성능, 안정성 및 지원 가능성을 향상 시키기 위해 Microsoft ODBC Driver for SQL Server로 마이그레이션해야 합니다. 관련 정보는 [MDAC에서 SQL Server Native Client 응용 프로그램 업데이트](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)를 참조 하세요.
* **Microsoft Jet 데이터베이스 엔진 4.0:** 버전 2.6부터 MDAC에 Jet 구성 요소가 더 이상 포함 되지 않습니다. 즉, MDAC 2.6, 2.7 및 2.8에 Microsoft Jet, Microsoft Jet OLE DB 공급자, ODBC 데스크톱 데이터베이스 드라이버 또는 Jet DAO (Data Access Objects)가 포함 되어 있지 않습니다. 

  Jet 데이터베이스 엔진, jet OLEDB 드라이버, Jet ODBC 드라이버 또는 Jet DAO의 64 비트 버전은 제공 되지 않습니다. 자세한 내용은 [기술 자료 문서 957570](https://support.microsoft.com/kb/957570)을 참조하십시오. 64 비트 버전의 Windows에서 32 비트 Jet는 Windows WOW64 하위 시스템에서 실행 됩니다. W o w 64에 대 한 자세한 내용은 [MSDN WOW64 설명서](/windows/desktop/WinProg64/wow64-implementation-details)를 참조 하세요. Native 64 비트 응용 프로그램은 w o w 64에서 실행 되는 32 비트 Jet 드라이버와 통신할 수 없습니다.

  Microsoft Jet 대신 관계형 데이터 저장소가 필요한 새로운 비 Microsoft Access 응용 프로그램을 개발할 때 [Microsoft SQL Server Express 버전](https://www.microsoft.com/sql-server/sql-server-editions-express) 을 사용 하는 것이 좋습니다. 이러한 새로운 또는 변환 된 Jet 응용 프로그램은 기본이 아닌 데이터 저장소에 대해 Microsoft Office 2003 및 이전 파일 (.mdb 및 .xls)를 사용 하 여 Jet를 계속 사용할 수 있습니다. 그러나 이러한 응용 프로그램의 경우 Jet에서 Microsoft Access 데이터베이스 엔진로 마이그레이션할 계획을 세워야 합니다. [Microsoft Access 데이터베이스 엔진를 다운로드](https://www.microsoft.com/download/details.aspx?id=54920)하 여 office 2003 (.mdb 및 .xls) 또는 office 2007 (* .accdb, * .xlsm, * .xlsx 및 * .xlsb) 파일 형식으로 기존 파일을 읽고 쓸 수 있습니다.

  > [!IMPORTANT]
  > 특정 사용 제한 사항은 2007 Office System 최종 사용자 사용권 계약을 참조 하십시오.

  > [!NOTE]
  > SQL Server 응용 프로그램은 2007 Office 시스템 드라이버를 통해 다른 유형의 데이터 연결 및 통합 서비스 기능 SQL Server의 2007 Office 시스템에도 액세스할 수 있습니다. 또한 64 비트 SQL Server 응용 프로그램은 64 비트 Windows에서 SQL Server Integration Services (SSIS)를 32 사용 하 여 32 비트 Jet 및 2007 Office 시스템 파일에 액세스할 수 있습니다.

* **MSDADS:** 데이터 셰이핑을 위한 Microsoft OLE DB 공급자 (MSDADS)를 사용 하 여 응용 프로그램의 키, 필드 또는 행 집합 간에 계층 관계를 만들 수 있습니다. MDAC 2.1 이후 주요 기능 개선 사항이 없습니다. 이 공급자는 더 이상 사용 되지 않습니다. MSDADS 대신 XML을 사용 하는 것이 좋습니다.
* **ORACLE ODBC 및 oracle OLE DB:** Microsoft Oracle ODBC Driver (Oracle ODBC) 및 Microsoft OLE DB Provider for Oracle (oracle OLE DB)는 Oracle 데이터베이스 서버에 대 한 액세스를 제공 합니다. 이러한 기능은 OCI (Oracle Call Interface) 버전 7을 사용 하 여 작성 되었으며 Oracle 7에 대 한 완전 한 지원을 제공 합니다. 또한 oracle 7 에뮬레이션을 사용 하 여 Oracle 8 데이터베이스에 대해 제한 된 지원을 제공 합니다. Oracle은 OCI 버전 7 호출을 사용 하는 응용 프로그램을 더 이상 지원 하지 않습니다. 이러한 기술은 더 이상 사용 되지 않습니다. Oracle 데이터 원본을 사용 하는 경우 Oracle에서 제공 하는 드라이버 및 공급자로 마이그레이션해야 합니다.
* **RDS:** RDS (원격 Data Services)는 인터넷 이나 인트라넷을 통해 원격 ADO 레코드 집합 개체에 액세스 하는 데 사용할 수 있는 전용 Microsoft 메커니즘입니다. RDS는 사용 되지 않습니다. MDAC 2.1 이후 RDS에 대 한 주요 기능이 향상 되지 않았습니다. Microsoft는 다양 한 SOAP 기능이 있으며 RDS 구성 요소를 대체 하는 .NET Framework를 출시 했습니다. 모든 RDS 서버 구성 요소는 Windows 7 이후 운영 체제에서 제거 됩니다.
* **JRO:** Jet 복제 개체 (JRO)는 더 이상 사용 되지 않습니다. JRO는 jet 데이터베이스 (.mdb)를 만들고 압축 하 고 Jet 복제 관리를 수행 하기 위해 Jet ( *.mdb) 데이터베이스를 사용 하는 ADO 내에서 사용 됩니다. MDAC 2.7는 마지막 릴리스가 될 예정입니다. JRO는 64 비트 Windows 운영 체제에서 사용할 수 없습니다. JRO은 Microsoft Access 2007 파일 형식 (* .accdb)에서 지원 되지 않습니다.
* **16 비트 ODBC 지원:** 16 비트 응용 프로그램을 사용 하는 경우 32 비트 응용 프로그램으로 마이그레이션해야 합니다. 16 비트 기능은 더 이상 사용 되지 않으며 64 비트 운영 체제에서 제거 됩니다. 자세한 내용은 [기술 자료 문서 896458](https://support.microsoft.com/kb/896458)을 참조하십시오.
* **OLEDB 단순 공급자 (MSDAOSP):** OLEDB 단순 공급자는 간단한 데이터를 통해 OLE DB 공급자를 빠르게 구축할 프레임 워크를 제공 합니다. MSDAOSP는 사용 되지 않습니다.
* **ODBC 커서 라이브러리:** ODBC 커서 라이브러리 (ODBCCR32)는 제한 된 클라이언트 쪽 데이터 커서를 제공 합니다. ODBC 커서 라이브러리는 더 이상 사용 되지 않습니다. 응용 프로그램은 서버 쪽 커서 구현을 대체 방법으로 사용할 수 있습니다.
* **OLE DB Out-of-process 인터페이스 원격 기능:** OLEDB 인터페이스 원격 (msdaps)이 OLE DB 공급자의 out-of-process 실행을 허용 하려고 했습니다. OLEDB out-of-process 인터페이스 remoting은 더 이상 사용 되지 않습니다.
* **AppleTalk 및 Banyan VINES SQL 네트워크 라이브러리:** Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet 및 RPC SQL 네트워크 라이브러리는 더 이상 사용 되지 않습니다. 이러한 기술 중 하나를 사용 하는 경우 TCP/IP 및 명명 된 파이프와 같은 다른 네트워크 라이브러리 중 하나를 사용 하도록 응용 프로그램을 수정 해야 합니다.

### <a name="mdacwdac-releases"></a>MDAC/WDAC 릴리스

다음은 가장 이른 버전부터 시작 하 여 이전 버전의 MDAC/WDAC 릴리스에 대 한 지원 가능성 시나리오의 목록입니다.

* **Mdac 1.5, mdac 2.0 및 mdac 2.1:** 이러한 MDAC 버전은 Microsoft Windows NT Option Pack, Microsoft Windows Platform SDK 또는 MDAC 웹 사이트를 통해 릴리스된 독립적인 릴리스입니다. 이러한 MDAC 버전은 더 이상 지원 되지 않습니다.
* **MDAC 2.5:** 이 MDAC 버전은 Windows 2000 운영 체제에 포함 되어 있습니다. MDAC 2.5의 서비스 팩은 해당 Windows 2000 서비스 팩에 포함 되어 있습니다.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 및 s p 2는 각각 Microsoft SQL Server 2000 RTM, SP1 및 s p 2에 포함 되었습니다. 또한 이러한 MDAC 서비스 팩은 Microsoft SQL Server 2000 서비스 팩 릴리스 일정에 따라 MDAC 웹 사이트로 릴리스 되었습니다. Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 및 Windows 98 플랫폼에이 버전의 MDAC 및 해당 서비스 팩을 설치할 수 있습니다. 이 MDAC 버전은 더 이상 지원 되지 않습니다.
* **MDAC 2.7:** 이 MDAC 버전은 Microsoft Windows XP RTM 및 SP1 운영 체제에 포함 되어 있습니다. Windows 2000, Windows Millennium, Windows NT 및 Windows 98 플랫폼에이 버전의 MDAC 및 해당 서비스 팩을 설치할 수 있습니다. 이 버전은 운영 체제 또는 서비스 팩을 통해서만 Windows XP 플랫폼에서 설치할 수 있습니다. 이 MDAC 버전은 더 이상 지원 되지 않습니다.
* **MDAC 2.8:** 이 MDAC 버전은 Windows Server 2003 및 Windows XP SP2 이상에 포함 되어 있습니다. Windows 2000에이 버전의 MDAC 및 해당 서비스 팩을 설치할 수도 있습니다.

  * 32 비트 버전의 MDAC 2.8은 Windows Server 2003를 고객에 게 릴리스한 동시에 MDAC 웹 사이트에도 출시 되었습니다.
  * 64 비트 버전의 MDAC 2.8은 Windows Server 2003 및 Windows XP 64 비트 버전과 함께 출시 되었습니다.

* **Windows Data Access Components (WDAC):** MDAC의 이름을 Windows Vista 및 Windows Server 2008부터 "Windows 데이터 액세스 구성 요소"로 변경 했습니다. WDAC는 운영 체제의 일부로 포함 되며 재배포를 위해 별도로 사용할 수 없습니다. WDAC에 대 한 서비스 기능은 운영 체제의 수명 주기에 따라 결정 됩니다.

  32 비트 및 64 비트 버전의 WDAC는 각각 32 비트 및 64 비트 버전의 Windows 운영 체제에서 릴리스됩니다.

## <a name="obsolete-data-access-technologies"></a>사용 되지 않는 데이터 액세스 기술

사용 되지 않는 기술은 여러 제품 릴리스에서 향상 되거나 업데이트 되지 않은 기술 이며 이후 제품 릴리스에서 제외 될 예정입니다. 새 응용 프로그램을 작성 하는 경우에는 이러한 기술을 사용 하지 마세요. 이러한 기술을 사용 하 여 작성 된 기존 응용 프로그램을 수정 하는 경우 해당 응용 프로그램을 ADO.NET 또는 다른 현재 기술로 마이그레이션하는 것이 좋습니다.

다음 구성 요소는 사용 되지 않는 것으로 간주 됩니다.

* **DB-Library:** DB-라이브러리는 C Api를 포함 하는 SQL Server 관련 프로그래밍 모델입니다. SQL Server 6.5부터 DB-LIBRARY의 기능이 향상 되었습니다. 최종 릴리스는 SQL Server 2000으로, 64 비트 Windows 운영 체제로 이식할 수 없습니다.
* **EMBEDDED SQL (E-sql):** E-SQL은 Transact-sql 문을 Visual C 코드에 포함할 수 있도록 하는 SQL Server 별 프로그래밍 모델입니다. SQL Server 6.5 이므로 E-SQL에 기능이 개선 되지 않았습니다. 최종 릴리스는 SQL Server 2000으로, 64 비트 Windows 운영 체제로 이식할 수 없습니다.
* **DAO (Data Access Objects):** DAO는 JET (Access) 데이터베이스에 대 한 액세스를 제공 합니다. 이 API는 Microsoft Visual Basic, Microsoft Visual C++및 스크립팅 언어에서 사용할 수 있습니다. Microsoft Office 2000 및 Office XP에 포함 되었습니다. DAO 3.6은이 기술의 최종 버전입니다. 64 비트 Windows 운영 체제에서는이 기능을 사용할 수 없습니다.
* **Remote Data Objects (RDO):** RDO는 원격 ODBC 관계형 데이터 원본에 액세스 하기 위해 특별히 설계 되었으며 복잡 한 응용 프로그램 코드 없이 ODBC를 더 쉽게 사용할 수 있게 되었습니다. Microsoft Visual Basic 버전 4, 5 및 6에 포함 되었습니다. RDO 버전 2.0은이 기술의 최종 버전 이었습니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
