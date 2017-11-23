---
title: "SQL 클라이언트 프로그래밍에 대 한 홈 페이지 | Microsoft Docs"
description: "다운로드 및 언어와 SQL Server 나 Azure SQL 데이터베이스에 연결 하기 위한 운영 체제의 다양 한 조합에 대 한 설명서에 대 한 주석이 추가 된 링크가 있는 허브 페이지입니다."
author: MightyPen
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: connect
ms.suite: sql
ms.custom: 
ms.technology: drivers
ms.topic: article
ms.reviewer: meetb
ms.author: genemi
ms.workload: Inactive
ms.openlocfilehash: dbbb2e06521b364de7d8de1b32869380fbc2772a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2017
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server를 프로그래밍 하는 클라이언트에 대 한 홈 페이지


클라이언트 및 Microsoft SQL Server와 클라우드의 Azure SQL 데이터베이스 상호 작용을 프로그래밍 하는 방법에 대 한 우리의 홈 페이지를 시작 합니다. 이 문서에서는 다음과 같은 내용을 다룹니다.

- 나열 하 고 사용 가능한 언어 및 드라이버 조합에 설명 합니다.
    - Linux (Ubuntu 및 기타), MacOS 등 및 Windows 운영 체제에 대 한 정보가 제공 됩니다.
- 각 조합에 대 한 자세한 설명서에 대 한 링크를 제공합니다.
- 적절 한 영역 및 특정 언어에 대 한 계층적 문서의 하위 영역을 표시 합니다.


#### <a name="azure-sql-database"></a>Azure SQL 데이터베이스

지정된 된 언어에서 SQL Server에 연결 하는 코드는 Azure SQL 데이터베이스에 연결 하기 위한 코드에 거의 동일 합니다.

Azure SQL 데이터베이스에 연결 하기 위한 연결 문자열에 대 한 세부 정보를 참조 하세요.

- [.NET Core (C#)를 사용 하 여 Azure SQL 데이터베이스 쿼리](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core)합니다.
- 다른 언어에 대 한 내용의 테이블에서 이전 문서 근처에 있는 다른 Azure SQL 데이터베이스입니다. 예를 들어 참조 [Azure SQL 데이터베이스 쿼리를 사용 하 여 PHP](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)합니다.


#### <a name="build-an-app-webpages"></a>웹 페이지 응용 프로그램 빌드

우리의 *응용 프로그램 빌드* 웹 페이지의 다른 형식에서 구성 정보와 함께 코드 예제를 제공 합니다. 자세한 내용은이 문서의 뒷부분에 나오는 참조는 [라는 섹션 *웹 사이트 응용 프로그램 빌드*](#an-204-aka-ms-sqldev)합니다.



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>언어 및 클라이언트 프로그램에 대 한 드라이버


다음 표에서 각 언어 이미지는 언어를 사용 하 여 SQL Server와 함께 하는 방법에 대 한 세부 사항에 링크 합니다. 각 링크는이 문서의 뒷부분에 나오는 섹션으로 이동합니다.

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp;[ ![C# 로고][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp;[ ![ORM Entity Framework는.NET Framework의][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp;[ ![Java 로고][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp;[ ![Node.js 로고][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu) | &nbsp;[ ![PHP 로고][image-ref-360-php]](#an-170-php-docu) |
| &nbsp;[ ![Python 로고][image-ref-370-python]](#an-180-python-docu) | &nbsp;[ ![Ruby 로고][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>다운로드 및 설치

다음 문서를 다운로드에 할당 되 고 프로그래밍 언어에서 사용 하기 위해 다양 한 SQL 연결 드라이버를 설치 합니다.

- [SQL Server 드라이버](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 로고][image-ref-320-csharp] ADO.NET을 사용 하 여 C#

C# 및 Visual Basic의 경우.NET 관리 되는 언어는 ADO.NET의 가장 일반적인 사용자입니다. *ADO.NET* .NET Framework 클래스의 하위 집합에 대 한 일반 이름입니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [ADO.NET을 사용 하 여 SQL에 연결 하는 개념 증명](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | 에 연결 하 고 SQL Server 쿼리 작은 코드 예제를 사용 하는 데 사용 됩니다. |
| [탄력적 ado.net SQL에 연결](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | 연결의 연결이 끊기지 발생할 수 있으므로 코드 예제에서는 논리를 다시 시도 하십시오.<br /><br />다시 시도 논리 연결 유지 관리 되는 인터넷을 통해 클라우드 데이터베이스로 같은 Azure SQL 데이터베이스에도 적용 됩니다. |
| [연결 및 쿼리를 C# 프로그램을 만들려면 macOS/Windows/Linux에서.NET Core를 사용 하는 방법의 데모를 azure SQL 데이터베이스:](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL 데이터베이스 예입니다. |
| [빌드-프로그램-응용 프로그램: C#, ADO.NET, Windows](http://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

|||
| :-- | :-- |
| [ADO.NET을 사용 하 여 C#](./ado-net/index.md)| 설명서의 루트입니다. |
| [Namespace: System.Data](http://docs.microsoft.com/dotnet/api/system.data) | ADO.NET에 대 한 사용 되는 클래스의 집합입니다. |
| [Namespace: System.Data.SqlClient](http://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 집합 ADO.NET 센터 직접 가장 되는 클래스입니다. |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![Entity Framework 로고][image-ref-333-ef] Entity Framework (EF)를 C&#x23;

Entity Framework (EF) 개체-관계형 매핑 ORM ()를 제공합니다. ORM 관계형 SQL 데이터베이스에서 검색 된 데이터를 조작 하기 위한 개체 지향 프로그래밍 OOP () 소스 코드 쉽게 있습니다.

EF 다음 기술과 함께 직접 또는 간접 관계에 있습니다.

- .NET Framework
- [LINQ to SQL](http://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/), 또는 [LINQ to Entities](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 향상 된 구문은 언어와 같은  **=>**  C#에서 연산자.
- SQL 데이터베이스의 테이블에 매핑되는 클래스에 대 한 소스 코드를 생성 하는 편리한 프로그램. 예를 들어, [EdmGen.exe](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)합니다.


#### <a name="original-ef-and-new-ef"></a>원래 EF 및 새 EF

[Entity Framework 용 시작 페이지](http://docs.microsoft.com/ef/) EF 다음과 비슷한 설명과 함께 소개 합니다.

- Entity Framework는.NET 개발자가.NET 개체를 사용 하 여 데이터베이스를 사용할 수 있도록 개체 관계형 매퍼 (O/RM). 대부분의 개발자는 일반적으로 작성 해야 하는 데이터 액세스 소스 코드에 대 한 필요가 없습니다.

*Entity Framework* 두 개의 별도 소스 코드 분기에서 공유 이름입니다. 이전, EF 분기 하나 이며 해당 소스 코드의 한 공개적인 유지 관리할 수 이제 있습니다. 다른 EF 새로운 기능입니다. 다음은 두 개의 EFs에 대 한 설명입니다.

|     |     |
| :-- | :-- |
| [EF 6.x](http://docs.microsoft.com/ef/ef6/) | Microsoft는 EF 2008 년 8 월에에서 처음 릴리스 합니다. 2015 년 3 월 Microsoft 발표 하 EF 6.x 개발할 때 Microsoft는 최종 버전 이었습니다. Microsoft 공용 도메인에 소스 코드를 릴리스 했습니다.<br /><br />처음 EF가.NET Framework의 일부입니다. 하지만 EF 6.x.NET Framework에서 제거 되었습니다.<br /><br />[Github 리포지토리에 EF 6.x 소스 코드 *aspnet/EntityFramework6*](http://github.com/aspnet/EntityFramework6) |
| [EF 코어](http://docs.microsoft.com/ef/core/) | Microsoft에서는 2016 년 6 월 새로 개발된 EF 코어를 릴리스 했습니다. EF 코어 우수한 유연성과 이동성 위해 설계 되었습니다. EF 코어도 Microsoft Windows 이외의 운영 체제에서 실행할 수 있습니다. 및 EF 코어는 Microsoft SQL Server 이외의 데이터베이스와 다른 관계형 데이터베이스와 상호 작용할 수 있습니다.<br /><br />**C&#x23; 코드 예:**<br />[Entity Framework Core 시작 하기](https://docs.microsoft.com/ef/core/get-started/index)<br />[기존 데이터베이스와.NET Framework에서 EF Core 시작 하기](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 및 관련된 기술에는 강력한 되며 전체 영역 마스터 하려는 개발자에 대 한 배울 있습니다.

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 로고][image-ref-330-java] Java 및 JDBC

Microsoft은 SQL Server와 함께 (또는 과정의 Azure SQL 데이터베이스) 사용 하기 위해 데이터베이스 JDBC (Java Connectivity) 드라이버를 제공합니다. Type 4 JDBC 드라이버 이며 표준 JDBC 응용 프로그램 인터페이스 (Api)를 통해 데이터베이스 연결을 제공 합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [코드 예제](./jdbc/code-samples/index.md) | 데이터 형식, 결과 집합 및 큰 데이터에 대 한 방법을 설명 하는 코드 예제입니다. |
| [연결 URL 샘플](./jdbc/connection-url-sample.md) | SQL Server에 연결할 연결 URL을 사용 하는 방법을 설명 합니다. 사용 하 여 SQL 문을 사용 하 여 데이터를 검색 합니다. |
| [데이터 원본 샘플](./jdbc/data-source-sample.md) | SQL Server에 연결할 데이터 원본을 사용 하는 방법에 설명 합니다. 다음 저장된 프로시저를 사용 하 여 데이터를 검색 합니다. |
| [Java를 사용 하 여 Azure SQL 데이터베이스 쿼리](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL 데이터베이스 예입니다. |
| [Ubuntu에서 SQL Server를 사용 하 여 Java 응용 프로그램 만들기](http://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

JDBC 설명서는 다음과 같은 주요 영역에 포함 됩니다.

|||
| :-- | :-- |
| [Java Database Connectivity (JDBC)](./jdbc/index.md) | JDBC 설명서의 루트입니다. |
| [참조](./jdbc/reference/index.md) | 인터페이스, 클래스 및 멤버를 선택 합니다. |
| [JDBC SQL 드라이버 프로그래밍 가이드](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 로고][image-ref-340-node] Node.js

Node.js와 함께 연결할 수 있습니다 SQL Server에서 Windows, Linux 또는 Mac. Node.js 설명서 루트가 [여기](./node-js/index.md)합니다.

SQL Server 용 Node.js 연결 드라이버는 JavaScript에서 구현 됩니다. 드라이버는 모든 최신 버전의 SQL Server에서 지원 되는 TDS 프로토콜을 사용 합니다. 드라이버는 오픈 소스 프로젝트 [Github에서 사용할 수 있는](http://tediousjs.github.io/tedious/)합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Node.js를 사용 하 여 SQL에 연결 하는 개념 증명](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 기본적인 소스 SQL Server에 연결 하는 쿼리를 실행 하기 위한 코드입니다. |
| [Azure SQL 데이터베이스: 쿼리를 사용 하 여 Node.js](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 클라우드에서 Azure SQL 데이터베이스에 대 한 예제를 제공 합니다. |
| [Node.js 앱 macOS에서 SQL Server를 사용 하도록 만들기](http://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C + +에 대 한 ODBC 

![ODBC 로고][image-ref-350-odbc]

개방형 데이터베이스 연결 (ODBC) 1990에서 개발한 및.NET Framework를 발생 합니다. ODBC는 별개의 운영 체제 및 모든 특정 데이터베이스 시스템의 독립적인 되도록 설계 되었습니다.

수 년에 걸쳐 다양 한 ODBC 드라이버 만들어져서 그룹 내에서 Microsoft 외부에서 해제 합니다. 여러 클라이언트 프로그래밍 언어를 포함 하는 드라이버의 범위. 데이터 대상 목록은 SQL Server를 훨씬 벗어납니다.

일부 연결 드라이버는 ODBC를 내부적으로 사용 합니다.

#### <a name="code-example"></a>코드 예제

- [C + + 코드 예제에서는 ODBC를 사용 하 여](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>문서 개요

이 섹션에서는 ODBC 콘텐츠 c + +에서 SQL Server 또는 Azure SQL 데이터베이스 액세스에 중점을 둡니다. 다음 표에서 ODBC에 대 한 주요 설명서의 대략적인 개요를 나열합니다.


| 영역 | 하위 영역 | Description |
| :--- | :------ | :---------- |
| [C + +에 대 한 ODBC](./odbc/index.md) | 설명서의 루트입니다. |
| [Linux 및 Mac](./odbc/linux-mac/index.md) | &nbsp; | Linux 또는 MacOS 운영 체제에서 ODBC를 사용 하는 방법에 대 한 정보입니다. |
| [창](./odbc/windows/index.md)     | &nbsp; | Windows 운영 체제에서 ODBC를 사용 하는 방법에 대 한 정보입니다. |
| [관리](../odbc/admin/index.md) | &nbsp; | ODBC 데이터 원본 관리를 위한 관리 도구입니다. |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 생성 되 고 Microsoft에서 제공 되는 다양 한 ODBC 드라이버 |
| [개념 및 참조](../odbc/reference/index.md) | &nbsp; | 기존 참조 외에도 ODBC 인터페이스에 대 한 개념 정보입니다. |
| &nbsp; " | [부록](../odbc/reference/appendixes/index.md)    | 상태 전환 테이블, ODBC 커서 라이브러리 등입니다. |
| &nbsp; " | [응용 프로그램 개발](../odbc/reference/develop-app/index.md)  | 함수, 핸들 및 등입니다. |
| &nbsp; " | [드라이버를 개발 합니다.](../odbc/reference/develop-driver/index.md) | 특수 한 데이터 원본이 있는 경우 사용자 고유의 ODBC 드라이버를 개발 하는 방법입니다. |
| &nbsp; " | [설치](../odbc/reference/install/index.md) | ODBC 설치를 더 합니다. |
| &nbsp; " | [구문](../odbc/reference/syntax/index.md)   | 설치, 설치 관리자, 변환 및 데이터 액세스 Api입니다. |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 로고][image-ref-360-php] PHP

SQL Server와 상호 작용할 수 PHP를 사용할 수 있습니다. Node.js 설명서 루트가 [여기](./php/index.md)합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [PHP를 사용 하 여 SQL에 연결 하는 개념 증명](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 에 연결 하 고 SQL Server 쿼리 작은 코드 예제를 사용 하는 데 사용 됩니다. |
| [Php SQL 탄력적 연결](./php/step-4-connect-resiliently-to-sql-with-php.md) | 인터넷 및 클라우드를 통해 연결 연결이 손실 시점에 부딪힐 수 때문에 코드 예제에서는 논리를 다시 시도 하십시오. |
| [Azure SQL 데이터베이스: 쿼리 하는 PHP 사용 하 여](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL 데이터베이스 예입니다. |
| [RHEL에서 SQL Server를 사용 하는 PHP 응용 프로그램 만들기](http://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 로고][image-ref-370-python] Python


SQL Server와 상호 작용할 수 Python을 사용할 수 있습니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Python pyodbc를 사용 하 여 SQL에 연결 하는 개념 증명](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 에 연결 하 고 SQL Server 쿼리 작은 코드 예제를 사용 하는 데 사용 됩니다. |
| [Azure SQL 데이터베이스: 쿼리를 사용 하 여 Python](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL 데이터베이스 예입니다. |
| [SLES에서 SQL Server를 사용 하는 PHP 응용 프로그램 만들기](http://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |

#### <a name="documentation"></a>설명서

| 영역 | Description |
| :--- | :---------- |
| [SQL Server에 대 한 Python](./python/index.md) | 설명서의 루트입니다. |
| [pymssql 드라이버](./python/pymssql/index.md) | Microsoft는 유지 관리 하거나 pymssql 드라이버를 테스트 하지 않습니다.<br /><br />Pymssql 연결 드라이버는 Python 프로그램에서 사용할 SQL 데이터베이스에 간단한 인터페이스입니다. Pymssql은 Microsoft SQL Server에 Python DB API (PEP 249) 인터페이스를 제공 하는 FreeTDS을 기반으로 구축 합니다. |
| [pyodbc 드라이버](./python/pyodbc/index.md)   | Pyodbc 연결 드라이버는 ODBC 데이터베이스에 액세스를 간소화 하는 오픈 소스 Python 모듈입니다. 이 API 2.0 DB 사양을 구현 하지만 더 많은 Pythonic 시간으로 압축 합니다. |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 로고][image-ref-380-ruby] Ruby

Ruby SQL 서버와 상호 작용에 사용할 수 있습니다. Ruby 설명서 루트가 [여기](./ruby/index.md)합니다.

#### <a name="code-examples"></a>코드 예제

|||
| :-- | :-- |
| [Sql Ruby로 연결 된 개념 증명](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 에 연결 하 고 SQL Server 쿼리 작은 코드 예제를 사용 하는 데 사용 됩니다. |
| [Azure SQL 데이터베이스: 쿼리를 사용 하 여 Ruby](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL 데이터베이스 예입니다. |
| [MacOS에서 SQL Server를 사용 하도록 Ruby 앱 만들기](http://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 코드 예제와 함께 구성 정보입니다. |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpwwwmicrosoftcomsql-serverdeveloper-get-started"></a>[SQL 클라이언트 개발에 대 한 응용 프로그램 빌드는 웹 사이트](http://www.microsoft.com/sql-server/developer-get-started/)


우리의 [ *응용 프로그램 빌드* ](https://www.microsoft.com/sql-server/developer-get-started/) 웹 페이지의 SQL Server에 연결 하기 위한 언어 프로그래밍 긴 목록에서 선택할 수 있습니다. 및 클라이언트 프로그램에서 다양 한 운영 체제를 실행할 수 있습니다.

*응용 프로그램 빌드* 개발자에 게 방금 시작 간소 성 및 완결성을 강조 합니다. 단계는 다음과 같은 작업에 설명 합니다.

1. Microsoft SQL Server를 설치 하는 방법
2. 다운로드 하 고 도구 및 드라이버를 설치 하는 방법.
3. 선택한 운영 체제에 따라 필요한 모든 구성을 확인 하는 방법.
4. 제공 된 소스 코드를 컴파일하는 방법입니다.
5. 프로그램을 실행 하는 방법.

다음은 몇 가지 대략적인 개요 웹 사이트에서 제공 된 세부 정보:

#### <a name="java-on-ubuntu"></a>Java ubuntu:

1. 환 결 설정
    - SQL Server를 설치 하는 단계 1.1
    - 단계 1.2 설치 Java
    - 1.3 단계 설치 Java Development Kit (JDK)
    - 1.4 단계 설치 Maven
2. SQL Server와 Java 응용 프로그램 만들기
    - 단계 2.1 SQL Server에 연결 하 고 쿼리를 실행 하는 Java 응용 프로그램 만들기
    - 단계 2.2는 인기 있는 프레임 워크의 최대 절전 모드를 사용 하 여 SQL Server에 연결 하는 Java 앱 만들기
3. 최대 100 배 Java 응용 프로그램을 더 빠르게 만들
    - Columnstore 인덱스를 보여 주기 위해 Java 앱 3.1 단계 만들기

#### <a name="python-on-windows"></a>Windows에서 Python:

1. 환 결 설정
    - SQL Server를 설치 하는 단계 1.1
    - 단계 1.2 설치 Python
    - SQL Server에 대 한 ODBC 드라이버와 SQL 명령줄 유틸리티를 설치 하는 백업
2. SQL Server와 함께 Python 응용 프로그램 만들기
    - SQL Server에 대 한 Python 드라이버를 설치 하는 단계 2.1
    - 2.2 단계 응용 프로그램에 대 한 데이터베이스 만들기
    - 단계 2.3 SQL Server에 연결 하 고 쿼리를 실행 하는 Python 응용 프로그램 만들기
3. 최대 100 배 Python 응용 프로그램을 더 빠르게 만들
    - 3.1 단계 5 백만 sqlcmd를 사용 하 여 새 테이블 만들기
    - 단계 3.2이이 테이블을 쿼리 하는 데 걸리는 시간을 측정 하는 Python 응용 프로그램 만들기
    - 쿼리를 실행 하는 데 걸리는 시간을 측정 단계 3.3
    - 3.4 단계 추가 사용자 테이블에 columnstore 인덱스
    - 단계 3.5 columnstore 인덱스가 포함 된 쿼리를 실행 하는 데 걸리는 시간 측정

다음 스크린샷에서 SQL 개발 설명서 웹 사이트의 모양을의 아이디어를 제공 합니다.

#### <a name="choose-a-language"></a>언어 선택:

![SQL 개발자 웹 사이트를 시작 하려면][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>운영 체제를 선택 합니다.

![Java Ubuntu SQL 개발자 웹 사이트][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>다른 개발


이 섹션에서는 다른 개발 옵션에 대 한 링크를 제공 합니다. 여기에 Azure 개발을 위한 일반적이 동일한 언어를 사용 합니다. 정보 되 면 방금 Azure SQL 데이터베이스 및 Microsoft SQL Server를 대상으로 합니다.

#### <a name="developer-hub-for-azure"></a>Azure에 대 한 개발자 허브

- [Azure에 대 한 개발자 허브](http://docs.microsoft.com/azure/)
- [.NET 개발자를 위한 azure](http://docs.microsoft.com/dotnet/azure/)
- [Java 개발자를 위한 azure](http://docs.microsoft.com/java/azure/)
- [Node.js 개발자를 위한 azure](http://docs.microsoft.com/nodejs/azure/)
- [Python 개발자를 위한 azure](http://docs.microsoft.com/python/azure/)
- [Azure에서 PHP 웹 응용 프로그램 만들기](http://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>다른 언어

- [SQL Server를 사용 하 여 Windows에서 Go 앱 만들기](http://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-310-ado-net]: ./media/homepage-sql-connection-drivers/gm-ado-net-an51.png
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

