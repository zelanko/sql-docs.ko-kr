---
title: SQL 클라이언트 프로그래밍 홈페이지 | Microsoft Docs
description: SQL Server 또는 Azure SQL Database에 연결하는 데 사용되는 다양한 언어 및 운영 체제 조합에 대한 다운로드 및 설명서 링크를 제공하는 허브 페이지입니다.
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 145ca5c64223e4d16b327e4caf23458a479b87a9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74491917"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server로의 클라이언트 프로그래밍 홈페이지


Microsoft SQL Server 및 클라우드의 Azure SQL Database와 상호 작용하기 위한 클라이언트 프로그래밍에 관련된 홈페이지에 오신 것을 환영합니다. 이 문서에서는 다음 정보를 제공합니다.

- 사용 가능한 언어 및 드라이버 조합을 나열하고 설명합니다.
    - Linux(Ubuntu 및 기타), MacOS 및 Windows의 운영 체제에 대한 정보를 제공합니다.
- 각 조합의 자세한 설명서에 대한 링크를 제공합니다.
- 특정 언어에 대한 계층적 설명서의 영역 및 하위 영역을 표시합니다(해당 하는 경우).


#### <a name="azure-sql-database"></a>Azure SQL Database

지정된 언어에서 SQL Server에 연결하는 코드는 Azure SQL Database에 연결하기 위한 코드와 거의 동일합니다.

Azure SQL Database에 연결하기 위한 연결 문자열에 대한 자세한 내용은 다음을 참조하세요.

- [.NET Core(C#)를 사용하여 Azure SQL 데이터베이스 쿼리](/azure/sql-database/sql-database-connect-query-dotnet-core).
- Azure SQL Database에서 기타 언어 사용에 대한 설명(목차에서 이전 항목과 가까이 있음). 예를 들어 [PHP를 사용하여 Azure SQL 데이터베이스 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)를 참조하세요.


#### <a name="build-an-app-webpages"></a>앱 빌드 웹 페이지

*앱 빌드* 웹 페이지에서는 구성 정보와 함께 코드 예제를 대체 형식으로 제공합니다. 자세한 내용은 이 문서의 뒷부분에 있는 [*앱 빌드 웹 사이트*](#an-204-aka-ms-sqldev) 섹션을 참조하세요.



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>클라이언트 프로그램용 언어 및 드라이버


다음 표에서 각 언어 이미지는 SQL Server에서 언어를 사용하는 방법에 대한 세부 정보 링크입니다. 각 링크는 이 문서의 이후 섹션으로 이동합니다.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C# 로고][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![.NET Framework의 ORM Entity Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 로고][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node.js 로고][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [ **`ODBC for C++`** ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 로고][image-ref-360-php]](#an-170-php-docu) |
| &nbsp;[![Python 로고][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 로고][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>다운로드 및 설치

다음 문서에서는 프로그래밍 언어에서 사용할 수 있도록 다양한 SQL 연결 드라이버를 다운로드하고 설치하는 방법을 설명합니다.

- [SQL Server 드라이버](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 로고][image-ref-320-csharp] ADO.NET 사용 C#

C# 및 Visual Basic 같은 .NET 관리 언어는 가장 일반적인 ADO.NET 사용자입니다. *ADO.NET*은 .NET Framework 클래스의 하위 집합에 대한 일반 이름입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [ADO.NET을 사용하여 SQL에 연결하는 개념 증명](./ado-net/step-3-connect-sql-ado-net.md) | SQL Server에 연결하고 쿼리하는 데 초점을 맞춘 소형 코드 예제입니다. |
| [ADO.NET을 사용하여 탄력적으로 SQL에 연결](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | 재시도 논리 코드 예제입니다(연결에서 간헐적으로 연결 손실이 발생할 수 있기 때문).<br /><br />재시도 논리는 인터넷을 통해 유지되는 클라우드 데이터베이스(예: Azure SQL Database) 쪽 연결에 잘 적용됩니다. |
| [Azure SQL Database: Windows/Linux/macOS에서 .NET Core를 사용하여 C# 프로그램을 만들고 연결하고 쿼리하는 방법에 대한 데모](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL Database 예제입니다. |
| [앱 빌드: C#, ADO.NET, Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>문서화

|||
| :-- | :-- |
| [ADO.NET 사용 C# ](./ado-net/index.md)| 설명서의 루트입니다. |
| [네임스페이스: System.Data](https://docs.microsoft.com/dotnet/api/system.data) | ADO.NET에 사용되는 클래스 집합입니다. |
| [네임스페이스: Microsoft.Data.SqlClient](https://docs.microsoft.com/dotnet/api/microsoft.data.SqlClient) | Microsoft .NET Data Provider for SQL Server에 사용되는 클래스 집합 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 로고][image-ref-333-ef] C&#x23; 사용 EF(Entity Framework)

EF(Entity Framework)는 ORM(개체 관계 매핑)을 제공합니다. ORM을 사용하면 OOP(개체 지향 프로그래밍) 소스 코드가 관계형 SQL 데이터베이스에서 검색된 데이터를 보다 쉽게 조작할 수 있습니다.

EF는 다음 기술과 직접 또는 간접적인 관계가 있습니다.

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/) 또는 [LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- C#의 **=>** 연산자와 같은 언어 구문 향상 기능입니다.
- SQL 데이터베이스의 테이블에 매핑되는 클래스에 대한 소스 코드를 생성하는 편리한 프로그램입니다. 예: [EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe).


#### <a name="original-ef-and-new-ef"></a>최초 EF, 새로운 EF

[Entity Framework 시작 페이지](https://docs.microsoft.com/ef/)는 다음과 같은 설명으로 EF를 소개합니다.

- Entity Framework는 .NET 개발자가 .NET 개체를 사용하여 데이터베이스 작업을 수행할 수 있도록 하는 O/RM(개체 관계 매퍼)입니다. 여기서는 개발자가 일반적으로 작성해야 하는 대부분의 데이터 액세스 소스 코드가 필요하지 않습니다.

*Entity Framework*는 두 개의 개별 소스 코드 분기에서 공유하는 이름입니다. 한 분기는 최초 EF이며, 이제 소스 코드가 공개적으로 유지 관리됩니다. 다른 분기는 새로운 EF입니다. 두 EF에 대해서는 다음에 설명되어 있습니다.

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft는 2008년 8월 EF를 최초로 발표했습니다. 2015년 3월에는 Microsoft가 개발한 최종 버전인 EF 6.x가 발표되었습니다. Microsoft는 퍼블릭 도메인에 소스 코드를 릴리스했습니다.<br /><br />초기에는 EF가 .NET Framework의 일부였습니다. 그러나 EF 6.x는 .NET Framework에서 제거되었습니다.<br /><br />[Github의 EF 6.x에서 소스 코드, 리포지토리: *aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft는 2016년 6월에 새로 개발된 EF Core를 출시했습니다. EF Core는 향상된 유연성 및 이식성을 제공하도록 설계되었습니다. EF Core는 Microsoft Windows 이외의 운영 체제에서도 실행할 수 있습니다. 또한 EF Core는 Microsoft SQL Server 및 기타 관계형 데이터베이스 이외의 데이터베이스와도 상호 작용할 수 있습니다.<br /><br />**C&#x23; 코드 예제:**<br />[Entity Framework Core 시작하기](https://docs.microsoft.com/ef/core/get-started/index)<br />[기존 데이터베이스를 사용하여 .NET Framework의 EF Core 시작하기](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 및 관련 기술은 강력하며 개발자가 전체 영역을 마스터하려면 학습할 내용이 많습니다.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 로고][image-ref-330-java] Java 및 JDBC

Microsoft는 SQL Server(또는 Azure SQL Database)와 함께 사용할 JDBC(Java Database Connectivity) 드라이버를 제공합니다. 표준 JDBC API(애플리케이션 인터페이스)를 통해 데이터베이스 연결을 제공하는 Type 4 JDBC 드라이버입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [코드 예제](./jdbc/code-samples/index.md) | 데이터 형식, 결과 집합 및 대량 데이터에 대해 학습하는 코드 예제입니다. |
| [연결 URL 샘플](./jdbc/connection-url-sample.md) | 연결 URL을 사용하여 SQL Server에 연결하는 방법을 설명합니다. 그런 다음 이를 통해 SQL 문을 사용하여 데이터를 검색합니다. |
| [데이터 원본 샘플](./jdbc/data-source-sample.md) | 데이터 원본을 사용하여 SQL Server에 연결하는 방법을 설명합니다. 그런 다음 저장 프로시저를 사용하여 데이터를 검색합니다. |
| [Java를 사용하여 Azure SQL Database 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL Database 예제입니다. |
| [Ubuntu에서 SQL Server를 사용하여 Java 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>문서화

JDBC 설명서에는 다음과 같은 주요 영역이 포함되어 있습니다.

|||
| :-- | :-- |
| [Java Database Connectivity(JDBC)](./jdbc/index.md) | JDBC 설명서의 루트입니다. |
| [참조](./jdbc/reference/index.md) | 인터페이스, 클래스 및 멤버입니다. |
| [JDBC SQL 드라이버 프로그래밍 가이드](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 로고][image-ref-340-node] Node.js

Node.js를 사용하여 Windows, Linux 또는 Mac에서 SQL Server에 연결할 수 있습니다. Node.js 설명서의 루트는 [여기](./node-js/index.md)입니다.

SQL Server용 Node.js 연결 드라이버는 JavaScript에서 구현됩니다. 이 드라이버는 모든 최신 버전의 SQL Server에서 지원되는 TDS 프로토콜을 사용합니다. 드라이버는 오픈소스 프로젝트이며 [Github에서 제공](https://tediousjs.github.io/tedious/)됩니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Node.js를 사용하여 SQL에 연결하는 개념 증명](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | SQL Server에 연결하고 쿼리를 실행하기 위한 기본 기능 소스 코드입니다. |
| [Azure SQL Database: Node.js를 사용하여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 클라우드 기반 Azure SQL Database의 예제입니다. |
| [macOS에서 SQL Server를 사용하는 Node.js 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C++용 ODBC 

![ODBC 로고][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

ODBC(Open Database Connectivity)는 .NET Framework보다 앞서 1990년에 개발되었습니다. ODBC는 특정 데이터베이스 시스템 및 운영 체제와 독립적으로 설계되었습니다.

수많은 ODBC 드라이버가 Microsoft 내부 및 외부 그룹에 의해 생성되고 릴리스되었습니다. 드라이버 범위에는 몇 가지 클라이언트 프로그래밍 언어가 포함됩니다. 데이터 대상 목록이 SQL Server보다 훨씬 광범위합니다.

일부 다른 연결 드라이버는 내부적으로 ODBC를 사용합니다.

#### <a name="code-example"></a>코드 예제

- [C++ 코드 예제, ODBC 사용](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>설명서 개요

이 섹션의 ODBC 관련 내용은 C++에서 SQL Server 또는 Azure SQL Database에 액세스하는 방법에 중점을 두고 있습니다. 다음 표에서는 주요 ODBC 설명서를 개략적으로 설명합니다.


| 영역 | 하위 영역 | Description |
| :--- | :------ | :---------- |
| [C++용 ODBC](./odbc/index.md) | 설명서의 루트입니다. |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | Linux 또는 MacOS 운영 체제에서 ODBC를 사용하는 방법입니다. |
| [Windows](./odbc/windows/index.md)     | &nbsp; | Windows 운영 체제에서 ODBC를 사용하는 방법입니다. |
| [관리](../odbc/admin/index.md) | &nbsp; | ODBC 데이터 원본을 관리하기 위한 관리 도구에 대한 설명입니다. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Microsoft에서 만들고 제공하는 다양한 ODBC 드라이버에 대한 설명입니다. |
| [개념 및 참조](../odbc/reference/index.md) | &nbsp; | 기존 참조 이외에 ODBC 인터페이스에 대한 개념 정보입니다. |
| &nbsp; " | [부록](../odbc/reference/appendixes/index.md)    | 상태 전환 테이블, ODBC 커서 라이브러리 등에 대한 설명입니다. |
| &nbsp; " | [앱 개발](../odbc/reference/develop-app/index.md)  | 함수, 핸들 등에 대한 설명입니다. |
| &nbsp; " | [드라이버 개발](../odbc/reference/develop-driver/index.md) | 특수 데이터 원본이 있는 경우 자체 ODBC 드라이버를 개발하는 방법입니다. |
| &nbsp; " | [설치](../odbc/reference/install/index.md) | ODBC 설치, 하위 키 등에 대한 설명입니다. |
| &nbsp; " | [구문](../odbc/reference/syntax/index.md)   | 설치, 설치 프로그램, 변환 및 데이터 액세스용 API에 대한 설명입니다. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 로고][image-ref-360-php] PHP

PHP를 사용하여 SQL Server와 상호 작용할 수 있습니다. PHP 설명서의 루트는 [여기](./php/index.md)입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [PHP를 사용하여 SQL에 연결하는 개념 증명](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | SQL Server에 연결하고 쿼리하는 데 초점을 맞춘 소형 코드 예제입니다. |
| [PHP를 사용하여 탄력적으로 SQL에 연결](./php/step-4-connect-resiliently-to-sql-with-php.md) | 재시도 논리 코드 예제입니다(인터넷 및 클라우드를 통한 연결에서 간헐적으로 연결 손실이 발생할 수 있기 때문). |
| [Azure SQL Database: PHP를 사용하여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL Database 예제입니다. |
| [RHEL에서 SQL Server를 사용하는 PHP 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 로고][image-ref-370-python] Python


Python을 사용하여 SQL Server와 상호 작용할 수 있습니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Python - pyodbc를 사용하여 SQL에 연결하는 개념 증명](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | SQL Server에 연결하고 쿼리하는 데 초점을 맞춘 소형 코드 예제입니다. |
| [Azure SQL Database: Python을 사용하여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL Database 예제입니다. |
| [SLES에서 SQL Server를 사용하는 PHP 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>문서화

| 영역 | Description |
| :--- | :---------- |
| [Python에서 SQL Server](./python/index.md) | 설명서의 루트입니다. |
| [pymssql 드라이버](./python/pymssql/index.md) | Microsoft는 pymssql 드라이버를 유지 관리하거나 테스트하지 않습니다.<br /><br />pymssql 연결 드라이버는 Python 프로그램에서 사용할 수 있는 간단한 SQL 데이터베이스 인터페이스입니다. Pymssql은 FreeTDS를 기반으로 하여 Microsoft SQL Server에 대한 Python DB-API(PEP-249) 인터페이스를 제공합니다. |
| [pyodbc 드라이버](./python/pyodbc/index.md)   | pyodbc 연결 드라이버는 ODBC 데이터베이스에 간편하게 액세스할 수 있는 오픈 소스 Python 모듈입니다. DB API 2.0 사양을 구현하지만 Python적 편의를 위해 압축됩니다. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 로고][image-ref-380-ruby] Ruby

Ruby를 사용하여 SQL Server와 상호 작용할 수 있습니다. Ruby 설명서의 루트는 [여기](./ruby/index.md)입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Ruby를 사용하여 SQL에 연결하는 개념 증명](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | SQL Server에 연결하고 쿼리하는 데 초점을 맞춘 소형 코드 예제입니다. |
| [Azure SQL Database: Ruby를 사용하여 쿼리](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL Database 예제입니다. |
| [MacOS에서 SQL Server를 사용하는 Ruby 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 구성 정보입니다. 코드 예제도 제공됩니다. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-development"></a>[앱 빌드 웹 사이트, SQL 클라이언트 개발](https://www.microsoft.com/sql-server/developer-get-started/)


[*앱 빌드*](https://www.microsoft.com/sql-server/developer-get-started/) 웹 페이지에서 SQL Server에 연결하기 위한 다수의 프로그래밍 언어 목록 중에서 선택할 수 있습니다. 또한 클라이언트 프로그램은 다양한 운영 체제를 실행할 수 있습니다.

*앱 빌드*는 처음 시작하는 개발자를 위해 단순성과 완전성을 강조합니다. 각 단계에서는 다음 작업을 설명합니다.

1. Microsoft SQL Server 설치 방법
2. 도구 및 드라이버를 다운로드하고 설치하는 방법입니다.
3. 선택한 운영 체제에 맞게 필요한 구성을 만드는 방법입니다.
4. 제공된 소스 코드를 컴파일하는 방법입니다.
5. 프로그램을 실행합니다.

다음은 웹 사이트에서 제공되는 세부 정보의 대략적인 개요입니다.

#### <a name="java-on-ubuntu"></a>Ubuntu에서의 Java:

1. 환경 설정
    - 1\.1 단계 SQL Server 설치
    - 1\.2 단계 Java 설치
    - 1\.3 단계 JDK(Java Development Kit) 설치
    - 1\.4 단계 Maven 설치
2. SQL Server를 사용하여 Java 애플리케이션 만들기
    - 2\.1 단계 SQL Server에 연결하고 쿼리를 실행하는 Java 앱 만들기
    - 2\.2 단계 인기 프레임워크 Hibernate를 사용하여 SQL Server에 연결하는 Java 앱 만들기
3. Java 애플리케이션을 최대 100배 빠르게 만들기
    - 3\.1 단계 Columnstore 인덱스를 시연하는 Java 앱 만들기

#### <a name="python-on-windows"></a>Windows에서의 Python:

1. 환경 설정
    - 1\.1 단계 SQL Server 설치
    - 1\.2 단계 Python 설치
    - 1\.3 단계 SQL Server용 ODBC 드라이버 및 SQL 명령줄 유틸리티 설치
2. SQL Server를 사용하여 Python 애플리케이션 만들기
    - 2\.1 단계 SQL Server용 Python 드라이버 설치
    - 2\.2 단계 애플리케이션용 데이터베이스 만들기
    - 2\.3 단계 SQL Server에 연결하고 쿼리를 실행하는 Python 앱 만들기
3. Python 앱을 최대 100배 빠르게 만들기
    - 3\.1 단계 sqlcmd를 사용하여 500만 개 데이터로 새 테이블 만들기
    - 3\.2 단계 이 테이블을 쿼리하고 소요 시간을 측정 하는 Python 앱 만들기
    - 3\.3 단계 쿼리를 실행하는 데 걸리는 시간 측정
    - 3\.4 단계 테이블에 columnstore 인덱스 추가
    - 3\.5 단계 columnstore 인덱스를 사용하여 쿼리를 실행하는 데 걸리는 시간 측정

다음 스크린샷은 SQL 개발 설명서 웹 사이트의 모습을 보여 줍니다.

#### <a name="choose-a-language"></a>언어 선택

![SQL Dev 웹 사이트, 시작하기][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>운영 체제 선택:

![SQL Dev 웹 사이트, Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>기타 개발


이 섹션에서는 다른 개발 옵션에 대한 링크를 제공합니다. 여기에는 일반적으로 Azure 개발에도 동일한 언어를 사용하는 것이 포함됩니다. 정보는 Azure SQL Database 및 Microsoft SQL Server만을 대상으로 하지 않습니다.

#### <a name="developer-hub-for-azure"></a>Azure 개발자 허브

- [Azure 개발자 허브](https://docs.microsoft.com/azure/)
- [.NET 개발자용 Azure](https://docs.microsoft.com/dotnet/azure/)
- [Java 개발자용 Azure](https://docs.microsoft.com/java/azure/)
- [Node.js 개발자용 Azure](https://docs.microsoft.com/nodejs/azure/)
- [Python 개발자용 Azure](https://docs.microsoft.com/python/azure/)
- [Azure에서 PHP 웹앱 만들기](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>기타 언어

- [Windows에서 SQL Server를 사용하여 Go 앱 만들기](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

