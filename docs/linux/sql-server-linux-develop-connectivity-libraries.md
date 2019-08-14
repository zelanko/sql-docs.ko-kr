---
title: 연결 라이브러리 및 프레임워크
description: 클라이언트 앱이 다양한 언어에서 Linux, Windows 또는 Docker에서 온-프레미스 또는 클라우드로 실행되는 Microsoft SQL Server와 Azure SQL Database 및 Azure SQL Data Warehouse에 연결하는 데 사용할 수 있는 연결 드라이버를 나열합니다.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: dd2a70cefd0e094b53656dde99af81afca2894c1
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077466"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Microsoft SQL Server의 연결 라이브러리 및 프레임워크

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

C#, Java, Node.js, PHP 및 Python과 같은 프로그래밍 언어를 빠르게 시작하고 SQL Server on Linux나 macOS 기반 Windows 또는 Docker를 사용하여 앱을 빌드하려면 [시작 자습서](https://aka.ms/sqldev)를 확인하세요.

다음 표에는 클라이언트 애플리케이션이 다양한 언어에서 Linux, Windows 또는 Docker에서 온-프레미스 또는 클라우드로 실행되는 Microsoft SQL Server와 Azure SQL Database 및 Azure SQL Data Warehouse에 연결하는 데 사용할 수 있는 연결 드라이버 및 *드라이버*가 나와 있습니다. 

| 언어 | 플랫폼 | 추가 리소스 | 다운로드 | 시작 |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET for SQL Server](https://msdn.microsoft.com/library/mt657768.aspx) | [다운로드](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [시작](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [SQL Server용 Microsoft JDBC Driver](https://msdn.microsoft.com/library/mt484311.aspx) | [다운로드](https://go.microsoft.com/fwlink/?LinkId=245496) |  [시작](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [PHP SQL Driver for SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | 운영 체제: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [시작](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [SQL Server용 Node.js 드라이버](../connect/node-js/node-js-driver-for-sql-server.md) |  [시작](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Python SQL Driver](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [시작](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [SQL Server용 Ruby 드라이버](../connect/ruby/ruby-driver-for-sql-server.md) | [시작](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [다운로드](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

다음 표에는 클라이언트 애플리케이션이 Linux, Windows 또는 Docker에서 온-프레미스 또는 클라우드로 실행되는 Microsoft SQL Server와 Azure SQL Database 및 Azure SQL Data Warehouse에서 사용할 수 있는 ORM(Object Relational Mapping) 프레임워크 및 웹 프레임워크의 몇 가지 예가 나와 있습니다. 

| 언어 | 플랫폼 | ORM |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[Hibernate ORM](https://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel(Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>관련 링크
- 클라이언트 애플리케이션에서 연결하기 위한 [SQL Server 드라이버](https://msdn.microsoft.com/library/mt654049.aspx)
