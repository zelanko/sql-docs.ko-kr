---
title: Microsoft SQL Database에 대 한 연결 라이브러리 | Microsoft Docs
description: 다양 한 클라이언트 프로그래밍 언어에서 Microsoft SQL Server 및 Azure SQL Database에 대 한 연결을 가능 하 게 하는 모듈에 대 한 다운로드 링크를 제공 합니다.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632811"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 데이터베이스용 연결 모듈

이 문서에서는 클라이언트 프로그램에서 [Microsoft SQL Server](../relational-databases/database-features.md)와 상호 작용 하는 데 사용할 수 있는 연결 모듈 또는 *드라이버* 와 클라우드 [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)의 해당 쌍에 대 한 다운로드 링크를 제공 합니다. 드라이버는 다음과 같은 운영 체제에서 실행 되는 다양 한 프로그래밍 언어에 사용할 수 있습니다.

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP-관계형 불일치

*관계형*: OOP (개체 지향 프로그래밍) 언어를 사용 하 여 작성 된 클라이언트 프로그램은 종종 쿼리 된 데이터를 개체 지향 보다 더 관계형 형식으로 반환 하는 SQL 드라이버를 사용 합니다. C#ADO.NET를 사용 하는 것은 한 가지 예입니다. OOP 관계형 형식 불일치는 때때로 OOP 코드를 작성 하 고 이해 하기 어렵게 만듭니다.

*ORM*: 다른 드라이버나 프레임 워크는 불일치를 방지 하 여 쿼리 된 데이터를 OOP 형식으로 반환 합니다. 이러한 드라이버는 특정 SQL 테이블의 데이터 열과 일치 하도록 클래스가 정의 되어 있어야 작동 합니다. 그런 다음 드라이버는 ORM ( *개체-관계형 매핑* )을 수행 하 여 쿼리 된 데이터를 클래스의 인스턴스로 반환 합니다. 용 C#EF (Microsoft Entity Framework) 및 Java 용 최대 절전 모드는 두 가지 예제입니다.

현재 문서에서는 이러한 두 가지 종류의 연결 드라이버에 대 한 별도의 섹션을의.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>관계형 액세스용 드라이버


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| 언어 | SQL 드라이버 다운로드 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[Linux-Ubuntu용.NET core](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, MacOS 용](https://www.microsoft.com/net/core#macos)<br />[Windows 용 .NET Core](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 드라이버, 설치 지침](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, 설치 지침](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[ODBC 다운로드](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 드라이버, 설치 지침](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 다운로드 페이지](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 액세스용 드라이버


다음 표에서는 클라이언트 응용 프로그램이 Microsoft SQL 데이터베이스에 연결 하는 데 사용 하는 ORM (개체 관계형 매핑) 프레임 워크의 예를 보여 줍니다.


| 언어 | ORM 드라이버 다운로드 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6gb 이상)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM, Laravel 설치에 포함 되어 있습니다.](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>응용 프로그램 빌드 웹 페이지
[https://aka.ms/sqldev](https://aka.ms/sqldev) *빌드-앱* 웹 페이지의 집합으로 이동 합니다. 웹 페이지에서는 프로그래밍 언어, 운영 체제 및 SQL 연결 드라이버의 다양 한 조합에 대 한 정보를 제공 합니다. 빌드-앱 웹 페이지에서 제공 하는 정보 중에는 다음 항목이 있습니다.

- 언어 + 운영 체제 + 드라이버의 각 조합에 대해 처음부터 시작 하는 방법에 대 한 세부 정보입니다.
    - 최신 SQL 연결 드라이버를 설치 하는 방법에 대 한 지침입니다.
- 다음 각 항목에 대 한 코드 예제는 다음과 같습니다.
    - 개체 관계형 코드 예제입니다.
    - ORM 코드 예제
    - Columnstore 인덱스는 훨씬 빠른 성능을 위해 데모를 수행 합니다.

#### <a name="first-page-of-build-an-app-webpages"></a>응용 프로그램 빌드 웹 페이지의 첫 번째 페이지
![빌드-앱 웹 페이지, 첫 번째 페이지 스크린샷][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Java 용 메뉴-Ubuntu, 앱 빌드 웹 페이지
![빌드-앱 웹 페이지, 메뉴 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>관련 링크
- [Java 및 기타 언어를 사용 하 여 클라우드에서 Azure SQL Database에 연결 하는 코드 예제](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)입니다.

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
