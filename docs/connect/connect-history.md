---
title: Microsoft SQL Server용 드라이버 기록 | Microsoft Docs
description: 이 페이지에서는 SQL Server에 연결하기 위한 Microsoft의 기록 데이터 연결 기술에 대해 설명합니다.
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3724e9c616a17e490946888d2acc8c886a57545a
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81529070"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server용 드라이버 기록

이 페이지에서는 SQL Server에 연결하기 위한 Microsoft의 기록 데이터 연결 기술에 대해 설명합니다.

## <a name="odbc"></a>ODBC

SQL Server용 Microsoft ODBC 드라이버의 세 가지 고유한 세대가 있습니다. 첫 번째 "SQL Server" ODBC 드라이버는 [Windows Data Access Components](#microsoft-or-windows-data-access-components)의 일부로 여전히 제공됩니다. 새 개발 작업에는 이 드라이버를 사용하지 않는 것이 좋습니다. SQL Server 2005부터 [SQL Server Native Client](#sql-server-native-client)가 ODBC 인터페이스를 포함하며, SQL Server 2005부터 SQL Server 2012까지 함께 제공되는 ODBC 드라이버입니다. 새 개발 작업에는 이 드라이버를 사용하지 않는 것이 좋습니다. SQL Server 2012 이후는 [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)가 최신 서버 기능으로 업데이트된 드라이버입니다.

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client는 OLE DB와 ODBC 모두에 사용되는 독립 실행형 라이브러리입니다. SQL Server Native Client(SNAC)는 SQL Server 2005~2012에 포함되었습니다. SQL Server Native Client는 SQL Server 2005~SQL Server 2012에 도입된 새로운 기능을 활용해야 하는 애플리케이션에 사용할 수 있습니다. (Microsoft/Windows Data Access Components는 SQL Server의 이러한 새 기능에 대해 업데이트되지 않습니다.) SQL Server 2012 이후 새로운 기능에 대해서는 SQL Server Native Client가 업데이트되지 않습니다. 계속해서 새로운 SQL Server 기능을 활용하려면 Microsoft ODBC Driver for SQL Server 또는 Microsoft OLE DB Driver for SQL Server로 전환하세요.

SQL Server Native Client에 대한 전체 설명은 [SQL Server Native Client 설명서](../relational-databases/native-client/sql-server-native-client-programming.md)를 참조하세요.

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 이후 SQL Server용 기본 ODBC 드라이버가 개발되고 Microsoft ODBC Driver for SQL Server로 릴리스되었습니다. 자세한 내용은 [Microsoft ODBC Driver for SQL Server 설명서](./odbc/microsoft-odbc-driver-for-sql-server.md)를 참조하세요.

## <a name="ole-db"></a>OLE DB

Microsoft OLE DB Provider for SQL Server의 세 가지 고유한 세대가 있습니다. 첫 번째 “Microsoft OLE DB Provider for SQL Server”(SQLOLEDB)는 [Windows Data Access Components](#microsoft-or-windows-data-access-components)의 일부로 계속 제공됩니다. 이 공급자는 새 기능으로 업데이트되지 않으며 새 개발 작업에 이 드라이버를 사용하지 않는 것이 좋습니다. SQL Server 2005부터 [SQL Server Native Client](#sql-server-native-client)가 SQLNCLI(OLE DB 공급자 인터페이스)를 포함하며 SQL Server 2005~SQL Server 2017에 제공된 OLE DB 공급자입니다. [2011년에 사용되지 않는 드라이버로 발표](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)되었으며, 새로운 개발에 이 드라이버를 사용하지 않는 것이 좋습니다. 2017년에는 OLE DB 데이터 액세스 기술이 [사용되지 않으며 2018년 릴리스 계획이 발표되었습니다](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/). 새 OLE DB 공급자를 "Microsoft OLE DB Driver for SQL Server"(MSOLEDBSQL)라고 하며 현재 유지 관리 및 지원되고 있습니다.

## <a name="adonet"></a>ADO.NET

ADO.NET는 Microsoft .NET Framework에서 도입되었으며 계속 유지 관리 및 향상되고 있습니다. Microsoft .NET Framework의 핵심 구성 요소입니다. 자세한 내용은 [Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-sql-server.md)를 참조하세요.

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>SQL Server용 Microsoft JDBC Driver

2000년에 도입된 Microsoft JDBC Driver for SQL Server는 계속 유지 관리 및 향상되고 있습니다. 2016년에 오픈 소스로 공개되었습니다. 드라이버를 다운로드하는 방법을 비롯한 최신 정보는 [JDBC 드라이버 개요](./jdbc/overview-of-the-jdbc-driver.md)를 참조하세요.

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server

2009년에 오픈 소스 프로젝트로 도입된 Microsoft Drivers for PHP for SQL Server는 계속 유지 관리 및 향상되고 있습니다. PHP 드라이버를 다운로드하는 방법을 비롯한 최신 정보는 [Microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md)를 참조하세요.

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Microsoft Driver for Node.js for SQL Server

Microsoft Driver for Node.js for SQL Server를 사용하면 Microsoft Windows 및 Microsoft Azure에서 Node.js 애플리케이션을 사용하여 Microsoft SQL Server와 Microsoft Azure SQL Database에 액세스할 수 있습니다. 이 드라이버는 더 이상 개발 노력의 초점이 아닙니다. Microsoft Driver for Node.js for SQL Server를 사용하여 새 애플리케이션을 개발하지 않는 것이 좋습니다.

Microsoft Driver for Node.js for SQL Server에 대한 자세한 내용은 [WindowsAzure / node-sqlserver](https://github.com/Azure/node-sqlserver)를 참조하세요.

### <a name="tedious"></a>Tedious

Microsoft에서는 현재 JavaScript를 사용하여 SQL Server에 연결할 수 있도록 Node.js에서 오픈 소스 Tedious 모듈을 지원 및 기여하고 있습니다. 자세한 내용은 [SQL Server용 Node.js 드라이버](./node-js/node-js-driver-for-sql-server.md)를 참조하세요.

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 또는 Windows Data Access Components

Microsoft/Windows Data Access Components(MDAC/WDAC)는 이전 버전 애플리케이션과의 호환성을 위해 Windows에서 제공 및 지원되며 현재 SQL Server 기술 스택의 일부가 아닙니다. MDAC/WDAC의 구성 요소는 새로운 기능이 추가되지 않으므로 새 애플리케이션 개발에 사용하지 않는 것이 좋습니다.

이 문서의 목적을 위해 MDAC/WDAC 스택을 기술 및 제품을 기반으로 다음 구성 요소로 나눌 수 있습니다.

* **ADO**(ADOMD 및 ADOX 포함)
* **OLE DB**(OLE DB Core Services, SQL Server OLE DB Provider, Oracle OLE DB Provider, OLE DB Provider for ODBC Drivers, Data Shape Provider 및 Remote Data Provider 포함)
* **ODBC**(ODBC 드라이버 관리자, SQL ODBC 드라이버 및 Oracle ODBC 드라이버 포함)

### <a name="mdacwdac-components"></a>MDAC/WDAC 구성 요소

MDAC/WDAC에는 다음 구성 요소가 포함됩니다.

* **ODBC:** Microsoft ODBC(Open Database Connectivity) 인터페이스는 애플리케이션에서 다양한 DBMS(데이터베이스 관리 시스템)의 데이터에 액세스할 수 있도록 하는 C 프로그래밍 언어 인터페이스입니다. 이 API를 사용하는 애플리케이션은 관계형 데이터 원본에만 액세스하도록 제한됩니다.
* **OLE DB:** OLE DB는 다양한 데이터 저장소의 데이터에 액세스하기 위한 COM 인터페이스 집합입니다. 데이터베이스, 파일 시스템, 메시지 저장소, 디렉터리 서비스, 워크플로 및 문서 저장소의 데이터에 액세스하기 위한 OLE DB 공급자가 있습니다.
* **ADO:** ADO(ActiveX Data Objects)는 상위 수준 프로그래밍 모델을 제공합니다. OLE DB 또는 ODBC를 직접 코딩하는 것보다 약간 떨어지는 성능이지만 ADO는 학습하고 사용하기 쉽습니다. VBScript(Microsoft Visual Basic Scripting Edition) 또는 Microsoft JScript와 같은 스크립트 언어에서 사용할 수 있습니다.
* **ADOMD:** ADOMD(ADO Multi-Dimensional)는 Microsoft Analysis Services Provider라고도하는 Microsoft OLAP Provider와 같은 다차원 데이터 공급자와 함께 사용됩니다. MDAC 2.0 이후 주요 기능 향상이 적용되지 않았습니다.
* **ADOX:** DDL 및 보안용 ADOX(ADO 확장)를 사용하면 데이터베이스, 테이블, 인덱스 또는 저장 프로시저의 정의를 만들고 수정할 수 있습니다. 모든 공급자에서 ADOX를 사용할 수 있습니다. Microsoft Jet OLE DB Provider는 ADOX에 대한 전체 지원을 제공하고, Microsoft SQL Server OLE DB Provider는 제한된 지원을 제공합니다.
* **Microsoft SQL Server 네트워크 라이브러리:** SQL Server 네트워크 라이브러리를 통해 SQLOLEDB 및 SQLODBC가 SQL Server 데이터베이스와 통신할 수 있습니다. 다음 SQL Server 네트워크 라이브러리는 MDAC/WDAC 릴리스에서 더 이상 사용되지 않습니다. Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet 및 RPC. TCP/IP 및 명명된 파이프는 계속 지원되며 64비트 Windows 운영 체제에서 사용할 수 있습니다.
* **MSDASQL:** MSDASQL(Microsoft OLE DB Provider for ODBC)를 사용하면 OLE DB 및 ADO(내부적으로 OLEDB를 사용)를 기반으로 하는 애플리케이션에서 ODBC 드라이버를 통해 데이터 원본에 액세스할 수 있습니다. MSDASQL은 데이터베이스 대신 ODBC에 연결하는 OLEDB 공급자입니다. 데이터 원본에 대한 직접 OLE DB 공급자가 없는 경우에는 OLE DB에서 ODBC 드라이버까지의 브리지로 연결됩니다. MSDASQL은 Windows 운영 체제와 함께 제공되며 Windows Server 2008 및 Vista SP1은 이 기술의 64비트 버전을 포함한 최초의 Windows 릴리스였습니다.

### <a name="deprecated-mdacwdac-components"></a>사용되지 않는 MDAC/WDAC 구성 요소

이러한 구성 요소는 현재 릴리스의 MDAC/WDAC에서 계속 지원되지만 이후 릴리스에서는 제거될 수 있습니다. 새 애플리케이션을 개발할 때 이러한 구성 요소를 사용하지 않는 것이 좋습니다. 또한 기존 애플리케이션을 업그레이드하거나 수정하는 경우에도 이러한 구성 요소에 대한 종속성을 제거하세요.

* **SQLOLEDB:** Microsoft SQL Server에 대한 액세스를 지원하는 SQLOLEDB(Microsoft OLE DB Provider for SQL Server)는 더 이상 사용되지 않습니다. 이후 버전의 SQL Server에 대한 연결이 지원되지 않을 수 있습니다. SQL Server 7 이전 버전에 연결하는 기능은 Windows 7 이후 운영 체제에서 제거될 예정입니다. 새 애플리케이션은 새로운 SQL Server 기능을 지원하는 MSOLEDBSQL(Microsoft OLE DB Driver for SQL Server)을 사용해야 합니다. 기존 애플리케이션은 더 나은 성능, 안정성 및 지원 가능성을 위해 Microsoft OLE DB Driver for SQL Server로 마이그레이션해야 합니다. 자세한 내용은 [MDAC에서 OLE DB Driver for SQL Server로 애플리케이션 업데이트](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)를 참조하세요.
* **SQLODBC:** Microsoft SQL Server에 대한 액세스를 지원하는 SQLODBC(Microsoft SQL Server ODBC Driver)는 더 이상 사용되지 않습니다. 이후 버전의 SQL Server에 대한 연결이 지원되지 않을 수 있습니다. SQL Server 7 이전 버전에 연결하는 기능은 Windows 7 이후 운영 체제에서 제거될 예정입니다. 새 애플리케이션은 새로운 SQL Server 기능을 지원하는 Windows의 Microsoft ODBC Driver for SQL Server를 사용해야 합니다. 기존 애플리케이션은 더 나은 성능, 안정성 및 지원 가능성을 위해 Microsoft ODBC Driver for SQL Server로 마이그레이션해야 합니다. 관련 정보는 [MDAC에서 SQL Server Native Client로 애플리케이션 업데이트](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)를 참조하세요.
* **Microsoft Jet 데이터베이스 엔진 4.0:** 버전 2.6부터 MDAC에 Jet 구성 요소가 더 이상 포함되지 않습니다. 즉, MDAC 2.6, 2.7 및 2.8에 Microsoft Jet, Microsoft Jet OLE DB Provider, ODBC 데스크톱 데이터베이스 드라이버 또는 Jet DAO(Data Access Objects)가 포함되어 있지 않습니다. 

  Jet 데이터베이스 엔진, Jet OLEDB 드라이버, Jet ODBC 드라이버 또는 Jet DAO의 64비트 버전은 제공되지 않습니다. 자세한 내용은 [기술 자료 문서 957570](https://support.microsoft.com/kb/957570)을 참조하십시오. 64비트 버전 Windows에서 32비트 Jet가 Windows WOW64 하위 시스템에서 실행됩니다. WOW64에 대한 자세한 내용은 [MSDN WOW64 설명서](/windows/desktop/WinProg64/wow64-implementation-details)를 참조하세요. 기본 64비트 애플리케이션은 WOW64에서 실행되는 32비트 Jet 드라이버와 통신할 수 없습니다.

  Microsoft Jet 대신 관계형 데이터 저장소를 필요로 하는 새로운 비 Microsoft Access 애플리케이션을 개발할 때 [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)을 사용하는 것이 좋습니다. 이러한 새로운 또는 변환된 Jet 애플리케이션은 기본이 아닌 데이터 저장소에 대해 Microsoft Office 2003 및 이전 파일(.mdb 및 .xls)를 사용하여 Jet를 계속 사용할 수 있습니다. 그러나 이러한 애플리케이션의 경우 Jet에서 Microsoft Access 데이터베이스 엔진으로 마이그레이션할 계획을 수립해야 합니다. [Microsoft Access 데이터베이스 엔진](https://www.microsoft.com/download/details.aspx?id=54920)을 다운로드하여 Office 2003(.mdb 및 .xls) 또는 Office 2007(*.accdb, *.xlsm, *.xlsx 및 *.xlsb) 파일 형식으로 기존 파일을 읽고 쓸 수 있습니다.

  > [!IMPORTANT]
  > 특정 사용 제한 사항은 2007 Office System 최종 사용자 사용권 계약을 참조하세요.

  > [!NOTE]
  > SQL Server 애플리케이션은 2007 Office 시스템 드라이버를 통해 SQL Server 이종 데이터 연결 및 통합 서비스 기능에서 2007 Office 시스템(및 이전) 파일에도 액세스할 수 있습니다. 또한 64비트 SQL Server 애플리케이션은 64비트 Windows에서 32비트 SSIS(SQL Server Integration Services)를 사용하여 32비트 Jet 및 2007 Office 시스템 파일에 액세스할 수 있습니다.

* **MSDADS:** MSDADS(Microsoft OLE DB Provider for Data Shaping)를 사용하여 애플리케이션의 키, 필드 또는 행 집합 간에 계층 관계를 만들 수 있습니다. MDAC 2.1 이후 주요 기능 향상이 없습니다. 이 공급자는 더 이상 사용되지 않습니다. MSDADS 대신 XML을 사용하는 것이 좋습니다.
* **Oracle ODBC 및 Oracle OLE DB:** Microsoft Oracle ODBC Driver(Oracle ODBC) 및 Microsoft OLE DB Provider for Oracle(Oracle OLE DB)는 Oracle 데이터베이스 서버에 대한 액세스를 제공합니다. 이러한 기능은 OCI(Oracle Call Interface) 버전 7을 사용하여 작성되었으며 Oracle 7에 대한 전체 지원을 제공합니다. 또한 Oracle 7 에뮬레이션을 사용하여 Oracle 8 데이터베이스에 대해 제한된 지원을 제공합니다. Oracle은 OCI 버전 7 호출을 사용하는 애플리케이션을 더 이상 지원하지 않습니다. 이러한 기술은 더 이상 사용되지 않습니다. Oracle 데이터 원본을 사용하는 경우 Oracle에서 제공하는 드라이버 및 공급자로 마이그레이션해야 합니다.
* **RDS:** RDS(Remote Data Services )는 인터넷 또는 인트라넷을 통해 원격 ADO 레코드 집합 개체에 액세스하는 데 사용할 수 있는 전용 Microsoft 메커니즘입니다. RDS는 더 이상 사용되지 않습니다. MDAC 2.1 이후 RDS에 대한 주요 기능이 향상되지 않았습니다. Microsoft는 다양한 SOAP 기능이 있고 RDS 구성 요소를 대체하는 .NET Framework를 출시했습니다. 모든 RDS 서버 구성 요소는 Windows 7 이후 운영 체제에서 제거됩니다.
* **JRO:** JRO(Jet Replication Objects)는 더 이상 사용되지 않습니다. JRO는 Jet 데이터베이스(.mdb)를 만들고 압축하고 Jet 복제 관리를 수행하기 위해 Jet( *.mdb) 데이터베이스를 사용하는 ADO 내에서 사용됩니다. MDAC 2.7이 마지막 릴리스가 될 예정입니다. JRO는 64비트 Windows 운영 체제에서 사용할 수 없습니다. JRO은 Microsoft Access 2007 파일 형식(* .accdb)에서 지원되지 않습니다.
* **16비트 ODBC 지원:** 16비트 애플리케이션을 사용하는 경우 32비트 애플리케이션으로 마이그레이션해야 합니다. 16비트 기능은 더 이상 사용되지 않으며 64비트 운영 체제에서 제거됩니다. 자세한 내용은 [기술 자료 문서 896458](https://support.microsoft.com/kb/896458)을 참조하십시오.
* **MSDAOSP(OLEDB Simple Provider):** OLEDB Simple Provider는 간단한 데이터를 통해 OLE DB 공급자를 빠르게 구축하기 위한 프레임워크를 제공합니다. MSDAOSP는 더 이상 사용되지 않습니다.
* **ODBC 커서 라이브러리:** ODBC 커서 라이브러리(ODBCCR32)는 제한된 클라이언트 쪽 데이터 커서를 제공합니다. ODBC 커서 라이브러리는 더 이상 사용되지 않습니다. 애플리케이션은 대체 방법으로 서버 쪽 커서 구현을 사용할 수 있습니다.
* **OLE DB Out-of-Process 인터페이스 원격:** OLEDB 인터페이스 원격(msdaps.dll)은 OLE DB 공급자의 out-of-process를 허용하기 위한 시도였습니다. OLEDB Out-of-Process 인터페이스 원격은 더 이상 사용되지 않습니다.
* **AppleTalk 및 Banyan Vines SQL 네트워크 라이브러리:** Banyan Vines, AppleTalk, ServerNet, IPX/SPX, Giganet 및 RPC SQL 네트워크 라이브러리는 더 이상 사용되지 않습니다. 이러한 기술 중 하나를 사용하는 경우 TCP/IP 및 명명된 파이프와 같은 다른 네트워크 라이브러리 중 하나를 사용하도록 애플리케이션을 수정해야 합니다.

### <a name="mdacwdac-releases"></a>MDAC/WDAC 릴리스

다음은 이전 버전의 MDAC/WDAC 릴리스에 대한 지원 가능성 시나리오의 목록입니다(가장 빠른 버전부터 시작).

* **MDAC 1.5, MDAC 2.0 및 MDAC 2.1:** 이러한 MDAC 버전은 Microsoft Windows NT Option Pack, Microsoft Windows Platform SDK 또는 MDAC 웹 사이트를 통해 릴리스된 독립적인 버전입니다. 이러한 MDAC 버전은 더 이상 지원되지 않습니다.
* **MDAC 2.5:** 이 MDAC 버전은 Windows 2000 운영 체제에 포함되었습니다. MDAC 2.5의 서비스 팩은 해당 Windows 2000 서비스 팩에 포함되었습니다.
* **MDAC 2.6:** MDAC 2.6 RTM, SP1 및 SP2는 각각 Microsoft SQL Server 2000 RTM, SP1 및 SP2에 각각 포함되었습니다. 또한 이러한 MDAC 서비스 팩은 Microsoft SQL Server 2000 서비스 팩 릴리스 일정에 따라 MDAC 웹 사이트로 릴리스되었습니다. Windows 2000, Windows Millennium Edition, Windows NT, Windows 95 및 Windows 98 플랫폼에 이 버전의 MDAC 및 해당 서비스 팩을 설치할 수 있습니다. 이 MDAC 버전은 더 이상 지원되지 않습니다.
* **MDAC 2.7:** 이 MDAC 버전은 Microsoft Windows XP RTM 및 SP1 운영 체제에 포함되었습니다. Windows 2000, Windows Millennium, Windows NT 및 Windows 98 플랫폼에 이 버전의 MDAC 및 해당 서비스 팩을 설치할 수 있습니다. 이 버전은 운영 체제 또는 서비스 팩을 통해서만 Windows XP 플랫폼에 설치할 수 있습니다. 이 MDAC 버전은 더 이상 지원되지 않습니다.
* **MDAC 2.8:** 이 MDAC 버전은 Windows Server 2003 및 Windows XP SP2 이상에 포함되었습니다. Windows 2000에 이 버전의 MDAC 및 해당 서비스 팩을 설치할 수도 있습니다.

  * 32비트 버전의 MDAC 2.8은 Windows Server 2003을 고객에게 릴리스된 동시에 MDAC 웹 사이트에도 릴리스되었습니다.
  * 64비트 버전의 MDAC 2.8은 Windows Server 2003 및 Windows XP 64비트 버전과 함께 릴리스되었습니다.

* **WDAC(Windows Data Access Components):** MDAC가 Windows Vista 및 Windows Server 2008부터 "Windows Data Access Components"로 이름을 변경했습니다. WDAC는 운영 체제의 일부로 포함되며 재배포를 위해 별도로 사용할 수 없습니다. WDAC에 대한 서비스 기능은 운영 체제의 수명 주기에 따라 결정됩니다.

  32비트 및 64비트 버전의 WDAC는 각각 32비트 및 64비트 버전의 Windows 운영 체제에서 릴리스됩니다.

## <a name="obsolete-data-access-technologies"></a>사용되지 않는 데이터 액세스 기술

사용되지 않는 기술은 여러 제품 릴리스에서 향상되거나 업데이트되지 않은 기술이며 이후 제품 릴리스에서 제외될 예정입니다. 새 애플리케이션을 개발하는 경우에는 이러한 기술을 사용하지 마세요. 이러한 기술을 사용하여 작성된 기존 애플리케이션을 수정하는 경우 해당 애플리케이션을 ADO.NET 또는 다른 최신 기술로 마이그레이션하는 것이 좋습니다.

다음 구성 요소는 사용되지 않는 것으로 간주됩니다.

* **DB-Library:** DB-Library는 C API를 포함하는 SQL Server 관련 프로그래밍 모델입니다. SQL Server 6.5 이후로는 DB-Library의 기능이 향상되지 않았습니다. 최종 릴리스는 SQL Server 2000이었으며, 64비트 Windows 운영 체제로 이식할 수 없습니다.
* **E-SQL(Embedded SQL):** E-SQL은 Transact-SQL 문을 Visual C 코드에 포함할 수 있게 하는 SQL Server 관련 프로그래밍 모델입니다. SQL Server 6.5 이후로는 E-SQL의 기능이 향상되지 않았습니다. 최종 릴리스는 SQL Server 2000이었으며, 64비트 Windows 운영 체제로 이식할 수 없습니다.
* **DAO(Data Access Objects):** DAO는 JET(Access) 데이터베이스에 대한 액세스를 제공합니다. 이 API는 Microsoft Visual Basic, Microsoft Visual C++ 및 스크립팅 언어에서 사용할 수 있습니다. Microsoft Office 2000 및 Office XP에 포함되었습니다. DAO 3.6이 이 기술의 최종 버전입니다. 64비트 Windows 운영 체제에서는 이 기능을 사용할 수 없습니다.
* **RDO(Remote Data Objects):** RDO는 원격 ODBC 관계형 데이터 원본에 액세스하기 위해 특별히 설계되었으며 복잡한 애플리케이션 코드 없이 ODBC를 더 쉽게 사용할 수 있게 되었습니다. Microsoft Visual Basic 버전 4, 5 및 6에 포함되었습니다. RDO 버전 2.0이 이 기술의 최종 버전입니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
