---
title: Java 데이터 형식
titleSuffix: SQL Server Language Extensions
description: 입력 및 출력 데이터 구조와 sp_execute_external_script의 입력 매개 변수에 대해 Java의 데이터 형식을 SQL Server에 매핑합니다.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 742eeac8d1255f02571f6a1e77d20cb0d8084fe3
ms.sourcegitcommit: 346a37242f889d76cd783f55aeed98023c693610
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91765757"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 및 SQL Server 지원되는 데이터 형식
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)의 데이터 구조 및 매개 변수에 대해 SQL Server 데이터 형식을 Java 데이터 형식에 매핑합니다.

현재 입력/출력 데이터 집합 및 입력/출력 매개 변수에 대해 지원되는 SQL 및 Java 데이터 형식은 다음과 같습니다.

| SQL 데이터 형식        | Java 데이터 형식 | 주석 |
| ------------- |-------------|-|
| bit      | boolean | |
| Tinyint      | short      | |
| Smallint | short      | |
| Int | int      | |
| Real | float      | |
| Bigint | long      | |
| float | double      | |
| nchar(n) | String      | |
| nvarchar(n) | String      | |
| binary(n) | byte[]      | |
| varbinary(n) | byte[]      | |
| nvarchar(max) | String      | |
| varbinary(max) | byte[]      | |
| uniqueidentifier | String | |
| char(n) | String | UTF8 문자열만 지원됨 |
| varchar(n) | String | UTF8 문자열만 지원됨 |
| varchar(max) | String | UTF8 문자열만 지원됨 |
| date | java.sql.date  | |
| numeric | java.math.BigDecimal  | |
| decimal | java.math.BigDecimal  | |
| money | java.math.BigDecimal  | |
| smallmoney | java.math.BigDecimal  | |
| smalldatetime | java.sql.timestamp  | |
| Datetime | java.sql.timestamp  | |
| datetime2 | java.sql.timestamp  | |


## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출하는 방법](../how-to/call-java-from-sql.md)