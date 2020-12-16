---
title: Always Encrypted를 사용하여 애플리케이션 개발 | Microsoft Docs
description: 중요한 데이터가 SQL Server 또는 Azure SQL Database에 공개되지 않도록 하는 Always Encrypted 클라이언트 쪽 암호화 기술에 대해 알아봅니다.
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57a306a3a076e11d797a6da7869833e439628622
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468544"
---
# <a name="develop-applications-using-always-encrypted"></a>Always Encrypted를 사용하여 애플리케이션 개발
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

[상시 암호화](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)는 중요한 데이터 및 관련 암호화 키가 SQL Server 또는 Azure SQL 데이터베이스에 한 번도 공개된 적이 없는 클라이언트 쪽 암호화 기술입니다. 상시 암호화를 사용하여 클라이언트 드라이버에서 데이터베이스 엔진으로 데이터를 전달하기 전에 중요한 데이터를 투명하게 암호화하고 암호화된 데이터베이스 열에서 검색된 데이터를 투명하게 암호 해독합니다.

상시 암호화로 보호된 데이터베이스를 사용하는 애플리케이션을 개발하는 방법과 상시 암호화를 지원하는 클라이언트 드라이버 및 드라이버 버전에 대한 자세한 내용은 다음을 참조하세요.

- [.NET Framework Data Provider for SQL Server와 Always Encrypted 사용](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [상시 암호화와 JDBC 드라이버 사용](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [상시 암호화와 ODBC 드라이버 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [상시 암호화와 PHP 드라이버 사용](../../../connect/php/using-always-encrypted-php-drivers.md)
- [.NET Core 및 .NET Framework 애플리케이션에서 Always Encrypted 및 Microsoft .NET Data Provider for SQL Server 사용](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
