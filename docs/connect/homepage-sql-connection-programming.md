---
title: SQL 클라이언트 프로그래밍 홈 페이지 | Microsoft Docs
description: SQL Server 또는 Azure SQL Database에 연결 하는 데 사용 되는 다양 한 언어 및 운영 체제 조합을 위한 다운로드 및 설명서 링크를 제공 하는 허브 페이지입니다.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451855"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server로의 클라이언트 프로그래밍 홈페이지


Microsoft SQL Server 및 클라우드에서 Azure SQL Database와 상호 작용 하는 클라이언트 프로그래밍에 대 한 홈 페이지를 시작 합니다. 이 문서에서는 다음 정보를 제공합니다.

- 사용 가능한 언어 및 드라이버 조합을 나열 하 고 설명 합니다.
    - Linux (Ubuntu 및 기타), MacOS 및 Windows의 운영 체제에 대 한 정보가 제공 됩니다.
- 각 조합에 대 한 자세한 설명서에 대 한 링크를 제공 합니다.
- 특정 언어에 대 한 계층적 설명서의 영역과 하위 영역을 표시 합니다 (해당 하는 경우).


#### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

지정 된 언어에서 SQL Server에 연결 하는 코드는 Azure SQL Database에 연결 하기 위한 코드와 거의 동일 합니다.

Azure SQL Database에 연결 하기 위한 연결 문자열에 대 한 자세한 내용은 다음을 참조 하세요.

- [.Net Core (C#)를 사용 하 여 Azure SQL database를 쿼리](/azure/sql-database/sql-database-connect-query-dotnet-core)합니다.
- 다른 언어에 대 한 목차에서 이전 문서에 가까이 있는 기타 Azure SQL Database. 예를 들어 [PHP를 사용 하 여 AZURE SQL database 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)를 참조 하세요.


#### <a name="build-an-app-webpages"></a>응용 프로그램 빌드 웹 페이지

*응용 프로그램 빌드* 웹 페이지에서는 구성 정보와 함께 코드 예제를 대체 형식으로 제공 합니다. 자세한 내용은이 문서의 뒷부분에 있는 [ *앱 빌드-앱 웹 사이트*섹션](#an-204-aka-ms-sqldev)을 참조 하세요.



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>클라이언트 프로그램용 언어 및 드라이버


다음 표에서 각 언어 이미지는 SQL Server 언어를 사용 하는 방법에 대 한 자세한 정보 링크입니다. 각 링크는이 문서의 이후 섹션으로 이동 합니다.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C# 로고][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM Entity Framework, .NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 로고][image-ref-330-java]](#an-130-jdbc-docu) |
| [![Node &nbsp; 로고][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 로고][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 로고][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 로고][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>다운로드 및 설치

다음 문서에서는 프로그래밍 언어에서 사용할 수 있도록 다양 한 SQL 연결 드라이버를 다운로드 하 고 설치 하는 방법을 설명 합니다.

- [SQL Server 드라이버](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#로고나][image-ref-320-csharp] C#ADO.NET 사용

C# 및 Visual Basic 같은 .net 관리 언어는 가장 일반적인 ADO.NET 사용자입니다. *ADO.NET* 는 .NET Framework 클래스의 하위 집합에 대 한 일반 이름입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [ADO.NET을 사용하여 SQL에 연결하는 개념 증명](./ado-net/step-3-connect-sql-ado-net.md) | SQL Server 연결 하 고 쿼리 하는 데 초점을 맞춘 작은 코드 예제입니다. |
| [ADO.NET을 사용하여 탄력적으로 SQL에 연결](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | 연결을 다시 시도 하는 경우 연결의 연결 손실이 발생할 수 있기 때문에 코드 예제의 다시 시도 논리<br /><br />재시도 논리는 인터넷을 통해 관리 되는 연결에 대해 Azure SQL Database와 같은 클라우드 데이터베이스로 잘 적용 됩니다. |
| [Azure SQL Database: Windows/Linux/macOS에서 .NET Core를 사용 하 여 C# 프로그램을 만들고 연결 하 고 쿼리 하는 방법에 대 한 데모](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | 예 Azure SQL Database. |
| [빌드-앱: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

|||
| :-- | :-- |
| [C#ADO.NET 사용](./ado-net/index.md)| 설명서의 루트입니다. |
| [네임 스페이스: System.object](https://docs.microsoft.com/dotnet/api/system.data) | ADO.NET에 사용 되는 클래스 집합입니다. |
| [네임스페이스: System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | ADO.NET 중심의 가장 직접적인 클래스 집합입니다. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 로고][image-ref-333-ef] Entity Framework (EF) C&#x23;

EF (Entity Framework)는 ORM (개체 관계형 매핑)을 제공 합니다. ORM을 사용 하면 OOP (개체 지향 프로그래밍) 소스 코드에서 관계형 SQL database에서 검색 된 데이터를 보다 쉽게 조작할 수 있습니다.

EF에는 다음 기술과의 직접 또는 간접 관계가 있습니다.

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)또는 [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 의 C# **=>** 연산자와 같은 언어 구문 향상
- SQL 데이터베이스의 테이블에 매핑되는 클래스에 대 한 소스 코드를 생성 하는 편리한 프로그램입니다. 예를 들면 [edmgen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)입니다.


#### <a name="original-ef-and-new-ef"></a>원본 EF 및 새 EF

[Entity Framework의 시작 페이지](https://docs.microsoft.com/ef/) 에는 다음과 유사한 설명이 포함 된 EF가 도입 되었습니다.

- Entity Framework는 .NET 개발자가 .NET 개체를 사용 하 여 데이터베이스 작업을 수행할 수 있도록 하는 O/RM (개체 관계형 매퍼)입니다. 개발자가 일반적으로 작성 해야 하는 대부분의 데이터 액세스 소스 코드가 필요 하지 않습니다.

*Entity Framework* 는 두 개의 개별 소스 코드 분기에서 공유 하는 이름입니다. 하나의 EF 분기가 오래 된 것 이며, 이제는 공용에서 소스 코드를 유지 관리할 수 있습니다. 다른 EF는 새로운 것입니다. 두 개의 EFs는 다음에 설명 되어 있습니다.

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft는 8 월 2008에 EF를 먼저 출시 했습니다. Microsoft에서 2015 년 3 월에 microsoft에서 개발한 최종 버전을 Microsoft에서 발표 했습니다. Microsoft에서 공용 도메인에 소스 코드를 출시 했습니다.<br /><br />처음에는 EF가 .NET Framework의 일부 였습니다. 그러나 EF 6.x는 .NET Framework에서 제거 되었습니다.<br /><br />[EF *6.x 리포지토리의 Github* 에 있는 EF 6.x 원본 코드](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft는 6 월 2016에 새로 개발 된 EF Core를 출시 했습니다. EF Core은 유연성과 이식성을 향상 시키기 위해 설계 되었습니다. EF Core Microsoft Windows 외의 운영 체제에서 실행할 수 있습니다. 및 EF Core는 Microsoft SQL Server 및 다른 관계형 데이터베이스 이외의 데이터베이스와 상호 작용할 수 있습니다.<br /><br />**C&#x23; 코드 예:**<br />[Entity Framework Core 시작](https://docs.microsoft.com/ef/core/get-started/index)<br />[기존 데이터베이스를 사용 하 여 .NET Framework에 대 한 EF Core 시작](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 및 관련 기술은 강력 하며 전체 영역을 마스터 하려는 개발자에 게 많은 정보를 알려 주는 것이 많습니다.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 로고][image-ref-330-java] Java 및 JDBC

Microsoft는 SQL Server (또는 Azure SQL Database 등)와 함께 사용할 JDBC (Java Database Connectivity) 드라이버를 제공 합니다. 표준 JDBC API(애플리케이션 인터페이스)를 통해 데이터베이스 연결을 제공하는 Type 4 JDBC 드라이버입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [코드 예제](./jdbc/code-samples/index.md) | 데이터 형식, 결과 집합 및 대량 데이터에 대해 학습 하는 코드 예제입니다. |
| [연결 URL 샘플](./jdbc/connection-url-sample.md) | 연결 URL을 사용 하 여 SQL Server에 연결 하는 방법을 설명 합니다. 그런 다음이를 사용 하 여 SQL 문을 사용 하 여 데이터를 검색 합니다. |
| [데이터 원본 샘플](./jdbc/data-source-sample.md) | 데이터 원본을 사용 하 여 SQL Server에 연결 하는 방법을 설명 합니다. 그런 다음 저장 프로시저를 사용 하 여 데이터를 검색 합니다. |
| [Java를 사용 하 여 Azure SQL database 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | 예 Azure SQL Database. |
| [Ubuntu에서 SQL Server를 사용 하 여 Java 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

JDBC 설명서에는 다음과 같은 주요 영역이 포함 되어 있습니다.

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | JDBC 설명서의 루트입니다. |
| [참조](./jdbc/reference/index.md) | 인터페이스, 클래스 및 멤버입니다. |
| [JDBC SQL 드라이버 프로그래밍 가이드](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 로고][image-ref-340-node] Node.js

Node.js를 사용 하 여 Windows, Linux 또는 Mac에서 SQL Server에 연결할 수 있습니다. Node.js 설명서의 루트는 [여기](./node-js/index.md)에 있습니다.

SQL Server 용 node.js 연결 드라이버는 JavaScript에서 구현 됩니다. 드라이버는 모든 최신 버전의 SQL Server에서 지 원하는 TDS 프로토콜을 사용 합니다. 드라이버는 [Github에서 사용할 수 있는](https://tediousjs.github.io/tedious/)오픈 소스 프로젝트입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Node.js를 사용하여 SQL에 연결하는 개념 증명](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | SQL Server에 연결 하 고 쿼리를 실행 하기 위한 완전 한 소스 코드입니다. |
| [Azure SQL database: node.js를 사용 하 여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 클라우드의 Azure SQL Database에 대 한 예입니다. |
| [MacOS에서 SQL Server를 사용 하는 node.js 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBCC++ 

![ODBC 로고][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

ODBC (Open database connectivity)는 1990에서 개발 되었으며 .NET Framework 이전의. ODBC는 특정 데이터베이스 시스템에 독립적 이며 운영 체제와 독립적으로 설계 되었습니다.

수많은 ODBC 드라이버가 Microsoft 내부 및 외부의 그룹에 의해 생성 되 고 릴리스 되었습니다. 드라이버 범위에는 몇 가지 클라이언트 프로그래밍 언어가 포함 됩니다. 데이터 대상 목록이 SQL Server 보다 잘 작동 합니다.

일부 다른 연결 드라이버는 내부적으로 ODBC를 사용 합니다.

#### <a name="code-example"></a>코드 예제

- [C++ 코드 예제, ODBC 사용](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>설명서 개요

이 섹션의 ODBC 내용은에서 C++SQL Server 또는 Azure SQL Database에 액세스 하는 방법에 중점을 두 며 다음 표에서는 ODBC에 대 한 주요 설명서의 대략적인 개요를 보여 줍니다.


| 영역 | 하위 | 설명 |
| :--- | :------ | :---------- |
| [ODBCC++](./odbc/index.md) | 설명서의 루트입니다. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Linux 또는 MacOS 운영 체제에서 ODBC를 사용 하는 방법에 대 한 정보입니다. |
| [창](./odbc/windows/index.md)     | &nbsp; | Windows 운영 체제에서 ODBC를 사용 하는 방법에 대 한 정보입니다. |
| [관리](../odbc/admin/index.md) | &nbsp; | ODBC 데이터 원본 관리를 위한 관리 도구입니다. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Microsoft에서 만들고 제공 하는 다양 한 ODBC 드라이버 |
| [개념 및 참조](../odbc/reference/index.md) | &nbsp; | 기존 참조 외에도 ODBC 인터페이스에 대 한 개념 정보입니다. |
| &nbsp; " | [부록](../odbc/reference/appendixes/index.md)    | 상태 전환 테이블, ODBC 커서 라이브러리 등입니다. |
| &nbsp; " | [앱 개발](../odbc/reference/develop-app/index.md)  | 함수, 핸들 등이 있습니다. |
| &nbsp; " | [드라이버 개발](../odbc/reference/develop-driver/index.md) | 특수 한 데이터 원본이 있는 경우 고유한 ODBC 드라이버를 개발 하는 방법입니다. |
| &nbsp; " | [설치](../odbc/reference/install/index.md) | ODBC 설치, 하위 키 등 |
| &nbsp; " | [구문](../odbc/reference/syntax/index.md)   | 설치, 설치 관리자, 변환 및 데이터 액세스용 Api. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 로고][image-ref-360-php] PHP

PHP를 사용 하 여 SQL Server와 상호 작용할 수 있습니다. PHP 설명서의 루트는 [여기](./php/index.md)에 있습니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [PHP를 사용하여 SQL에 연결하는 개념 증명](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | SQL Server 연결 하 고 쿼리 하는 데 초점을 맞춘 작은 코드 예제입니다. |
| [PHP를 사용하여 탄력적으로 SQL에 연결](./php/step-4-connect-resiliently-to-sql-with-php.md) | 인터넷 및 클라우드를 통한 연결에서 연결 손실이 발생 하는 경우를 대비 하 여 코드 예제에서 재시도 논리를 수행할 수 있습니다. |
| [Azure SQL database: PHP를 사용 하 여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | 예 Azure SQL Database. |
| [RHEL에서 SQL Server 사용할 PHP 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 로고][image-ref-370-python] Python


Python을 사용 하 여 SQL Server와 상호 작용할 수 있습니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Pyodbc를 사용 하 여 Python으로 SQL에 연결 하는 개념 증명](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | SQL Server 연결 하 고 쿼리 하는 데 초점을 맞춘 작은 코드 예제입니다. |
| [Azure SQL database: Python을 사용 하 여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | 예 Azure SQL Database. |
| [SLES에서 SQL Server 사용할 PHP 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

| 영역 | 설명 |
| :--- | :---------- |
| [Python SQL Server](./python/index.md) | 설명서의 루트입니다. |
| [pymssql 드라이버](./python/pymssql/index.md) | Microsoft는 pymssql 드라이버를 유지 관리 하거나 테스트 하지 않습니다.<br /><br />Pymssql 연결 드라이버는 Python 프로그램에서 사용할 수 있는 SQL database에 대 한 간단한 인터페이스입니다. Pymssql는 FreeTDS를 기반으로 하 여 Microsoft SQL Server에 Python DB-LIBRARY (PEP-249) 인터페이스를 제공 합니다. |
| [pyodbc 드라이버](./python/pyodbc/index.md)   | Pyodbc 연결 드라이버는 ODBC 데이터베이스에 간단 하 게 액세스할 수 있도록 하는 오픈 소스 Python 모듈입니다. DB API 2.0 사양을 구현 하지만 훨씬 더 Python 편의를 위해 압축 됩니다. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 로고][image-ref-380-ruby] Ruby

Ruby를 사용 하 여 SQL Server와 상호 작용할 수 있습니다. Ruby 설명서의 루트는 [여기](./ruby/index.md)에 있습니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Ruby를 사용하여 SQL에 연결하는 개념 증명](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | SQL Server 연결 하 고 쿼리 하는 데 초점을 맞춘 작은 코드 예제입니다. |
| [Azure SQL database: Ruby를 사용 하 여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | 예 Azure SQL Database. |
| [MacOS에서 SQL Server 사용할 Ruby 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 코드 예제와 함께 구성 정보 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[빌드-앱 웹 사이트, SQL 클라이언트 개발용](https://www.microsoft.com/sql-server/developer-get-started/)


[*앱 빌드-앱*](https://www.microsoft.com/sql-server/developer-get-started/) 내 웹 페이지에서 SQL Server에 연결 하기 위한 긴 프로그래밍 언어 목록 중에서 선택할 수 있습니다. 그리고 클라이언트 프로그램은 다양 한 운영 체제를 실행할 수 있습니다.

*빌드-앱* 은 단순히 시작 된 개발자에 대 한 단순성 및 완전성을 강조 합니다. 이 단계에서는 다음 작업을 설명 합니다.

1. Microsoft SQL Server 설치 방법
2. 도구 및 드라이버를 다운로드 하 고 설치 하는 방법
3. 선택한 운영 체제에 맞게 필요한 구성을 만드는 방법
4. 제공 된 소스 코드를 컴파일하는 방법입니다.
5. 프로그램을 실행합니다.

다음은 웹 사이트에서 제공 되는 세부 정보의 대략적인 개요입니다.

#### <a name="java-on-ubuntu"></a>Ubuntu의 Java:

1. 환경 설정
    - 1\.1 단계 SQL Server 설치
    - 1\.2 단계 Java 설치
    - 1\.3 단계 JDK (Java Development Kit) 설치
    - 1\.4 단계 Maven 설치
2. SQL Server를 사용 하 여 Java 응용 프로그램 만들기
    - 2\.1 단계 SQL Server 연결 하 고 쿼리를 실행 하는 Java 앱 만들기
    - 2\.2 단계 인기 있는 프레임 워크 최대 절전 모드를 사용 하 여 SQL Server에 연결 하는 Java 앱 만들기
3. Java 응용 프로그램을 더 빨리 100x로 설정
    - 3\.1 단계-Columnstore 인덱스를 시연 하는 Java 앱 만들기

#### <a name="python-on-windows"></a>Windows의 Python:

1. 환경 설정
    - 1\.1 단계 SQL Server 설치
    - 1\.2 단계 Python 설치
    - 1\.3 단계 SQL Server에 대 한 ODBC 드라이버 및 SQL 명령줄 유틸리티 설치
2. SQL Server를 사용 하 여 Python 응용 프로그램 만들기
    - 2\.1 단계 SQL Server 용 Python 드라이버 설치
    - 2\.2 단계 응용 프로그램에 대 한 데이터베이스 만들기
    - 2\.3 단계 SQL Server 연결 하 고 쿼리를 실행 하는 Python 앱 만들기
3. Python 앱을 더 빨리 100x 가능 하 게 만들기
    - 3\.1 단계 sqlcmd를 사용 하 여 500만를 사용 하 여 새 테이블 만들기
    - 3\.2 단계이 테이블을 쿼리하고 소요 시간을 측정 하는 Python 앱 만들기
    - 3\.3 단계 쿼리를 실행 하는 데 걸리는 시간 측정
    - 3\.4 단계 테이블에 columnstore 인덱스 추가
    - 3\.5 단계는 columnstore 인덱스를 사용 하 여 쿼리를 실행 하는 데 걸리는 시간을 측정 합니다.

다음 스크린샷은 SQL 개발 설명서 웹 사이트의 모습을 알려 줍니다.

#### <a name="choose-a-language"></a>언어 선택

![SQL Dev 웹 사이트, 시작][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>운영 체제 선택:

![SQL Dev 웹 사이트, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>기타 개발


이 섹션에서는 다른 개발 옵션에 대 한 링크를 제공 합니다. 여기에는 일반적으로 Azure 개발에 동일한 언어를 사용 하는 것이 포함 됩니다. 정보는 Azure SQL Database 및 Microsoft SQL Server를 대상으로 하지 않습니다.

#### <a name="developer-hub-for-azure"></a>Azure 용 개발자 허브

- [Azure 용 개발자 허브](https://docs.microsoft.com/azure/)
- [.NET 개발자 용 Azure](https://docs.microsoft.com/dotnet/azure/)
- [Java 개발자 용 Azure](https://docs.microsoft.com/java/azure/)
- [Node.js 개발자 용 Azure](https://docs.microsoft.com/nodejs/azure/)
- [Python 개발자 용 Azure](https://docs.microsoft.com/python/azure/)
- [Azure에서 PHP 웹 앱 만들기](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>기타 언어

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

