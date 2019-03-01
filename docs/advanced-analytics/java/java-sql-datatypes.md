---
title: SQL Server 2019-SQL Server Machine Learning Services에서에서 지 원하는 Java 데이터 형식
description: 데이터 형식을 Java에서 SQL Server에 입력 및 출력 데이터 구조 및 입력된 매개 변수를 sp_execute_external_script 매핑하십시오.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4c0f691b8bb389c2da2001d19f0684b7f928f707
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017819"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java와 SQL Server 데이터 형식 지원

이 문서에서 SQL Server 데이터 형식을 매개 변수와 데이터 구조에 대 한 Java 데이터 형식에 매핑하 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다.

## <a name="data-types-for-data-sets"></a>데이터 집합에 대 한 데이터 형식

SQL 및 Java 데이터 형식 입력 및 출력 데이터 집합에 대 한 현재 지원 됩니다.

| SQL 데이터 형식        | Java 데이터 형식 | 설명 | |
| ------------- |-------------|-|
| 비트      | boolean | |
| Tinyint      | short      | |
| Smallint | short      | |
| Int | ssNoversion      | |
| Real | FLOAT      | |
| Bigint | long      | |
| FLOAT | double      | |
| nchar(n) | 문자열      | |
| nvarchar(n) | 문자열  | |
| binary(n) | byte[]      | |
| varbinary (n) | byte[]      | |
| nvarchar(max) | 문자열 | |
| varbinary(max) | byte[] | |
| uniqueidentifier | 문자열 | |
| char(n) | 문자열 | 지원 되는 UTF8 문자열만 |
| varchar(n) | 문자열 | 지원 되는 UTF8 문자열만 |
| varchar(max) | 문자열 | 지원 되는 UTF8 문자열만 |

## <a name="data-types-for-input-parameters"></a>입력된 매개 변수에 대 한 데이터 형식

SQL 및 Java 데이터 형식 입력된 매개 변수에 대 한 현재 지원 됩니다.

| SQL 데이터 형식        | Java 데이터 형식 | 설명 | |
| ------------- |-------------|-|-|
| 비트      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | 문자열      | | |
| nvarchar(n) | 문자열      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |
| nvarchar(max) | 문자열      | | |
| varbinary(max) | byte[]      | | |
| uniqueidentifier | 문자열 | | |
| char(n) | 문자열 | 지원 되는 UTF8 문자열만 | |
| varchar(n) | 문자열 | 지원 되는 UTF8 문자열만 | |
| varchar(max) | 문자열 | 지원 되는 UTF8 문자열만 | |

## <a name="see-also"></a>참고자료

+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [SQL Server에서 Java 언어 확장](extension-java.md)