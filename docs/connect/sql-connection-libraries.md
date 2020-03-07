---
title: Microsoft SQL Database용 연결 라이브러리 | Microsoft Docs
description: 다양한 클라이언트 프로그래밍 언어에서 Microsoft SQL Server 및 Azure SQL Database에 연결할 수 있도록 돕는 모듈의 다운로드 링크를 제공합니다.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338614"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL Database용 연결 모듈

이 문서에서는 클라이언트 프로그램이 [Microsoft SQL Server](../relational-databases/database-features.md) 및 클라우드 [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/) 내 해당 쌍과의 상호 작용에 사용할 수 있는 연결 모듈 또는 *드라이버*의 다운로드 링크를 제공합니다. 드라이버는 다음의 운영 체제에서 실행되는 다양한 프로그래밍 언어에 사용할 수 있습니다.

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP-관계형 불일치

*관계형*: OOP(개체 지향 프로그래밍) 언어로 작성된 클라이언트 프로그램은 쿼리된 데이터를 개체 지향에 비해 좀 더 관계형인 형식으로 반환하는 SQL 드라이버를 사용하는 경우가 많습니다. 그 예로는 C# 사용 ADO.NET을 들 수 있습니다. OOP 코드는 때때로 OOP 관계형 형식 불일치로 인해 작성과 이해가 어려워지는 경우가 있습니다.

*ORM*: 다른 드라이버나 프레임워크는 쿼리된 데이터를 OOP 형식으로 반환하여 불일치 문제를 방지합니다. 이러한 드라이버는 클래스가 특정 SQL 테이블의 데이터 열과 일치하도록 정의되어 있어야 작동합니다. 그러면 드라이버는 *ORM*(개체-관계형 매핑)을 수행하여 쿼리된 데이터를 클래스의 인스턴스로서 반환합니다. 그 예로는 Microsoft의 C#용 EF(Entity Framework)와 Java용 Hibernate를 들 수 있습니다.

이 문서는 별도의 섹션에 이 두 가지 연결 드라이버가 설명되어 있습니다.

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
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[Linux-Ubuntu용.NET core](https://www.microsoft.com/net/core#Ubuntu)<br />[MacOS용 .NET Core](https://www.microsoft.com/net/core#macos)<br />[Windows용 .NET Core](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 드라이버, 설치 지침](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, 설치 지침](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[ODBC 다운로드](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 드라이버, 설치 지침](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 다운로드 페이지](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 액세스용 드라이버


다음 표에는 클라이언트 애플리케이션이 Microsoft SQL Database와의 연결에 사용하는 ORM(개체 관계형 매핑) 프레임워크의 예제가 나열되어 있습니다.


| 언어 | ORM 드라이버 다운로드 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework(6.x 이상)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM, Laravel 설치 시 포함됨](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>애플리케이션 빌드 웹 페이지
[https://aka.ms/sqldev](https://aka.ms/sqldev)를 클릭하면 일단의 *애플리케이션 빌드* 웹 페이지로 이동하실 수 있습니다. 해당 웹 페이지에서는 프로그래밍 언어, 운영 체제, SQL 연결 드라이버를 어떻게 다양한 방법으로 조합할 수 있을지 소개합니다. 애플리케이션 빌드 웹 페이지에서 제공되는 정보에는 다음 사항도 포함됩니다.

- 각각의 언어, 운영 체제, 드라이버 조합과 관련해 작업을 시작하는 방법을 처음부터 자세히 설명합니다.
    - 최신 SQL 연결 드라이버의 설치 방법에 대한 지침
- 다음 각 항목에 대해 코드 예제를 제공합니다.
    - 개체 관계형 코드 예제
    - ORM 코드 예제
    - 더욱 빠른 성능 실현을 위한 Columnstore 인덱스 데모

#### <a name="first-page-of-build-an-app-webpages"></a>애플리케이션 빌드 웹 페이지의 첫 페이지
![애플리케이션 빌드 웹 페이지의 첫 페이지 스크린샷][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>애플리케이션 빌드 웹 페이지의 Java 메뉴(Ubuntu)
![애플리케이션 빌드 웹 페이지의 Java 메뉴(Ubuntu)][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>관련 링크
- [클라우드에서 Java와 기타 언어로 Azure SQL Database에 연결하기 위한 코드의 예제](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
