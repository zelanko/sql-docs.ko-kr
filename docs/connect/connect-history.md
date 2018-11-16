---
title: Microsoft SQL Server에 대 한 드라이버 기록 | Microsoft Docs
ms.custom: ''
ms.date: 5/4/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: d040c333aec94cc1de41df03906470356a530faa
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51605633"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server에 대 한 드라이버 기록

이 페이지에는 SQL Server에 연결 하기 위한 Microsoft의 기록 데이터 연결 기술을 설명 합니다.

## <a name="odbc"></a>ODBC

SQL Server 용 Microsoft ODBC 드라이버의 세 고유 세대가 있습니다. 일부로 계속 제공 되는 첫 번째 "SQL Server" ODBC 드라이버 [Windows Data Access Components](#microsoft-or-windows-data-access-components)합니다. 하지 새로운 개발에이 드라이버를 사용 하는 것이 좋습니다. SQL Server 2005부터 합니다 [SQL Server Native Client](#sql-server-native-client) ODBC 인터페이스를 포함 하 고 SQL Server 2012를 통해 SQL Server 2005와 함께 제공 되는 ODBC 드라이버입니다. 하지 새로운 개발에이 드라이버를 사용 하는 것이 좋습니다. SQL Server 2012 이후에 [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server) 앞으로 최신 서버 기능을 사용 하 여 업데이트 되는 드라이버입니다.

### <a name="sql-server-native-client"></a>SQL Server Native Client 

SQL Server Native Client는 OLE DB 및 ODBC 모두에 사용 되는 독립 실행형 라이브러리입니다. SQL Server Native Client (종종 약식된 SNAC) 2012를 통해 SQL Server 2005에 포함 되었습니다. SQL Server 2012를 통해 SQL Server 2005에 도입 된 새 기능을 활용 해야 하는 응용 프로그램에 대 한 SQL Server Native Client은 사용할 수 있습니다. (Microsoft/Windows Data Access Components SQL Server에서 이러한 새 기능에 대 한 업데이트 되지 않습니다.) SQL Server 2012 이상의 새로운 기능에 대 한 SQL Server Native Client 업데이트 되지 않습니다. 전환할 Microsoft ODBC Driver for SQL Server 또는 Microsoft OLE DB Driver for SQL Server 앞으로 새 SQL Server 기능을 활용 하려는 경우.

SQL Server Native Client의 전체 설명서를 참조 하세요. 합니다 [SQL Server Native Client 설명서](../relational-databases/native-client/sql-server-native-client-programming.md)합니다.

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 이후에 SQL Server에 대 한 기본 ODBC 드라이버 개발 되었으며 SQL Server 용 Microsoft ODBC Driver로 출시 됩니다. 자세한 내용은 참조는 [Microsoft ODBC Driver for SQL Server 설명서](./odbc/microsoft-odbc-driver-for-sql-server.md)합니다.

## <a name="ole-db"></a>OLE DB

SQL Server 용 Microsoft OLE DB 공급자의 세 가지 고유한 세대가 있습니다. 일부로 계속 제공 되는 첫 번째 "Microsoft OLE DB Provider for SQL Server" (SQLOLEDB) [Windows Data Access Components](#microsoft-or-windows-data-access-components)합니다. 새로운 기능을 사용 하 여이 공급자 업데이트 되지 않습니다 하 고 새로운 개발에 대 한이 드라이버를 사용 하는 것은 권장 되지 않습니다. SQL Server 2005에서 시작 합니다 [SQL Server Native Client](#sql-server-native-client) OLE DB 공급자 인터페이스 (SQLNCLI)를 포함 하 고 SQL Server 2017을 통해 SQL Server 2005와 함께 제공 되는 OLE DB 공급자입니다. 되었기 [2011에서 사용 중단 될 예정](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) 새로운 개발에이 드라이버를 사용 하는 권장 되지 않습니다. 2017 년에 OLE DB 데이터 액세스 기술 된 이후에 [다시 사용 하 고 새 계획 된 릴리스를 발표](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) 2018에 대 한 합니다. 새 OLE DB 공급자 "Microsoft OLE DB 드라이버에 대 한 SQL Server" (MSOLEDBSQL) 라고는 현재 유지 관리 및 지원 합니다.

## <a name="adonet"></a>ADO.NET

ADO.NET은 Microsoft.NET Framework를 사용 하 여 도입 하 고 개선 되 고 유지 관리를 계속 합니다. Microsoft.NET Framework의 핵심 구성 요소 이며 자세한 내용은 [SQL Server 용 Microsoft ADO.NET](ado-net/microsoft-ado-net-for-sql-server.md)합니다.

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver

Microsoft JDBC Driver for SQL Server 2000에 도입 된, 개선 되 고 유지 관리를 계속 합니다. 2016에서 오픈 소스 이었습니다. 드라이버를 다운로드 하는 방법을 비롯 한 최신 정보를 참조 하세요 [JDBC 드라이버 개요](./jdbc/overview-of-the-jdbc-driver.md)합니다.

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server

오픈 소스 프로젝트로 2009에 도입 된, Microsoft Drivers for PHP for SQL Server 계속 개선 되 고 유지 관리 합니다. PHP driver를 다운로드 하는 방법을 비롯 한 최신 정보를 참조 하세요 [&#40;microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md)합니다.

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Microsoft Driver for SQL Server 용 Node.js

Microsoft Driver for Node.js for SQL Server는 Microsoft SQL Server 및 Microsoft Windows Azure SQL Database에 액세스 하려면 Microsoft Windows 및 Microsoft Windows Azure에서 Node.js 응용 프로그램을 허용 합니다. 개발 작업이이 드라이버에서 더 이상 집중 됩니다. Node.js 용 Microsoft 드라이버를 사용 하 여 SQL Server에 대 한 새 응용 프로그램을 만드는 권장 되지 않습니다.

자세한 내용은 Microsoft 드라이버에 대 한 Node.js에 대 한 SQL Server에 대 한 참조 [WindowsAzure / 노드-sqlserver](https://github.com/Azure/node-sqlserver)합니다.

### <a name="tedious"></a>Tedious

현재 Microsoft에 기여 하 게 되 고 JavaScript를 사용 하 여 SQL Server에 대 한 연결에 대 한 Node.js에서 오픈 소스 지루한 모듈을 지원 합니다. 자세한 내용은 [SQL Server 용 Node.js 드라이버](./node-js/node-js-driver-for-sql-server.md)합니다.

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 또는 Windows Data Access Components

Microsoft/Windows Data Access Components (MDAC/WDAC)에서 지 원하는 Windows 응용 프로그램에 대 한 이전 버전과 호환성 및 현재 SQL Server 기술 스택의 일부로 없는와 함께 제공 됩니다. 새로운 기능은 없습니다 MDAC/WDAC의 구성 요소에 추가 됩니다 하 고 새 응용 프로그램 개발에 대 한 데 좋지 않습니다.

이 문서에서는 기술 및 제품에 따라 다음 구성 요소를 MDAC/WDAC 스택을 나눌 수 있습니다.

* **ADO** (ADOX 및 ADOMD 포함)
* **OLE DB** (OLE DB 핵심 서비스, SQL Server OLE DB 공급자, Oracle OLE DB 공급자, OLE DB Provider for ODBC 드라이버, Data Shape 공급자 및 원격 Data Provider)
* **ODBC** (ODBC 드라이버 관리자, SQL ODBC 드라이버 및 Oracle ODBC 드라이버 포함)

### <a name="mdacwdac-components"></a>MDAC/WDAC 구성 요소

MDAC/WDAC 이러한 구성 요소를 포함 합니다.

* **ODBC:** Microsoft ODBC Open Database Connectivity () 인터페이스는 응용 프로그램의 다양 한 데이터베이스 관리 시스템 (DBMS)의 데이터에 액세스할 수 있도록 하는 C 프로그래밍 언어 인터페이스입니다. 이 API를 사용 하는 응용 프로그램은 관계형 데이터 원본에만 액세스를 제한 합니다.
* **OLE DB:** OLE DB는 다양 한 데이터 저장소에서에서 데이터에 액세스 하는 것에 대 한 COM 인터페이스 집합입니다. OLE DB 공급자는 데이터베이스, 파일 시스템, 메시지 저장소, 디렉터리 서비스, 워크플로 및 문서 저장소의 데이터에 액세스 하기 위해 존재 합니다.
* **ADO:** ActiveX 데이터 개체 (ADO)에 높은 수준의 프로그래밍 모델을 제공 합니다. 하지만 OLE DB 또는 ODBC를 직접 코딩 보다 약간 작습니다은 그리 ADO 배우고 사용 하기 위해 간단 합니다. Microsoft Visual Basic Scripting Edition (VBScript) 또는 Microsoft JScript와 같은 스크립트 언어에서 사용할 수 있습니다.
* **ADOMD:** ADO 다차원 (ADOMD) Microsoft OLAP 공급자 라고도 Microsoft Analysis Services 공급자와 같은 다차원 데이터 공급자와 함께 사용 하는 것입니다. MDAC 2.0부터에 없는 중요 한 기능 기능이 향상 되었습니다.
* **ADOX:** 작성 및 수정을 데이터베이스, 테이블, 인덱스 또는 저장된 프로시저의 정의의 DDL 및 보안 (ADOX)에 대 한 ADO 확장을 사용 하도록 설정 합니다. ADOX 모든 공급자를 사용 하 여 사용할 수 있습니다. Microsoft Jet OLE DB Provider는 Microsoft SQL Server OLE DB Provider에는 제한 된 지원을 제공 하는 동안 전체 ADOX 지원 합니다.
* **Microsoft SQL Server 네트워크 라이브러리:** SQLOLEDB 및 SQLODBC SQL Server 데이터베이스와 통신할 수 있도록 하는 SQL Server 네트워크 라이브러리입니다. 다음 SQL Server 네트워크 라이브러리 사용 되지 않는 MDAC/WDAC 릴리스에서: Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet, 및 RPC 합니다. TCP/IP 및 명명 된 파이프 지원 되는 데 계속 되 고 64 비트 Windows 운영 체제에서 사용할 수 있습니다.
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL)에 빌드된 응용 프로그램은 OLE DB 및 ADO (내부적으로 OLEDB 사용)에서 ODBC 드라이버를 통해 데이터 원본 액세스를 허용 합니다. MSDASQL은 데이터베이스 대신 ODBC에 연결 하는 OLEDB 공급자입니다. 말로 다리 OLE DB에서 ODBC 드라이버를 직접 OLE DB 공급자는 데이터 원본에 존재 하는 경우. MSDASQL은 Windows 운영 체제와 함께 제공 되 고 기술의 64 비트 버전을 포함 하도록 첫 번째 Windows 해제 된 Windows Server 2008 및 Vista SP1.

### <a name="deprecated-mdacwdac-components"></a>사용 되지 않는 MDAC/WDAC 구성 요소

이러한 구성 요소는 현재 MDAC/WDAC 릴리스에서 계속 지원 되지만 이후 릴리스에서 제거 될 수 있습니다. 새 응용 프로그램을 개발할 때 이러한 구성 요소를 사용 하지 않는 것이 좋습니다. 또한 업그레이드 하거나 기존 응용 프로그램은 수정 하면 이러한 구성 요소에 대 한 종속성을 제거 합니다.

* **SQLOLEDB:** Microsoft OLE DB Provider for SQL Server (SQLOLEDB), Microsoft SQL Server에 대 한 액세스를 지 원하는, 사용 되지 않습니다. SQL Server의 나중 버전으로 해당 연결을 지원할 수 있습니다. SQL Server 7 이전 버전에 연결 하는 기능 후 Windows 7 운영 체제에서 제거 됩니다. 새 응용 프로그램에 대 한 SQL Server (MSOLEDBSQL), 새로운 SQL Server 기능을 지 원하는 Microsoft OLE DB 드라이버를 사용 해야 합니다. 기존 응용 프로그램으로 마이그레이션해야 Microsoft OLE DB Driver for SQL Server도 더 나은 성능, 안정성 및 지원 가능성에 대 한 합니다. 자세한 내용은 [MDAC에서 SQL Server 용 OLE DB 드라이버로 응용 프로그램 업데이트](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)합니다.
* **SQLODBC:** 는 Microsoft SQL Server ODBC 드라이버 (SQLODBC), Microsoft SQL Server에 대 한 액세스를 지 원하는, 사용 되지 않습니다. SQL Server의 나중 버전으로 해당 연결을 지원할 수 있습니다. SQL Server 7 이전 버전에 연결 하는 기능 후 Windows 7 운영 체제에서 제거 됩니다. 새 응용 프로그램을 새 SQL Server 기능을 지 원하는 Windows에서 SQL Server 용 Microsoft ODBC Driver를 사용 해야 합니다. 기존 응용 프로그램으로 마이그레이션해야 Microsoft ODBC Driver for SQL Server도 더 나은 성능, 안정성 및 지원 가능성에 대 한 합니다. 관련 정보를 참조 하세요 [MDAC에서 SQL Server Native Client로 응용 프로그램 업데이트](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)합니다.
* **Microsoft Jet 데이터베이스 엔진 4.0:** 버전 2.6 이상에서는 MDAC 이상 Jet 구성 요소를 포함 합니다. 즉, Microsoft Jet, Microsoft Jet OLE DB Provider, ODBC 데스크톱 데이터베이스 드라이버 또는 Jet 데이터 액세스 개체 (DAO)에 MDAC 2.6 고 2.7, 2.8 포함 되지 않습니다. Microsoft Jet 데이터베이스 엔진 4.0 구성 요소 엔지니어링 유지 및 Windows 2000에서 Microsoft Windows의 멤버가 되 면 이후 수준 향상 된 기능을 받지 못한 기능 사용 중단 상태를 입력 합니다.

  사용할 수 없는 64 비트 버전의 Jet 데이터베이스 엔진, Jet OLEDB Driver, Jet ODBC 드라이버 또는 DAO Jet 있습니다. 자세한 내용은 [기술 자료 문서 957570](https://support.microsoft.com/kb/957570)을 참조하십시오. Windows의 64 비트 버전에서 32 비트 Jet Windows WOW64 하위 시스템에서 실행 됩니다. WOW64에 대 한 자세한 내용은 참조는 [MSDN WOW64 설명서](/windows/desktop/WinProg64/wow64-implementation-details)합니다. 네이티브 64 비트 응용 프로그램에서는 WOW64에서 실행 중인 32 비트 Jet 드라이버와 통신할 수 없습니다.

  Microsoft Jet 대신 사용 하 여 것이 좋습니다 [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express) 새 관계형 데이터 저장소를 필요로 하는 비 Microsoft Access 응용 프로그램을 개발 하는 경우. 이러한 새 또는 변환 Jet 응용 프로그램을 위해 Microsoft Office 2003 및 이전 파일 (.mdb 및.xls)를 사용 하 여 Jet을 사용 하 여 기본이 아닌 데이터 저장소에 대 한 계속 수 있습니다. 그러나 이러한 응용 프로그램에 대 한 Jet에서 2007 Office System 드라이버 마이그레이션하도록 계획 해야 있습니다. 할 수 있습니다 [2007 Office System 드라이버 다운로드](https://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=7554f536-8c28-4598-9b72-ef94e038c891)를 읽고 (.mdb 및.xls)의 Office 2003 또는 Office 2007 (*.accdb, *.xlsm, *.xlsx 및 *.xlsb) 파일 형식 중 하나에서 기존 파일에 쓸 수 있습니다.

  > [!IMPORTANT]
  > 특정 사용 제한 사항에 대 한 2007 Office System 최종 사용자 사용권 계약을 읽어보세요.

  > [!NOTE]
  > SQL Server 응용 프로그램 2007 Office System을 액세스할 수도 있습니다 및 앞에서 파일을 SQL Server 유형이 다른 데이터 연결 및 통합 서비스 기능에도 2007 Office System 드라이버를 통해. 또한 64 비트 SQL Server 응용 프로그램 64 비트 Windows에서 32 비트 SQL Server Integration Services (SSIS)를 사용 하 여 32 비트 Jet 및 2007 Office System 파일에 액세스할 수 있습니다.

* **MSDADS:** Microsoft OLE DB Provider에 대 한 데이터 셰이핑 (MSDADS)를 사용 하 여 응용 프로그램에서 키, 필드 또는 행 집합 간의 계층 관계를 만들 수 있습니다. 주요 기능 향상 없이 MDAC 2.1 이후 이루어졌습니다. 이 공급자는 더 이상 사용 되지 않습니다. MSDADS 대신 XML을 사용 하는 것이 좋습니다.
* **Oracle ODBC 및 Oracle OLE DB:** Microsoft Oracle ODBC Driver (Oracle ODBC) 및 Microsoft OLE DB Provider for Oracle (Oracle OLE DB) Oracle 데이터베이스 서버에 대 한 액세스를 제공 합니다. Oracle OCI (Call Interface) 버전 7 사용 하 여 작성 된 하며 Oracle 7에 대 한 전체 지원을 제공 합니다. 또한 Oracle 8 데이터베이스에 대 한 제한 된 지원을 제공 Oracle 7 에뮬레이션을 사용 합니다. Oracle는 OCI 버전 7 호출을 사용 하는 응용 프로그램을 더 이상 지원 합니다. 이러한 기술은 사용 되지 않습니다. Oracle 데이터 소스를 사용 하는 경우 Oracle에서 제공한 드라이버와 공급자를 마이그레이션해야 합니다.
* **RDS:** 원격 데이터 서비스 (RDS)는 인터넷 또는 인트라넷에서 원격 ADO 레코드 집합 개체에 액세스 하기 위한 전용 Microsoft 메커니즘입니다. RDS는 사용 되지 않습니다. MDAC 2.1부터 RDS에 없는 중요 한 기능 기능이 향상 되었습니다. Microsoft는 광범위 한 SOAP 기능을 포함 하 고 RDS 구성 요소를 대체.NET Framework를 출시 했습니다. 모든 RDS 서버 구성 요소는 Windows 7 이후 운영 체제에서 제거 됩니다.
* **JRO:** Jet 복제 개체 (JRO)는 사용 되지 않습니다. JRO Jet 사용 하 여 ADO 내에서 사용 됩니다 (*.mdb) 데이터베이스를 만들어서 Jet 데이터베이스 (.mdb의)을 압축 하 고 Jet 복제 관리를 수행 합니다. MDAC 2.7 마지막 출시 됩니다. JRO 64 비트 Windows 운영 체제에서 제공 되지 않습니다. JRO Microsoft Access 2007 파일 형식에서 지원 되지 않습니다 (*.accdb).
* **16 비트 ODBC 지원:** 16 비트 응용 프로그램을 사용 하는 경우 32 비트 응용 프로그램을로 마이그레이션할 해야 있습니다. 16 비트 기능 않으며 64 비트 운영 체제에서 제거 됩니다. 자세한 내용은 [기술 자료 문서 896458](https://support.microsoft.com/kb/896458)을 참조하십시오.
* **OLEDB 공급자 (MSDAOSP)가 간단한:** OLEDB 간단한 공급자는 간단한 데이터에 대 한 OLE DB 공급자를 신속 하 게 빌드하기 위한 프레임 워크를 제공 합니다. MSDAOSP 사용 되지 않습니다.
* **ODBC 커서 라이브러리:** ODBC 커서 라이브러리 (ODBCCR32.dll) 제한 된 클라이언트 쪽 데이터 커서를 제공 합니다. ODBC 커서 라이브러리는 더 이상 사용 되지 않습니다. 응용 프로그램 대신 서버 쪽 커서 구현을 사용할 수 있습니다.
* **OLE DB-Out-of-process 인터페이스 원격:** OLEDB 인터페이스 원격 (msdaps.dll) OLE DB 공급자가 out-of-process 실행 수를 허용 하려고 합니다. OLEDB-Out-of-process 인터페이스 remoting은 사용 하는 사용 되지 않습니다.
* **AppleTalk 및 Banyan Vines SQL 네트워크 라이브러리:** The Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet, 및 RPC SQL 네트워크 라이브러리를 사용 하는 사용 되지 않습니다. 이러한 기술 중 하나를 사용 하는 경우 TCP/IP 및 명명 된 파이프와 같은 다른 네트워크 라이브러리를 중 하나를 사용 하도록 응용 프로그램을 수정 해야 합니다.

### <a name="mdacwdac-releases"></a>MDAC/WDAC 릴리스

가장 빠른 시작, 과거 MDAC/WDAC 버전의 지원 가능성 시나리오 목록은 다음과 같습니다.

* **MDAC 1.5, MDAC 2.0 및 2.1 MDAC:** 이러한 버전의 MDAC는 Microsoft Windows NT 옵션 팩, Microsoft Windows Platform SDK 또는 MDAC 웹 사이트를 통해 릴리스된 독립 릴리스 되었습니다. 이러한 버전의 MDAC 더 이상 지원 되지.
* **MDAC 2.5:** 이 버전의 MDAC는 Windows 2000 운영 체제에 포함 되어 있습니다. 서비스 팩 MDAC 2.5의 해당 Windows 2000 서비스 팩 포함 되었습니다.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 및 SP2에 포함 된 Microsoft SQL Server 2000 RTM, SP1 및 SP2, 각각. 또한 이러한 MDAC 서비스 팩은 Microsoft SQL Server 2000 서비스 팩 릴리스 일정에 따라 MDAC 웹 사이트에 발표 되었습니다. Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 및 Windows 98 플랫폼에서이 버전의 MDAC 및 서비스 팩을 설치할 수 있습니다. 이 버전의 MDAC에는 더 이상 다음이 지원 됩니다.
* **MDAC 2.7:** 이 버전의 MDAC는 Microsoft Windows XP RTM 및 SP1 운영 체제에 포함 되었습니다. Windows 2000, Windows Millennium, Windows NT 및 Windows 98 플랫폼에서이 버전의 MDAC 및 서비스 팩을 설치할 수 있습니다. 해당 서비스 팩 또는 운영 체제를 통해서만 Windows XP 플랫폼에서이 버전을 설치할 수 있습니다. 이 버전의 MDAC에는 더 이상 다음이 지원 됩니다.
* **MDAC 2.8:** 이 버전의 MDAC 이상 및 Windows Server 2003 및 Windows XP SP2에 포함 되었습니다. Windows 2000에서이 MDAC 및 서비스 팩이 버전을 설치할 수도 있습니다.

  * MDAC 2.8의 32 비트 버전도 출시 되었습니다 MDAC 웹 사이트에 동시에 Windows Server 2003 고객에 게 출시 되었습니다.
  * Windows Server 2003 및 Windows XP 64 비트 버전과 64 비트 버전의 MDAC 2.8 릴리스 되었습니다.

* **Windows Data Access Components (WDAC):** MDAC WDAC-"Windows Data Access Components" Windows Vista 및 Windows Server 2008을 사용 하 여 시작 하려면 해당 이름을 변경 합니다. WDAC 운영 체제의 일부로 포함 됩니다. 되며 개별적으로 재배포 하는 데 사용할 수 없습니다. WDAC에 대 한 서비스는 운영 체제의 수명 주기 될 수 있습니다.

  WDAC의 32 비트 및 64 비트 버전 Windows 운영 체제의 32 비트 및 64 비트 버전을 사용 하 여 각각 해제 됩니다.

## <a name="obsolete-data-access-technologies"></a>사용 되지 않는 데이터 액세스 기술

사용 되지 않는 기술은 되거나 되지 않은 향상 된 몇 가지 제품 릴리스에서 업데이트 및 향후 제품 버전에서 제외 되도록 하는 기술입니다. 새 응용 프로그램을 작성 하는 경우에 이러한 기술을 사용 하지 마세요. 이러한 기술을 사용 하 여 작성 된 기존 응용 프로그램을 수정 하면 ADO.NET 또는 현재 다른 기술과 이러한 응용 프로그램을 마이그레이션하는 것이 좋습니다.

다음 구성 요소는 사용 되지 않는 것으로 간주 됩니다.

* **Db-library:** DB 라이브러리는 C Api를 포함 하는 SQL Server 관련 프로그래밍 모델입니다. SQL Server 6.5 이후에 Db-library에 없는 기능이 향상 되었습니다. SQL Server 2000을 사용 하 여 최종 릴리스 되었으며 64 비트 Windows 운영 체제에 이식할 수 됩니다.
* **포함 된 SQL (E-SQL):** E SQL은 TRANSACT-SQL 문을 Visual C 코드에 포함 될 수 있도록 하는 SQL Server 관련 프로그래밍 모델입니다. SQL Server 6.5 이후에 E-sql 없습니다 기능 기능이 향상 되었습니다. SQL Server 2000을 사용 하 여 최종 릴리스 되었으며 64 비트 Windows 운영 체제에 이식할 수 됩니다.
* **데이터 액세스 개체 (DAO):** DAO JET (Access) 데이터베이스에 대 한 액세스를 제공 합니다. 이 API는 Microsoft Visual Basic, Microsoft Visual c + + 및 스크립팅 언어에서 사용할 수 있습니다. Microsoft Office 2000 및 Office XP에 포함 되어 있었습니다. DAO 3.6에는이 기술의 최종 버전입니다. 64 비트 Windows 운영 체제에서 제공 됩니다.
* **원격 데이터 개체 (RDO):** RDO 원격 ODBC 관계형 데이터 원본에 액세스 하도록 구체적으로 설계 되 고 쉽게 복잡 한 응용 프로그램 코드 없이 ODBC를 사용 합니다. Microsoft Visual Basic 버전 4, 5 및 6에 포함 되어 있었습니다. RDO 버전 2.0에는이 기술의 마지막 버전 이었습니다.
