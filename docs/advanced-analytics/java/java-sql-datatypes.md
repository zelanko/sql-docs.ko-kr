---
title: SQL Server 2019에 지원 되는 Java 데이터 형식 | Microsoft Docs
description: 데이터 형식을 Java에서 SQL Server에 입력 및 출력 데이터 구조 및 입력된 매개 변수를 sp_execute_external_script 매핑하십시오.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3510b53510514daa125382fc10ea33285fe44a80
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715437"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java와 SQL Server 데이터 형식 지원

이 문서에서 SQL Server 데이터 형식을 매개 변수와 데이터 구조에 대 한 Java 데이터 형식에 매핑하 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)합니다.

## <a name="data-types-for-data-sets"></a>데이터 집합에 대 한 데이터 형식

SQL 및 Java 데이터 형식 입력 및 출력 데이터 집합에 대 한 현재 지원 됩니다.

| SQL 형식        | Java 형식 | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| 정수 | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | 문자열 (유니코드)      | | |
| nvarchar (n) | 문자열 (유니코드)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |

## <a name="data-types-for-input-parameters"></a>입력된 매개 변수에 대 한 데이터 형식

SQL 및 Java 데이터 형식 입력된 매개 변수에 대 한 현재 지원 됩니다.

| SQL 형식        | Java 형식 | | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| 정수 | ssNoversion      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | 문자열 (유니코드)      | | |
| nvarchar (n) | 문자열 (유니코드)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |
| nvarchar(max) | 문자열 (유니코드)      | | |
| varbinary(max) | byte[]      | | |

## <a name="see-also"></a>참고자료

+ [SQL Server에서 Java를 호출 하는 방법](howto-call-java-from-sql.md)
+ [SQL Server에서 Java 샘플](java-first-sample.md)
+ [SQL Server에서 Java 언어 확장](extension-java.md)