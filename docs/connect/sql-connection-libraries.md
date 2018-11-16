---
title: Microsoft SQL 데이터베이스에 대 한 연결 라이브러리 | Microsoft Docs
description: 다양 한 클라이언트 프로그래밍 언어에서에서 Microsoft SQL Server 및 Azure SQL Database에 연결할 수 있도록 하는 모듈에 대 한 다운로드 링크를 제공 합니다.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 4286a9a1fcc2eff3becd483d658b371bb6452032
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600373"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 데이터베이스에 대 한 연결 모듈

이 문서에서는 연결 모듈에 대 한 다운로드 링크를 제공 하거나 *드라이버* 클라이언트 프로그램 상호 작용에 사용할 수 있는 [Microsoft SQL Server](../relational-databases/database-features.md), 및 클라우드에서 해당 쌍을 사용 하 여 [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/)합니다. 드라이버는 다음 운영 체제에서 실행 되는 프로그래밍 언어의 다양 한 사용할 수 있습니다.

- Linux(Ubuntu)
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP-관계형 일치 하지 않습니다.

*관계형*: 자주 하는 개체 지향 프로그래밍 (OOP) 언어에서 기록 되는 클라이언트 프로그램 개체 지향 보다 더 관계형 형식으로 쿼리 된 데이터를 반환 하는 SQL 드라이버를 사용 합니다. ADO.NET을 사용 하 여 C#은 하나의 예제입니다. OOP 관계형 형식 불일치 경우에 따라 어려워집니다 OOP 코드를 작성 하 고 이해 합니다.

*ORM*: 다른 드라이버 또는 프레임 워크 불일치를 방지 하는 OOP 형식으로 쿼리 된 데이터를 반환 합니다. 이러한 드라이버는 클래스는 특정 SQL 테이블의 데이터 열에 맞게 정의 된 예상 하 여 작동 합니다. 다음 드라이버를 수행 합니다 *개체-관계형 매핑* (ORM) 클래스의 인스턴스로 쿼리 된 데이터를 반환할 합니다. Microsoft의 EF (Entity Framework) C# 및 Java에 대 한 최대 절전 모드는 두 가지 예입니다.

현재 문서는 이러한 두 종류의 연결 드라이버를 별도 섹션 하기가 합니다.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>드라이버에 대 한 관계형 액세스


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| 언어 | SQL driver 다운로드 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br /><br />[Linux Ubuntu 용.NET core](https://www.microsoft.com/net/core#Ubuntu)<br />[MacOS 용.NET core](https://www.microsoft.com/net/core#macos)<br />[Windows에 대 한.NET core](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 드라이버를 설치 지침](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, 설치 지침](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[ODBC를 다운로드 합니다.](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 드라이버 설치 지침](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 다운로드 페이지](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 액세스에 대 한 드라이버


다음 표에서 Microsoft SQL 데이터베이스에 연결 하려면 클라이언트 응용 프로그램을 사용 하는 개체 관계형 매핑 (ORM) 프레임 워크의 예를 나열 합니다.


| 언어 | ORM 드라이버 다운로드 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x 이상)](https://docs.microsoft.com/ef/) |
| Java | [ORM 최대 절전 모드로 전환](https://hibernate.org/orm)|
| PHP | [Eloquent ORM, Laravel 설치에 포함](https://laravel.com/docs/) |
| Node.js | [ORM sequelize](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>웹 앱을 빌드 페이지
[https://aka.ms/sqldev](https://aka.ms/sqldev) 집합이 안내 *앱을 빌드* 웹 페이지입니다. 웹 페이지 프로그래밍 언어, 운영 체제 및 SQL 연결 드라이버의 다양 한 조합에 대 한 정보를 제공 합니다. 웹 앱을 빌드 페이지에서 제공한 정보는 다음 항목이 같습니다.

- 운영 체제, 언어 + 드라이버의 각 조합에 대해 처음부터 시작 하는 방법에 대 한 세부 정보입니다.
    - 최신 SQL 연결 드라이버를 설치 하기 위한 지침입니다.
- 다음 항목 중 각각에 대 한 코드 예제:
    - 개체-관계형 코드 예제입니다.
    - ORM 코드 예제
    - 훨씬 빠른 성능을 위해 Columnstore 인덱스 데모입니다.

#### <a name="first-page-of-build-an-app-webpages"></a>앱을 빌드 웹 페이지의 첫 번째 페이지
![웹 페이지 앱을 빌드, 첫 번째 페이지 스크린샷][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Java-빌드-앱을 웹 페이지의 Ubuntu에 대 한 메뉴
![웹 페이지 앱을 빌드 메뉴 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>관련 링크
- [코드, Java 및 기타 언어를 사용 하 여 클라우드에서 Azure SQL Database에 연결 하기 위한 예제](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)합니다.

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
