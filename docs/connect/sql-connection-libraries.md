---
title: "Microsoft SQL 데이터베이스에 대 한 연결 라이브러리 | Microsoft Docs"
description: "다양 한 클라이언트 프로그래밍 언어의 Microsoft SQL Server 및 Azure SQL 데이터베이스에 연결 하는 모듈에 대 한 다운로드 링크를 제공 합니다."
author: MightyPen
ms.service: 
ms.component: connect
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.technology: dbe-data-tier-apps
ms.custom: 
ms.workload: data-management
ms.topic: article
ms.date: 08/09/2017
ms.author: genemi
ms.openlocfilehash: 9c85a5e40ca7d3b6e35cdb09fc4becbe5c9c65c3
ms.sourcegitcommit: 1a3584a60c12521ba5b4b12a18d8cb32b1f2d555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 데이터베이스에 대 한 연결 모듈

이 문서에서는 연결 모듈에 대 한 다운로드 링크를 제공 하거나 *드라이버* 클라이언트 프로그램 상호 작용에 사용할 수 있는 [Microsoft SQL Server](../index.md), 클라우드에서로 해당 이중 가진 [Azure SQL 데이터베이스](http://docs.microsoft.com/azure/sql-database/)합니다. 드라이버는 다양 한 다음 운영 체제에서 실행 되는 프로그래밍 언어를 사용할 수 있습니다.

- Linux (Ubuntu)
- MacOS
- 창


#### <a name="oop-to-relational-mismatch"></a>OOP-관계형 일치 하지 않습니다.

*관계형*: 클라이언트 프로그램에 종종 프로그래밍 (OOP) 개체 지향 언어에서 작성 된 개체 지향 보다 더 관계형 되는 형식으로 쿼리 된 데이터를 반환 하는 SQL 드라이버를 사용 합니다. ADO.NET을 사용 하 여 C#은 한 예입니다. OOP 관계형 형식 일치 하지 않습니다 때로는 OOP 코드 하기 어렵게 만듭니다 작성 하 고 이해 합니다.

*ORM*: 다른 프레임 워크 또는 드라이버 불일치를 방지 OOP 형식으로 쿼리 된 데이터를 반환 합니다. 이러한 드라이버 클래스 특정 SQL 테이블의 데이터 열에 맞게 정의 된 예상 하 여 작동 합니다. 드라이버 후 수행 하는 *개체-관계형 매핑* ORM ()는 클래스의 인스턴스도 쿼리 된 데이터를 반환 하려면. C#에 대 한 Microsoft의 Entity Framework (EF) 및 Java에 대 한 최대 절전 모드는 두 가지 예입니다.

현재 문서는 이러한 두 종류의 연결 드라이버를 별도 섹션 하기가 합니다.


<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>드라이버에 대 한 관계형 액세스


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  http://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is http://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->


| 언어 | SQL 드라이버를 다운로드 합니다. |
| :------- | :---------------------- |
| C#       | [ADO.NET](http://www.microsoft.com/net/download/)<br /><br />[.NET Core, for Linux-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, for MacOS](https://www.microsoft.com/net/core#macos)<br />[Windows 용.NET core](https://www.microsoft.com/net/core) |
| C++      | [ODBC](http://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server) |
| Java     | [JDBC](http://www.microsoft.com/download/details.aspx?id=55539) |
| Node.js  | [Node.js 드라이버, 설치 지침](http://docs.microsoft.com/sql/connect/node-js/step-1-configure-development-environment-for-node-js-development) |
| PHP      | *운영 체제:*<br /><br />[Windows PHP driver](https://www.microsoft.com/download/details.aspx?id=55642)<br />[Github에서 Ubuntu 또는 MacOS PHP 드라이버](http://github.com/Microsoft/msphpsql/tree/dev#install-unix) |
| Python   | [pyodbc, 설치 지침](http://docs.microsoft.com/sql/connect/python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development)<br />[ODBC를 다운로드 합니다.](http://docs.microsoft.com/sql/connect/odbc/download-odbc-driver-for-sql-server) |
| Ruby     | [Ruby 드라이버, 설치 지침](https://docs.microsoft.com/sql/connect/ruby/step-1-configure-development-environment-for-ruby-development)<br />[Ruby 다운로드 페이지](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |


<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 액세스에 대 한 드라이버


다음 표에서 Microsoft SQL 데이터베이스에 연결 하려면 클라이언트 응용 프로그램 사용 하는 개체 관계형 매핑 ORM () 프레임 워크의 예를 나열 합니다.


| 언어 | ORM 드라이버 다운로드 |
| :------- | :------------------ |
| C# | [Entity Framework Core](http://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x 이상)](http://docs.microsoft.com/ef/) |
| Java | [ORM 최대 절전 모드로 전환](http://hibernate.org/orm)|
| PHP | [알기 쉬운 ORM, Laravel 설치에 포함](http://laravel.com/docs/) |
| Node.js | [ORM sequelize](http://docs.sequelizejs.com) |
| Python | [Django](http://www.djangoproject.com/) |
| Ruby | [레일에 ruby](http://rubyonrails.org/) |
| &nbsp; | <br /> |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>웹 페이지 응용 프로그램 빌드


[http://aka.ms/sqldev](http://aka.ms/sqldev) 집합이로 이동 *응용 프로그램 빌드* 웹 페이지입니다. 웹 페이지 프로그래밍 언어, 운영 체제 및 SQL 연결 드라이버의 다양 한 조합에 대 한 정보를 제공 합니다. 응용 프로그램 빌드 웹 페이지에서 제공 하는 정보는 다음 항목:

- 운영 체제 언어 + 드라이버의 각 조합에 대해를 맨 처음부터 시작 하는 방법에 대 한 세부 정보입니다.
    - 최신 SQL 연결 드라이버를 설치 하기 위한 지침입니다.
- 다음 항목에는 각각에 대 한 코드 예제:
    - 개체-관계형 코드 예제입니다.
    - ORM 코드 예제입니다.
    - 훨씬 빠른 성능을 위해 Columnstore 인덱스 데모입니다.


#### <a name="first-page-of-build-an-app-webpages"></a>응용 프로그램 빌드 웹 페이지의 첫 번째 페이지

![웹 페이지 응용 프로그램 빌드, 첫 번째 페이지 스크린샷][image-ref-163-buildanapp-webpages-first-page]


#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Java-응용 프로그램 빌드 웹 페이지의 Ubuntu 용 메뉴

![웹 페이지 응용 프로그램 빌드, Java Ubuntu 메뉴][image-ref-167-buildanapp-webpages-menu-java-ubuntu]


&nbsp;


## <a name="related-links"></a>관련 링크

- [코드 Java 및 다른 언어를 사용 하 여 클라우드에서 Azure SQL 데이터베이스에 연결 하기 위한 예제](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)합니다.


<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
