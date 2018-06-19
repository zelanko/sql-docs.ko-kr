---
title: 상시 암호화(클라이언트 개발) | Microsoft 문서
ms.custom: ''
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b6cd19272cc7c8c3f7129b3089c7ae575350b52e
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698254"
---
# <a name="always-encrypted-client-development"></a>상시 암호화(클라이언트 개발)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[상시 암호화](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)는 중요한 데이터 및 관련 암호화 키가 SQL Server 또는 Azure SQL 데이터베이스에 한 번도 공개된 적이 없는 클라이언트 쪽 암호화 기술입니다. 상시 암호화를 사용하여 클라이언트 드라이버에서 데이터베이스 엔진으로 데이터를 전달하기 전에 중요한 데이터를 투명하게 암호화하고 암호화된 데이터베이스 열에서 검색된 데이터를 투명하게 암호 해독합니다.

상시 암호화로 보호된 데이터베이스를 사용하는 응용 프로그램을 개발하는 방법과 상시 암호화를 지원하는 클라이언트 드라이버 및 드라이버 버전에 대한 자세한 내용은 다음을 참조하세요.

- [.NET Framework Data Provider for SQL Server와 Always Encrypted 사용](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [상시 암호화와 JDBC 드라이버 사용](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [상시 암호화와 Windows ODBC 드라이버 사용](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)



## <a name="see-also"></a>참고 항목

[상시 암호화(데이터베이스 엔진)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)

