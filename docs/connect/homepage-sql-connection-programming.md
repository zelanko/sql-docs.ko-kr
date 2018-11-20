---
title: SQL 클라이언트 프로그래밍에 대 한 홈 페이지 | Microsoft Docs
description: 다운로드 한 언어 및 Azure SQL Database 또는 SQL Server에 연결 하는 것에 대 한 운영 체제의 다양 한 조합에 대 한 설명서에 대 한 주석이 추가 된 링크를 사용 하 여 허브 페이지입니다.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: d773e05a3ed953e5210c0ade3226b4a32e82aeab
ms.sourcegitcommit: 8cc38f14ec72f6f420479dc1b15eba64b1a58041
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/08/2018
ms.locfileid: "51289903"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL server 프로그래밍 하는 클라이언트에 대 한 홈 페이지


Microsoft SQL Server와 클라우드의 Azure SQL Database와 상호 작용을 프로그래밍 하는 클라이언트에 대 한 당사의 홈페이지를 시작 합니다. 이 문서에서는 다음 정보를 제공 합니다.

- 나열 하 고 사용 가능한 언어 및 드라이버 조합을 설명 합니다.
    - Linux (Ubuntu 등), MacOS 및 Windows 운영 체제에 대 한 정보가 제공 됩니다.
- 각 조합에 대 한 자세한 설명서 링크를 제공합니다.
- 적절 한 영역 및 특정 언어에 대 한 계층적 설명서의 하위 영역을 표시 합니다.


#### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

지정 된 모든 언어에서 SQL Server에 연결 하는 코드는 Azure SQL Database에 연결 하기 위한 코드와 거의 동일 합니다.

Azure SQL Database에 연결 하기 위한 연결 문자열에 대 한 자세한 내용은 다음을 참조 하세요.

- [.NET Core (C#)를 사용 하 여 Azure SQL database 쿼리](/azure/sql-database/sql-database-connect-query-dotnet-core)합니다.
- 근처의 다른 언어에 대 한 내용의 테이블의 이전 문서는 다른 Azure SQL 데이터베이스입니다. 예를 들어, 참조 [Azure SQL database 쿼리를 사용 하 여 PHP](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)합니다.


#### <a name="build-an-app-webpages"></a>웹 앱을 빌드 페이지

우리의 *앱을 빌드* 웹 페이지의 다른 형식에서 구성 정보와 함께 코드 예제를 제공 합니다. 자세한 내용은이 문서의 뒷부분 참조를 [레이블이 지정 된 섹션 *응용 프로그램 빌드를 웹 사이트*](#an-204-aka-ms-sqldev)합니다.



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>언어 및 클라이언트 프로그램에 대 한 드라이버


다음 표에서 각 언어 이미지에는 SQL Server를 사용 하 여 언어를 사용 하는 방법에 대 한 세부 정보로 링크입니다. 각 링크는이 문서의 뒷부분에 나오는 섹션으로 이동합니다.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C# 로고][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![.NET Framework의 ORM Entity Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 로고][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node.js 로고][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu)<br/>[![cpp 큰 장점][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 로고][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 로고][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 로고][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>다운로드 및 설치

다음 문서를 다운로드 하는 데 및 프로그래밍 언어에서 사용 하기 위해 다양 한 SQL 연결 드라이버를 설치 합니다.

- [SQL Server 드라이버](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 로고][image-ref-320-csharp] ADO.NET을 사용 하 여 C#

C# 및 Visual Basic 같은.NET 관리 되는 언어는 ADO.NET의 가장 일반적인 사용자입니다. *ADO.NET* .NET Framework 클래스의 하위 집합에 대 한 일반 이름입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [ADO.NET을 사용하여 SQL에 연결하는 개념 증명](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | 작은 코드 예제는 연결 및 SQL Server 쿼리를 중점적으로 수행 합니다. |
| [ADO.NET을 사용하여 탄력적으로 SQL에 연결](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | 연결 분 연결 손실의 정도 부딪힐 수 있으므로 코드 예제에서는 논리 다시 시도 하세요.<br /><br />재시도 논리는 유지 관리는 인터넷을 통해 클라우드 데이터베이스에 같은 Azure SQL Database에 연결에도 적용 됩니다. |
| [연결 및 쿼리 하는 C# 프로그램을 만들려면 Windows/Linux/macOS에서.NET Core를 사용 하는 방법의 데모를 azure SQL Database:](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 예입니다. |
| [빌드-는 앱: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

|||
| :-- | :-- |
| [ADO.NET을 사용 하 여 C#](./ado-net/index.md)| 설명서의 루트입니다. |
| [Namespace: System.Data](https://docs.microsoft.com/dotnet/api/system.data) | ADO.NET에 대 한 사용 되는 클래스의 집합입니다. |
| [네임스페이스: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | ADO.NET center 대부분 직접 클래스의 집합입니다. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 로고][image-ref-333-ef] C 사용 하 여 entity Framework (EF)&#x23;

EF (entity Framework)는 개체-관계형 매핑 (ORM)를 제공합니다. ORM 쉽게 관계형 SQL 데이터베이스에서 검색 된 데이터를 조작 하 여 개체 지향 프로그래밍 (OOP) 소스 코드용 있습니다.

EF는 다음과 같은 기술 사용 하 여 직접 또는 간접 관계가:

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), 또는 [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 언어 구문 향상 같은 합니다 **=>** C# 연산자입니다.
- SQL database의 테이블에 매핑되는 클래스에 대 한 소스 코드를 생성 하는 편리한 프로그램. 예를 들어 [EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)합니다.


#### <a name="original-ef-and-new-ef"></a>원래 EF 및 새 EF

합니다 [Entity Framework에 대 한 시작 페이지](https://docs.microsoft.com/ef/) EF 다음과 유사한 설명과 함께 소개 합니다.

- Entity Framework는.NET 개발자가.NET 개체를 사용 하 여 데이터베이스를 작업할 수 있도록 개체 관계형 매퍼 (O/RM). 대부분의 개발자는 일반적으로 작성 해야 하는 데이터 액세스 소스 코드에 대 한 필요가 없습니다.

*Entity Framework* 이름이 두 개의 별도 소스 코드 분기에서 모두 공유 합니다. 이전에 EF 분기 하나 이며 해당 소스 코드는 공개적으로 이제 유지할 수 있습니다. 다른 EF의 새로운 기능입니다. 다음은 두 EFs에 대 한 설명입니다.

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft는 2008 년 8 월에에서 EF를 처음 릴리스 합니다. 2015 년 5 월 Microsoft는 발표 EF 6.x는 Microsoft를 개발 하는 마지막 버전 이었습니다. Microsoft 공용 도메인에 소스 코드를 릴리스 했습니다.<br /><br />처음에 EF는.NET Framework의 일부가 되었습니다. 하지만 EF 6.x는.NET Framework에서 제거 되었습니다.<br /><br />[EF 6.x 소스 코드 리포지토리에 github *aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft은 2016 년 6 월에에서 새로 개발 된 EF Core를 출시 합니다. EF Core는 우수한 유연성과 이식성을 위해 설계 되었습니다. EF Core는 바로 Microsoft Windows 이외의 운영 체제에서 실행할 수 있습니다. 및 EF Core는 Microsoft SQL Server 이외의 데이터베이스 및 기타 관계형 데이터베이스와 상호 작용할 수 있습니다.<br /><br />**C&#x23; 코드 예제:**<br />[Entity Framework Core 시작](https://docs.microsoft.com/ef/core/get-started/index)<br />[기존 데이터베이스를 사용 하 여.NET Framework에서 EF Core 시작](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 및 관련된 기술 강력 되며 전체 영역을 마스터 하려는 개발자를 위한 학습할 내용이 많습니다.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 로고][image-ref-330-java] Java 및 JDBC

Microsoft은 SQL Server를 사용 하 여 (또는 물론 Azure SQL Database를 사용 하 여) 사용에 대 한 Java JDBC (Database Connectivity) 드라이버를 제공합니다. 표준 JDBC API(응용 프로그램 인터페이스)를 통해 데이터베이스 연결을 제공하는 Type 4 JDBC 드라이버입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [코드 예제](./jdbc/code-samples/index.md) | 데이터 형식, 결과 집합 및 큰 데이터에 대 한 설명 하는 코드 예제입니다. |
| [연결 URL 샘플](./jdbc/connection-url-sample.md) | SQL Server에 연결할 연결 URL을 사용 하는 방법에 설명 합니다. 사용 하 여 SQL 문을 사용 하 여 데이터를 검색 합니다. |
| [데이터 원본 샘플](./jdbc/data-source-sample.md) | SQL Server에 연결할 데이터 원본을 사용 하는 방법에 설명 합니다. 다음 데이터를 검색 하는 저장된 프로시저를 사용 합니다. |
| [Java를 사용 하 여 Azure SQL database 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 예입니다. |
| [Ubuntu에서 SQL Server를 사용 하 여 Java 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

다음 주요 영역을 포함 하는 JDBC 설명서:

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | 루트 JDBC 설명서입니다. |
| [참조](./jdbc/reference/index.md) | 인터페이스, 클래스 및 멤버를 선택 합니다. |
| [JDBC SQL 드라이버 프로그래밍 가이드](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 로고][image-ref-340-node] Node.js

Node.js를 사용 하 여 있습니다 수 연결할 SQL Server에서 Windows, Linux 또는 Mac. Node.js 설명서의 루트가 [여기](./node-js/index.md)합니다.

SQL Server 용 Node.js 연결 드라이버는 JavaScript에서 구현 됩니다. 드라이버는 모든 최신 버전의 SQL Server에서 지원 되는 TDS 프로토콜을 사용 합니다. 드라이버는 오픈 소스 프로젝트 [Github에서 사용할 수 있는](https://tediousjs.github.io/tedious/)합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Node.js를 사용하여 SQL에 연결하는 개념 증명](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 기본적인 원본 SQL Server에 연결 및 쿼리 실행에 대 한 코드입니다. |
| [Azure SQL database: Node.js 쿼리를 사용 하 여](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 클라우드에서 Azure SQL Database에 대 한 예제를 제공 합니다. |
| [SQL Server를 사용 하 여 macos에 Node.js 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C + +에 대 한 ODBC 

![ODBC 로고][image-ref-350-odbc] ![cpp 큰 장점][image-ref-322-cpp]

해당.NET Framework 클래스 및 열려 있는 데이터베이스 연결 (ODBC) 1990, 개발 되었습니다. ODBC는 모든 특정 데이터베이스 시스템의 독립적 이며 운영 체제의 독립적인 되도록 설계 되었습니다.

년에 걸쳐 다양 한 ODBC 드라이버 작성 및 Microsoft 내외부에서 그룹 해제 합니다. 드라이버의 범위는 클라이언트는 여러 프로그래밍 언어를 포함 합니다. SQL Server 것을 뛰어넘는 데이터 대상 목록을 이동합니다.

일부 다른 연결 드라이버는 ODBC를 내부적으로 사용 합니다.

#### <a name="code-example"></a>코드 예제

- [C + + 코드 예제에서는 ODBC를 사용 하 여](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>설명서 개요

이 섹션에서는 ODBC 콘텐츠는 c + +에서 SQL Server 또는 Azure SQL Database에 액세스에 중점을 둡니다. 다음 표에서 ODBC에 대 한 주요 설명서에 대 한 대략적인 개요를 나열합니다.


| 영역 | 하위 영역 | 설명 |
| :--- | :------ | :---------- |
| [C + +에 대 한 ODBC](./odbc/index.md) | 설명서의 루트입니다. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Linux 또는 MacOS 운영 체제에서 ODBC를 사용 하는 방법에 대 한 정보입니다. |
| [창](./odbc/windows/index.md)     | &nbsp; | Windows 운영 체제에서 ODBC를 사용 하는 방법에 대 한 정보입니다. |
| [관리](../odbc/admin/index.md) | &nbsp; | ODBC 데이터 소스 관리에 대 한 관리 도구입니다. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 생성 되 고 Microsoft에서 제공 되는 다양 한 ODBC 드라이버. |
| [개념 및 참조](../odbc/reference/index.md) | &nbsp; | 기존 참조 하는 것 외에도 ODBC 인터페이스에 대 한 개념 정보. |
| &nbsp; " | [부록](../odbc/reference/appendixes/index.md)    | 상태 전환 테이블, ODBC 커서 라이브러리 등입니다. |
| &nbsp; " | [앱 개발](../odbc/reference/develop-app/index.md)  | 함수, 핸들 및 등입니다. |
| &nbsp; " | [드라이버 개발](../odbc/reference/develop-driver/index.md) | 특수 한 데이터 원본이 있는 경우 사용자 고유의 ODBC 드라이버를 개발 하는 방법입니다. |
| &nbsp; " | [설치](../odbc/reference/install/index.md) | ODBC 설치를 더 합니다. |
| &nbsp; " | [구문](../odbc/reference/syntax/index.md)   | 설치, 설치 관리자, 변환 및 데이터 액세스 Api입니다. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 로고][image-ref-360-php] PHP

PHP를 사용 하 여 SQL 서버와 상호 작용할 수 있습니다. PHP 설명서의 루트가 [여기](./php/index.md)합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [PHP를 사용하여 SQL에 연결하는 개념 증명](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 작은 코드 예제는 연결 및 SQL Server 쿼리를 중점적으로 수행 합니다. |
| [PHP를 사용하여 탄력적으로 SQL에 연결](./php/step-4-connect-resiliently-to-sql-with-php.md) | 인터넷 및 클라우드를 통해 연결 분 연결 손실의 정도 부딪힐 수 있으므로 코드 예제에서는 논리 다시 시도 하세요. |
| [Azure SQL database: PHP 쿼리를 사용 하 여](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 예입니다. |
| [RHEL에서 SQL Server를 사용 하려면 PHP 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 로고][image-ref-370-python] Python


SQL Server와 상호 작용에 Python을 사용할 수 있습니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Pyodbc를 사용 하 여 Python 사용 하 여 SQL에 연결 하는 개념 증명](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 작은 코드 예제는 연결 및 SQL Server 쿼리를 중점적으로 수행 합니다. |
| [Azure SQL database: Python 쿼리를 사용 하 여](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 예입니다. |
| [SLES의 SQL Server를 사용 하려면 PHP 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

| 영역 | 설명 |
| :--- | :---------- |
| [SQL Server에는 Python](./python/index.md) | 설명서의 루트입니다. |
| [pymssql 드라이버](./python/pymssql/index.md) | Microsoft는 유지 관리 하거나 pymssql 드라이버를 테스트 하지 않습니다.<br /><br />Pymssql 연결 드라이버에는 Python 프로그램에서 사용할 SQL 데이터베이스에 간단한 인터페이스입니다. Microsoft SQL server Python DB API (PEP 249) 인터페이스를 제공 하는 FreeTDS를 기반으로 Pymssql. |
| [pyodbc 드라이버](./python/pyodbc/index.md)   | Pyodbc 연결 드라이버는 간단한 ODBC 데이터베이스에 액세스 하는 오픈 소스 Python 모듈. DB API 2.0 사양을 구현 않지만 더 많은 Pythonic 편의 사용 하 여 압축 됩니다. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 로고][image-ref-380-ruby] Ruby

Ruby를 사용 하 여 SQL 서버와 상호 작용할 수 있습니다. Ruby 설명서의 루트가 [여기](./ruby/index.md)합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Ruby를 사용하여 SQL에 연결하는 개념 증명](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 작은 코드 예제는 연결 및 SQL Server 쿼리를 중점적으로 수행 합니다. |
| [Azure SQL database: Ruby 쿼리를 사용 하 여](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 예입니다. |
| [SQL Server를 사용 하 여 MacOS에서 Ruby 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[SQL 클라이언트 개발에 대 한 앱을 빌드 웹 사이트](https://www.microsoft.com/sql-server/developer-get-started/)


우리의 [ *앱을 빌드* ](https://www.microsoft.com/sql-server/developer-get-started/) 웹 페이지 프로그래밍 언어를 SQL Server에 연결 하는 것에 대 한 긴 목록에서 선택할 수 있습니다. 및 클라이언트 프로그램에서 다양 한 운영 체제를 실행할 수 있습니다.

*앱을 빌드* 이제 막 시작 하는 개발자를 위한 간단 하 고 완성도 강조 합니다. 단계는 다음과 같은 작업을 설명합니다.

1. Microsoft SQL Server를 설치 하는 방법
2. 도구 및 드라이버를 설치 하는 방법입니다.
3. 선택한 운영 체제에 따라 모든 필요한 구성을 확인 하는 방법.
4. 제공된 된 소스 코드를 컴파일하는 방법입니다.
5. 프로그램을 실행 하는 방법입니다.

다음은 몇 가지 대략적인 개요 웹 사이트에 제공 된 세부 정보:

#### <a name="java-on-ubuntu"></a>Ubuntu에서 Java:

1. 환경 설정
    - 1.1 단계 SQL Server 설치
    - 1.2 단계 설치 Java
    - 1.3 단계: Java Development Kit (JDK) 설치
    - 1.4 단계 설치 Maven
2. SQL Server를 사용 하 여 Java 응용 프로그램 만들기
    - 2.1 단계 SQL Server에 연결 하 고 쿼리를 실행 하는 Java 앱 만들기
    - 2.2 단계는 인기 있는 프레임 워크의 최대 절전 모드를 사용 하 여 SQL Server에 연결 하는 Java 앱 만들기
3. 최대 100 배의 Java 앱을 더 빠르게 확인
    - Columnstore 인덱스를 보여 주기 위해 Java 앱 3.1 단계 만들기

#### <a name="python-on-windows"></a>Windows에 Python:

1. 환경 설정
    - 1.1 단계 SQL Server 설치
    - 1.2 단계 Python 설치
    - SQL Server 용 ODBC 드라이버 및 SQL 명령줄 유틸리티를 설치 하는 1.3 단계
2. SQL Server를 사용 하 여 Python 응용 프로그램 만들기
    - 2.1 단계 SQL Server 용 Python driver를 설치 합니다.
    - 2.2 단계 응용 프로그램에 대 한 데이터베이스 만들기
    - 2.3 단계 SQL Server에 연결 하 고 쿼리를 실행 하는 Python 앱 만들기
3. 최대 100 배의 Python 앱을 더 빠르게 확인
    - 3.1 단계 5 백만 sqlcmd를 사용 하 여 새 테이블 만들기
    - 3.2 단계는이 테이블을 쿼리하고 걸린 시간을 측정 하는 Python 앱 만들기
    - 3.3 단계 쿼리를 실행 하는 데 걸리는 시간을 측정합니다
    - 3.4 단계 추가 테이블에 columnstore 인덱스
    - 3.5 단계 columnstore 인덱스를 사용 하 여 쿼리를 실행 하는 데 걸리는 시간을 측정합니다

다음 스크린샷은 SQL 개발 설명서 웹 사이트의 모양은의 아이디어를 제공 합니다.

#### <a name="choose-a-language"></a>언어 선택

![SQL 개발자 웹 사이트 시작][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>운영 체제를 선택 합니다.

![SQL 개발자 웹 사이트에서 Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>다른 개발


이 섹션에서는 다른 개발 옵션에 대 한 링크를 제공 합니다. 여기에 일반적 Azure 개발을 위한 이러한 동일한 언어를 사용 합니다. 정보를 Azure SQL Database 및 Microsoft SQL Server만 대상으로 하 넘어섭니다.

#### <a name="developer-hub-for-azure"></a>Azure에 대 한 개발자 허브

- [Azure에 대 한 개발자 허브](https://docs.microsoft.com/azure/)
- [.NET 개발자 용 azure](https://docs.microsoft.com/dotnet/azure/)
- [Java 개발자 용 azure](https://docs.microsoft.com/java/azure/)
- [Node.js 개발자 용 azure](https://docs.microsoft.com/nodejs/azure/)
- [Python 개발자 용 azure](https://docs.microsoft.com/python/azure/)
- [Azure에서 PHP 웹 앱 만들기](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>다른 언어

- [Windows에서 SQL Server를 사용 하 여 Go 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

