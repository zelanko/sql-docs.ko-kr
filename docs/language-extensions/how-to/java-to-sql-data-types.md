---
title: SQL Server 2019에서 지원되는 Java 데이터 형식
titleSuffix: SQL Server Language Extensions
description: 입력 및 출력 데이터 구조와 sp_execute_external_script의 입력 매개 변수에 대해 Java의 데이터 형식을 SQL Server에 매핑합니다.
author: dphansen
ms.author: davidph
ms.date: 09/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9daca9c607befe077fcccec20385a36c82b04c6f
ms.sourcegitcommit: a97d551b252b76a33606348082068ebd6f2c4c8c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2019
ms.locfileid: "73588837"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java 및 SQL Server 지원되는 데이터 형식
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)의 데이터 구조 및 매개 변수에 대해 SQL Server 데이터 형식을 Java 데이터 형식에 매핑합니다.

현재 입력/출력 데이터 집합 및 입력/출력 매개 변수에 대해 지원되는 SQL 및 Java 데이터 형식은 다음과 같습니다.

| SQL 데이터 형식        | Java 데이터 형식 | 설명 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| 정수 | int      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | UTF8 문자열만 지원됨 | |
| varchar(n) | String | UTF8 문자열만 지원됨 | |
| varchar(max) | String | UTF8 문자열만 지원됨 | |
| 날짜 | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| Datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>다음 단계

+ [SQL Server에서 Java를 호출하는 방법](../how-to/call-java-from-sql.md)
