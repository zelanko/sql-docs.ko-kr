---
title: Always Encrypted를 사용하여 애플리케이션 개발 | Microsoft Docs
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 235dc20ca94affa5f022bc242aa0ef6726f1542c
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594442"
---
# <a name="develop-applications-using-always-encrypted"></a>Always Encrypted를 사용하여 애플리케이션 개발
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[상시 암호화](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)는 중요한 데이터 및 관련 암호화 키가 SQL Server 또는 Azure SQL 데이터베이스에 한 번도 공개된 적이 없는 클라이언트 쪽 암호화 기술입니다. 상시 암호화를 사용하여 클라이언트 드라이버에서 데이터베이스 엔진으로 데이터를 전달하기 전에 중요한 데이터를 투명하게 암호화하고 암호화된 데이터베이스 열에서 검색된 데이터를 투명하게 암호 해독합니다.

상시 암호화로 보호된 데이터베이스를 사용하는 애플리케이션을 개발하는 방법과 상시 암호화를 지원하는 클라이언트 드라이버 및 드라이버 버전에 대한 자세한 내용은 다음을 참조하세요.

- [.NET Framework Data Provider for SQL Server와 Always Encrypted 사용](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [상시 암호화와 JDBC 드라이버 사용](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [상시 암호화와 ODBC 드라이버 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [상시 암호화와 PHP 드라이버 사용](../../../connect/php/using-always-encrypted-php-drivers.md)
- [.NET Core 및 .NET Framework 애플리케이션에서 Always Encrypted 사용(Microsoft.Data.SqlClient)](https://github.com/dotnet/sqlclient/tree/master/release-notes)
- [항상 암호화](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
