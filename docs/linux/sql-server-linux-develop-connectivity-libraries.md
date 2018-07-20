---
title: 연결 라이브러리 및 프레임 워크 | Microsoft Docs
description: 클라이언트 앱은 다양 한 언어에서 Microsoft SQL Server 온-프레미스 또는 클라우드, Linux, Windows 나 Docker 및 Azure SQL Database 및 Azure SQL Data Warehouse에 연결 하는 데 사용할 수 있는 연결 드라이버를 나열 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: 7a2f02323a3fb02cb74da3112c084609c5fe2b34
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085015"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>연결 라이브러리 및 Microsoft SQL Server에 대 한 프레임 워크

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

체크 아웃 합니다 [자습서 시작 하기](http://aka.ms/sqldev) 를 신속 하 게 C#, Java, Node.js, PHP 및 Python과 같은 프로그래밍 언어와 시작 하 고 Linux 또는 Windows 나 Docker에서 SQL Server를 사용 하 여 macOS에서 앱을 빌드합니다.

다음 표에서 연결 라이브러리 또는 *드라이버* 연결 하 여 온-프레미스를 실행 중인 Microsoft SQL Server를 사용 하는 언어 또는 클라우드에서 Linux, Windows 또는 Docker에서 다양 한 클라이언트 응용 프로그램에서 사용할 수 있습니다 및 또한에 Azure SQL Database 및 Azure SQL Data Warehouse. 

| 언어 | 플랫폼 | 추가 자료 | 다운로드 | 시작 |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET for SQL Server](http://msdn.microsoft.com/library/mt657768.aspx) | [다운로드](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [SQL Server용 Microsoft JDBC Driver](http://msdn.microsoft.com/library/mt484311.aspx) | [다운로드](http://go.microsoft.com/fwlink/?LinkId=245496) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [SQL Server 용 PHP SQL 드라이버](http://msdn.microsoft.com/library/dn865013.aspx) | 운영 체제: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [SQL Server용 Node.js 드라이버](../connect/node-js/node-js-driver-for-sql-server.md) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Python SQL 드라이버](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [SQL Server용 Ruby 드라이버](../connect/ruby/ruby-driver-for-sql-server.md) | [시작](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [다운로드](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

다음 표에서 몇 가지 예가 클라우드, Linux, Windows 나 Docker 및 Azure SQL Database로 개체 관계형 매핑 (ORM) 프레임 워크 및 온-프레미스를 실행 중인 Microsoft SQL Server 또는 클라이언트 응용 프로그램 사용할 수 있는 웹 프레임 워크 및 Azure SQL Data Warehouse입니다. 

| 언어 | 플랫폼 | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[ORM 최대 절전 모드로 전환](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [ORM sequelize](http://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](http://rubyonrails.org/) |

## <a name="related-links"></a>관련 링크
- [SQL Server 드라이버](http://msdn.microsoft.com/library/mt654049.aspx) 클라이언트 응용 프로그램에서 연결
